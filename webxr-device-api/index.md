# WebXR API

The WebXR Device API lets you create augmented reality and virtual reality web sites by providing access to input and output capabilities of AR/VR hardware. As of early 2018, examples include [Google’s Daydream](https://vr.google.com/daydream/), the [Oculus Rift](https://www3.oculus.com/rift/), the [Samsung Gear VR](http://www.samsung.com/global/galaxy/gear-vr/), the [HTC Vive](https://www.htcvive.com/), and [Windows Mixed Reality headsets](https://developer.microsoft.com/en-us/windows/mixed-reality).

## Concepts and Usage

This section will eventually answer the following questions:

[x] How do I get a device (`XRDevice`), a session (`XRSession`), a context (`XRPresentationContext`) etc.?
[x] How is XR functionality advertised to the viewer?
[] What is a presentation loop and how do I implement it?
[] What happens to the device object during navigation?
[] What do I do differently to get AR (as opposed to VR)?

### What's the X in XR mean?

There are many "&#95;&#95;&#95; reality" buzzwords flying around today. _virtual reality_, _augmented reality_, _mixed reality_, etc.. It can be hard to keep track, even though there are many similarities between them. This API aims to provide foundational elements with which to do all of the above. Since the designers of the API don't want to be limited to just one facet of AR, VR, or anything in between, the "X" in "XR" is not part of an acronym, but an algebraic variable of sorts to refer to whatever a web developer needs or wants it to be.

### Exclusive versus Non-Exclusive Sessions

There are two types of sessions: exclusive sessions and non-exclusive sessions.

**Exclusive session:** An immersive presentation in which content is presented directly to the device. Entering an exclusive session requires a user gesture.

**Non-exclusive session:** A non-immersive presentation in which device tracking information is used to render content on a page. This is sometimes referred to as "magic window" mode. It enables the viewer to look around a scene by moving the device.

### Lifetime of an AR/VR web application

The lifetime of an AR/VR web application is generally as follows.

1. Request a _device_ through the API.
1. If a device is available, do one of two things.
   * For an exclusive session, _advertise_ the AR/VR functionality to the viewer and prompt the user to enter AR/VR. If the user accepts use the user gesture to request a _session_.
   * For a non-exclusive session simply request the session.
1. Use the session to run a _render loop_, which produces graphical _frames_ and displays them to the device.
1. Within each frame loop through _views_ and draw content to them.
1. Repeat the render loop until the user decides to exit AR/VR.


Let's look at each step in detail.

#### Request a device

The WebXR Device API added the [XR](xr) interface to the `navigator` object. Use this to do both feature detection and requesting a device. The code below demonstrates this with a few necessary elaborations.

Notice that `XR.requestDevice()` returns a promise that resolves with an `XRDevice` object or rejects with a `NotFoundError`.

```javascript
if (navigator.xr) {
  navigator.xr.requestDevice()
  .then(xrDevice => {
    // Advertise the AR/VR functionality.
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

Use the displayed control's event handler to call `requestSession()`. It returns a promise that resolves with `xrSession` object.

```javascript
xrButton.addEventListener('click', (event) => {
  xrDevice.requestSession(sessionOptions)
  .then(session => {
    // Initialize the render loop.
  });
})
```

#### Or, Just Get a Non-exclusive Session

If you're using a non-exclusive session, a "magic window", some call it, getting a session is much simpler. As before, you need a context and a session options object.

```javascript
xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
let sessionOptions = {
  // The exclusive option is option for non-exclusive sessions; the value
  //   defaults to false.
  exclusive: false,
  outputContext: xrPresentationContext
}
```

This time you can skip the user gesture and go straight to requesting the session.

```javascript
xrDevice.requestSession(sessionOptions)
.then(session => {
  // Initialize the render loop.
})
```

#### Start the Render loop

#### Draw Content to the Views

#### Exit VR



### matrices

Some WebXR ojbects return data in the form of matrices. WebXR matrices are always 4 by 4 and returned as 16 element `Float32Arrays` in column major order. They may be passed directly to WebGL's `uniformMatrix4fv()` method, used to create an equivalent `DOMMatrix`, or used with a variety of third-party math libraries. Values in WebXR matrices are always given in meters.

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
  <dd>TBD</dd>
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

### Layers

<dl>
  <dt><a href="xr">XRLayer</a></dt>
  <dd>TBD</dd>
  <dt><a href="xr">XRWebGLLayer</a></dt>
  <dd>TBD</dd>
</dl>

## Canvas Rendering Context

<dl>
  <dt><a href="xr">XRPresentationContext</a></dt>
  <dd>TBD</dd>
</dl>

### Partial Interfaces

<dl>
  <dt><a href="partial_navigator">navigator.xr</a></dt>
  <dd>TBD</dd>
  <dt><a href="partial_webglcontextattributes">WebGLRenderingContex.setCompatibleXRDevice()</a></dt>
  <dd>TBD</dd>
</dl>

## Examples


## Specifications

[Latest](https://immersive-web.github.io/webxr/spec/latest/)

## Browser Compatibility

* Chrome 66 or later

## See Also

[Glossary of AR/VR Terms](glossary.md)
