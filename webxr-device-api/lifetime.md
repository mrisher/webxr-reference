# Lifetime of an AR/VR Web Application

The lifetime of an AR/VR web application is generally as follows.

1. Request a _device_ through the API.
1. If a device is available, do one of two things.
   * For an _exclusive session_, advertise the AR/VR functionality to the viewer and prompt the user to enter AR/VR. If the user accepts use the _user gesture_ to request a _session_.
   * For a _non-exclusive_ session simply request the session.
1. Create a _graphics layer_ to provide bitmap images to the device.
1. Use the session to run a _render loop_, which produces graphical _frames_ and displays them to the device.
1. For each frame loop through its _views_ and draw content to them.
1. Repeat the render loop until the user decides to exit AR/VR.

Let's look at each step in detail.

## Request a device

The WebXR Device API added the [XR](xr) interface to the `navigator` object. Use this to do both feature detection and requesting a device. The code below demonstrates this with a few necessary elaborations.

Notice that `XR.requestDevice()` returns a promise that resolves with an `XRDevice` object or rejects with a `NotFoundError`. Another possibility is `NotAllowedError`, which occurs when device permissions have not been granted. See [Requesting Device Permissions](permissions) for more information.

```javascript
if (navigator.xr) {
  navigator.xr.requestDevice()
  .then(xrDevice => {
    // Advertise the AR/VR functionality to get a user gesture.
  })
  .catch(err => {
    if (err.name === 'NotFoundError') {
      // No XRDevices available.
      console.error('No XR devices available:', err);
    else if (err.name === 'NotAllowedError') {
      // Permissions have not been granted.
      // Trigger permission flow.
    } else {
      // An error occurred while requesting an XRDevice.
      console.error('Requesting XR device failed:', err);
    }
  })
} else{
  console.log("This browser does not support the WebXR API.");
}
```
## For an Exclusive Session, Get a User Gesture

For an exclusive session entering AR/VR requires a user gesture. Start by defining session options, which includes both the type of session and a presentation context, which is actually the `HTMLCanvasElement` where AR/VR content will be displayed.

The example below shows this. Note that when calling `getContext()` you must pass the `'xrpresent'` keyword, which is new with the WebXR specification.

```javascript
xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
let sessionOptions = {
  exclusive: true,
  outputContext: xrPresentationContext
}
```

Call `supportsSession()` with your chosen session options. If it succeeds, use the returned promise to display or enable a control for entering VR. The example below does this by flipping a button's display from `"none"` to `"block"`.

```javascript
xrDevice.supportsSession(sessionOptions)
.then(()) => {
  // Make the button visible by changing "none" to "block".
  xrButton.style.display = "block";
})
.catch(err => {
  logger.error("AR/VR session could not be created. ", err);
})
```

Use the displayed control's event handler to call `requestSession()`. It returns a promise that resolves with an `xrSession` object.

```javascript
xrButton.addEventListener('click', (event) => {
  xrDevice.requestSession(sessionOptions)
  .then(session => {
    // Initialize the render loop.
  });
})
```

## Or, Just Get a Non-exclusive Session

If you're using a non-exclusive session, also called a "magic window", getting a session is much simpler. As before, you need a context and a session options object.

```javascript
xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
let sessionOptions = {
  // The exclusive option is optional for non-exclusive sessions; the value
  //   defaults to false.
  exclusive: false,
  outputContext: xrPresentationContext
}
```

This time you can skip the user gesture and go straight to requesting the session.

```javascript
xrDevice.requestSession(sessionOptions)
.then(session => {
  // Create a graphics layer and initialize the render loop.
})
```

## Create a Graphics Layer

Note: The remaining steps rely on WebGL. To avoid turning this into a WebGL tutorial, it will use [Cottontail](https://github.com/immersive-web/webxr-samples/tree/master/js/cottontail), a simple WebGL framework used in the [samples from the Immersive Web Community Group](https://github.com/immersive-web/webxr-samples). This is also not a tutorial on Cottontail, so it may gloss over things for the benefit of focusing on WebXR.

Presenting AR or VR to a viewer requires a source of bitmaps. This source of bitmaps must be supplied by one of the `XRLayer` interface's subtypes. The code below uses an `XRWebGLLayer` subtype (which is the only one supported in the first version of the WebXR specification).

As stated, this code relies heavily on Cottontail. The actual creation of the bitmap source, as far as WebXR is concerned is near the bottom. The sessions base layer gets an instance of `XRWebGLLayer`.

```javascript
// Do some Cottontail stuff.
let scene = new Scene();
scene.addNode(new CubeSea());

xrDevice.requestSession(sessionOptions)
.then(session => {
  // Use Cottontail's createWebGLContext() method.
  gl = createWebGLContext({
    // It needs an instance of XRDevice.
    compatibleXRDevice: session.device
  });
  // Use Cottontail's Renderer object.
  renderer = new Renderer(gl);
  scene.setRenderer(renderer);
  session.baseLayer = new XRWebGLLayer(session, gl);

  // Initialize the render loop.
})
```

## Start the Render loop

Before you can start the render loop you need an `XRFrameOfReference` object which describes the space or stage in which AR/VR content will be created. There are different types, so one must be specified when calling `requestFrameOfReference()`. (See "Frame of Reference Types" above.) This function returns a promise that resolves with an <a href="xrframeofreference">XRFrameOfReference</a> object. If and only if the promise resolves you call `requestAnimationFrame()` to start the render loop.

This function takes a callback function. Notice below that this callback is defined separately instead of as a lamda in `requestAnimationFrame()`. This is because it needs to be called repeatedly while the render loop runs.

```javascript
let xrFrameOfRef = null;

xrDevice.requestSession(sessionOptions)
.then(session => {
  // Set up Cottontail and get an XRWebGLLayer.

  session.requestFrameOfReference('eyeLevel')
  .then(frameOfRef => {
    xrFrameOfRef = frameOfRef;
    session.requestAnimationFrame(onFrame)
  })
})

function onFrame(time, frame) {
  // Continue the render loop.
}
```

## The Render Loop

Conceptually the render loop is pretty simple.

1. Request an animation frame.
1. In the animation frame get an <a href="xrdevicepose">XRDevicePose</a> object.
1. Loop through it's <a href="xrview">XRView</a> objects, and draw a scene to each view.
1. repeat until the viewer choses to quit.

Where it gets complex, is with the drawing of graphics to the views. As stated before, that complexity is outside the scope of this article.

The code below shows the basic structure excluding any graphics work. This code is not usable as is. It's intended to make the render loop easier to understand. We'll add graphic drawing code later.

```javascript
session.requestAnimationFrame(onFrame);

function onFrame(time, frame) {
  let pose = frame.getDevicePose(xrFrameOfRef);
  if (pose) {
    for (let view of frame.views) {
      scene.draw(view.projectionMatrix, pose.getViewMatrix(view))
    }
  }
  frame.session.requestAnimationFrame(onFrame);
}
```
There are a few things to call out. First, you should always check that pose did not return `null`. There are a number of reasons this might happen and testing for it prevents later code from throwing exceptions. (See Recovering from a null Poses for details.)

The next `requestAnimationFrame()` call can occur anywhere inside the frame callback.

If I add the graphics stuff, the code looks like this.

```javascript
function onFrame(time, frame) {
  let session = frame.session;
  let layer = new XRWebGLLayer(session, gl);
  scene.startFrame();
  gl.bindFramebuffer(gl.FRAMEBUFFER, session.baseLayer.framebuffer);
  gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
  let pose = frame.getDevicePose(xrFrameOfRef);
  if (pose) {
    for (let view of frame.views) {
      let viewport = layer.getViewport(session.baseLayer);
      gl.viewport(viewport.x, viewport.y,
                  viewport.width, viewport.height);
      scene.draw(view.projectionMatrix, pose.getViewMatrix(view));
    }
  }
  frame.session.requestAnimationFrame(onFrame);
  scene.endFrame();
}
```

## Exit VR

TBD

## Recovering from a null Pose
