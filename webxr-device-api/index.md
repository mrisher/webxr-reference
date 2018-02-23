# WebXR API

## Concepts and Usage

This section should eventually answer the following questions:

* How do I get a device (`XRDevice`)?
* What happens to the device object during navigation?

## WebVR Device Interfaces

### Device Enumeration

<dl>
  <dt><a href="xr.md">XR</a></dt>
  <dd>Provides the means to query for attached AR/VR devices and receive events when device availability changes. A requested device is accessed through a returned XRDevice object.</dd>
  <dt><a href="xrdevice.md">XRDevice</a></dt>
  <dd>Provides information about a AR/VR device and methods for obtaining an XRSession object. Once a session is obtained, subsequent interactions with the hardware are done through it.</dd>
</dl>

### Sessions

<dl>
  <dt><a href="xrsession.md">XRSession</a></dt>
  <dd>Provides the means to interact with an AR/VR device, providing features such as polling the device pose, getting information about the user's environment, and presenting imagery to the user.</dd>
  <dt><a href="xrsessionevent.md">XRSessionEvent</a></dt>
  <dd>TBD</dd>
</dl>

### Frame Loop

<dl>
  <dt><a href="xrpresentationframe.md">XRPresentationFrame</a></dt>
  <dd>rovides all of the values needed to render a single frame of an AR/VR scene to the display represented by the XRDevice interface.</dd>
</dl>

### Coordinate Systems

<dl>
  <dt><a href="xrcoordinatesystem.md">XRCoordinateSystem</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrcoordinatesystemevent.md">XRCoordinateSystemEvent</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrframeofreference.md">XRFrameOfReference</a></dt>
  <dd>Provides information about the spatial point from which AR/VR measurements are made.</dd>
  <dt><a href="xrxrstagebounds.md">XRStageBounds</a></dt>
  <dd>TBD</dd>
  <dd>TBD</dd>
  <dt><a href="xrxrstageboundspoint.md">XRStageBoundsPoint</a></dt>
  <dd>TBD</dd>
</dl>

### Views

<dl>
  <dt><a href="xrview.md">XRView</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrviewport.md">XRViewport</a></dt>
  <dd>TBD</dd>
</dl>

### Poses

<dl>

  <dt><a href="xrdevicepose.md">XRDevicePose</a></dt>
  <dd>Represents the state of a VR sensor at a specific timestamp. Sensor state includes orientation, position, velocity, and acceleration information.</dd>
</dl>

### Layers

<dl>
  <dt><a href="xr.md">XRLayer</a></dt>
  <dd>TBD</dd>
  <dt><a href="xr.md">XRWebGLLayer</a></dt>
  <dd>TBD</dd>
</dl>

## Canvas Rendering Context

<dl>
  <dt><a href="xr.md">XRPresentationContext</a></dt>
  <dd>TBD</dd>
</dl>

### Partial Interfaces

<dl>
  <dt><a href="partial_navigator.md">navigator.xr</a></dt>
  <dd>TBD</dd>
  <dt><a href="partial_webglcontextattributes.md">WebGLRenderingContex.setCompatibleXRDevice()</a></dt>
  <dd>TBD</dd>
</dl>

## Examples

## Specifications

## Browser Compatibility
