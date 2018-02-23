# WebXR API

The WebXR Device API lets you create augmented reality and virtual reality web sites by providing access to input and output capabilities of AR/VR hardware. As of early 2018, examples include [Google’s Daydream](https://vr.google.com/daydream/), the [Oculus Rift](https://www3.oculus.com/rift/), the [Samsung Gear VR](http://www.samsung.com/global/galaxy/gear-vr/), the [HTC Vive](https://www.htcvive.com/), and [Windows Mixed Reality headsets](https://developer.microsoft.com/en-us/windows/mixed-reality).  

## Concepts and Usage

This section should eventually answer the following questions:

* How do I get a device (`XRDevice`), a session (`XRSession`), a context (`xrPresentationContext`) etc.?
* How is XR functionality advertised to the viewer?
* What is a presentation loop and how do I implement it?
* What happens to the device object during navigation?

### What's the X in XR mean?

There are many "_____ Reality" buzzwords flying around today. _virtual reality_, _augmented reality_, _mixed reality_, etc.. It can be hard to keep track, even though there are many similarities between them. This API aims to provide foundational elements with which to do all of the above. Since the designers of the API don't want to be limited to just one facet of AR, VR, or anything in between, the "X" in "XR" is not part of an acronym, but an algebraic variable of sorts to refer to whatever a web developer needs or wants it to be.

## WebVR Device Interfaces

### Device Enumeration

<dl>
  <dt><a href="xr">XR</a></dt>
  <dd>Provides the means to query for attached AR/VR devices and receive events when device availability changes. A requested device is accessed through a returned XRDevice object.</dd>
  <dt><a href="xrdevice">XRDevice</a></dt>
  <dd>Provides information about a AR/VR device and methods for obtaining an XRSession object. Once a session is obtained, subsequent interactions with the hardware are done through it.</dd>
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
  <dd>rovides all of the values needed to render a single frame of an AR/VR scene to the display represented by the XRDevice interface.</dd>
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

## Browser Compatibility
