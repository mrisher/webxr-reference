# WebXR API

The WebXR Device API lets you create augmented reality and virtual reality web sites by providing access to input and output capabilities of AR/VR hardware. As of early 2018, examples include [Google’s Daydream](https://vr.google.com/daydream/), the [Oculus Rift](https://www3.oculus.com/rift/), the [Samsung Gear VR](http://www.samsung.com/global/galaxy/gear-vr/), the [HTC Vive](https://www.htcvive.com/), and [Windows Mixed Reality headsets](https://developer.microsoft.com/en-us/windows/mixed-reality).

## Concepts and Usage

Intro - TBD

### What's the X in XR mean?

There are many "&#95;&#95;&#95; reality" buzzwords flying around today. _virtual reality_, _augmented reality_, _mixed reality_, etc.. It can be hard to keep track, even though there are many similarities between them. This API aims to provide foundational elements with which to do all of the above. Since the designers of the API don't want to be limited to just one facet of AR, VR, or anything in between, the "X" in "XR" is not part of an acronym, but an algebraic variable of sorts to refer to whatever a web developer needs or wants it to be.

### Exclusive versus Non-Exclusive Sessions

There are two types of sessions: exclusive sessions and non-exclusive sessions.

**Exclusive session:** An immersive presentation in which content is presented directly to the device. Entering an exclusive session requires a user gesture.

**Non-exclusive session:** A non-immersive presentation in which device tracking information is used to render content on a page. This is sometimes referred to as "magic window" mode. It enables the viewer to look around a scene by moving the device.

### Frame of Reference Types

A frame of reference describes the space or stage in which AR/VR content will be created. Each frame of reference implies two facts that you need to be aware of when drawing content.

* Where is the origin of the coordinate system?
* What happens to the origin when the viewer moves?

A frame of reference can be one of three types.

* `"headModel"`&mdash;The origin is approximately the location of the viewer's head and does not change if the viewer moves.
* `"eyeLevel"`&mdash;The origin is the viewer's head and moves with the viewer.
* `"stage"`&mdash;The origin is implied to be the center of the room at floor level and does not change if the viewer moves.

The `"eyeLevel"` and `"stage"` frames of reference are referred to as 'room scale' frames of reference.

### Matrices

Some WebXR objects return data in the form of matrices. WebXR matrices are always 4 by 4 and returned as 16 element `Float32Arrays` in column major order. They may be passed directly to WebGL's `uniformMatrix4fv()` method, used to create an equivalent `DOMMatrix`, or used with a variety of third-party math libraries. Values in WebXR matrices are always given in meters.

### Lifetime of an AR/VR Web Application

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

#### Request a device

The WebXR Device API added the [XR](xr) interface to the `navigator` object. Use this to do both feature detection and requesting a device. The code below demonstrates this with a few necessary elaborations.

Notice that `XR.requestDevice()` returns a promise that resolves with an `XRDevice` object or rejects with a `NotFoundError`.

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
    } else {
      // An error occurred while requesting an XRDevice.
      console.error('Requesting XR device failed:', err);
    }
  })
} else{
  console.log("This browser does not support the WebXR API.");
}
```
#### For an Exclusive Session, Get a User Gesture

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

#### Or, Just Get a Non-exclusive Session

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

#### Create a Graphics Layer

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

#### Start the Render loop

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

#### The Render Loop

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

#### Exit VR

TBD

### Recovering from a Null pose

TBD

## WebVR Device Interfaces

### Device Enumeration

<dl>
  <dt><a href="xr">XR</a></dt>
  <dd>Provides the means to query for attached AR/VR devices and receive events when device availability changes. A requested device is accessed through a returned `XRDevice` object.</dd>
  <dt><a href="xrdevice">XRDevice</a></dt>
  <dd>Provides information about a AR/VR device and methods for obtaining an `XRSession object`. Once a session is obtained, subsequent interactions with the hardware are done through it.</dd>
</dl>

### Sessions

<dl>
  <dt><a href="xrsession">XRSession</a></dt>
  <dd>Provides the means to interact with an AR/VR device, providing features such as polling the device pose, getting information about the user's environment, and presenting imagery to the user.</dd>
  <dt><a href="xrsessionevent">XRSessionEvent</a></dt>
  <dd>The event type passed to all of the `XRSession` events, specifically, `onblur`, `onfocus`, `onresetpose`, and `onend`.</dd>
</dl>

### Frame Loop

<dl>
  <dt><a href="xrpresentationframe">XRPresentationFrame</a></dt>
  <dd>Provides all of the values needed to render a single frame of an AR/VR scene to the display represented by the `XRDevice` interface.</dd>
</dl>

### Coordinate Systems

<dl>
  <dt><a href="xrcoordinatesystem">XRCoordinateSystem</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrcoordinatesystemevent">XRCoordinateSystemEvent</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrframeofreference">XRFrameOfReference</a></dt>
  <dd>Provides information about the spatial point from which AR/VR measurements are made.</dd>
  <dt><a href="xrxrstagebounds">XRStageBounds</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrxrstageboundspoint">XRStageBoundsPoint</a></dt>
  <dd>TBD</dd>
</dl>

### Views

<dl>
  <dt><a href="xrview">XRView</a></dt>
  <dd>Describes a single view into an AR/VR scene. Each view corresponds to a display or portion of a display used by a device to present imagery to the user.</dd>
  <dt><a href="xrviewport">XRViewport</a></dt>
  <dd>Describes a viewport, or rectangular region, of a graphics surface.</dd>
</dl>

### Poses

<dl>
  <dt><a href="xrdevicepose">XRDevicePose</a></dt>
  <dd>Describes the position and orientation of an <a href="xrdevice">XRDevice</a> relative to the <a href="xrcoordinateSystem">XRCoordinateSystem</a> it was queried with. It also describes the view and projection matrices that should be used by the application to render a frame of an AR/VR scene.</dd>
</dl>

### Input

<dl>
  <dt><a href="xrinputsource">XRInputSource</a></dt>
  <dd>Returns information about the Web AR/VR control device being used. The control device is platform-specific and defines a primary action. A primary action is a trigger, touchpad, button, spoken command, or hand gesture that when performed produces selectstart, selectend, and select events.</dd>
  <dt><a href="xrinputpose">XRInputPose</a></dt>
  <dd>Returns information about the pose (position) of the input device in 3D space.</dd>
</dl>

### Layers

<dl>
  <dt><a href="xr">XRLayer</a></dt>
  <dd>Defines a source of bitmap images and a description of how the image is to be rendered in the device. Do not use this interface directly. Rather use one of its subtypes. As of the first version of the [WebXR Device API](https://immersive-web.github.io/webxr/) only one subtype, `XRWebGLLayer` is supported.</dd>
  <dt><a href="xr">XRWebGLLayer</a></dt>
  <dd>An XRLayer subtype that allows WebGL to provide the bitmaps to be rendered to a device.</dd>
</dl>

### Canvas Rendering Context

<dl>
  <dt><a href="xr">XRPresentationContext</a></dt>
  <dd>A wrapper object for the \{\{domxref("HTMLCanvasElement")\}\} object on which AR or VR content will be drawn. To retrieve an instance of this object, call `getContext()` on a canvas object with the value `'xrpresent'`.</dd>
</dl>

### Partial Interfaces

<dl>
  <dt><a href="partial_navigator">navigator.xr</a></dt>
  <dd>Returns a new XR object.</dd>
  <dt><a href="partial_webglcontextattributes">WebGLRenderingContex.setCompatibleXRDevice()</a></dt>
  <dd>Sets an <a href="xrdevice">XRDevice</a> after a presentation context has been created.</dd>
</dl>

## Examples


## Specifications

[Latest](https://immersive-web.github.io/webxr/spec/latest/)

## Browser Compatibility

* Chrome 66 or later

## See Also

[Glossary of AR/VR Terms](glossary.md)
