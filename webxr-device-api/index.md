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

### Lifetime of an AR/VR web application

The lifetime of an AR/VR web application is generally as follows.

1. Request a device through the API.
1. If a device is available, the application advertises the AR/VR functionality to the viewer.
1. The viewer responds with a user gesture, which triggers a request for a session. (Though, certain types of AR/VR experiences do not require a user gesture to enter a session. More about this later.)
1. Use the session to run a _render loop_, which produces graphical frames and displays them to the device.
1. Continue producing frames until the user indicates that they want to exit AR/VR.

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

#### Advertise the AR/VR functionality

In most cases entering AR/VR requires a user gesture. Start by calling `XRDevice.supportsSession()` with options for the type of session you want. The example shown creates an exclusive session, which is one in which content is presented directly to the device. (See "Exclusive versus Non-Exclusive Sessions", below.) The session options must include a reference to an `xrPresentationContext`. Retrieve this by calling `getContext()` on a canvas element.

If the session type is available, this call returns a promise that resolves with an `XRSession` object. Use the promise resolution to display or enable a control for entering VR. The example below does this by flipping a button's display from `"none"` to `"block"`.

```javascript
xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
sessionOptions = {
  exclusive: true,
  outputContext: xrPresentationContext
}
xrDevice.supportsSession(sessionOptions)
.then(()) => {
  // Make the button visible by changing "none" to "block".
  xrButton.style.display = "block";
})
.catch(err => {
  logger.error("AR/VR session could not be created. ", err);
})
```

#### Request a Session

```javascript
xrButton.addEventListener('click', (event) => {
  xrDevice.requestSession(sessionOptions)
  .then(session => {
    // initialize the render loop
  });
})
```

#### Run the Render loop

#### Exit VR

### Exclusive versus Non-Exclusive Sessions

It's been mentioned a few times that there are two types of sessions: exclusive sessions and non-exclusive sessions.

**Exclusive session:** An immersive presentation in which content is presented directly to the device.

**Non-exclusive session:** A non-immersive presentation in which device tracking information is used to render content on a page. This is sometimes referred to as "magic window" mode. It enables the viewer to look around a scene by moving the device.

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
  <dd>TBD</dd>
  <dt><a href="xrviewport">XRViewport</a></dt>
  <dd>TBD</dd>
</dl>

### Poses

<dl>

  <dt><a href="xrdevicepose">XRDevicePose</a></dt>
  <dd>Represents the state of a VR sensor at a specific timestamp. Sensor state includes orientation, position, velocity, and acceleration information.</dd>
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
