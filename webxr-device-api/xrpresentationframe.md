# XRPresentationFrame

The **`XRPresentationFrame`** interface of the WebXR Device API provides all of the values needed to render a single frame of an AR/VR scene to the display represented by the <a href="xrdevice.md">XRDevice</a> interface.

## Properties

<dl>
  <dt>views</dt>
  <dd>Returns an array of scene views. A view is a display or portion of a display used by an AR/VR device to present imagery to the viewer.</dd>
</dl>

## Methods

<dl>
  <dt>getDevicePose()</dt>
  <dd>Takes an <a href="xrpresentationframe">XRPresentationFrame</a> object and Returns the state of the VR sensor for that object. Unless the value of `XRFrameOfReference` is `"headMode"`, this function is not guaranteed to return a value.</dd>
</dl>

## Examples

## Specifications

[XRPresentationFrame Interface](https://immersive-web.github.io/webxr/spec/latest/#xrpresentationframe-interface)

## Browser Compatibility

* Chrome 66 or later.
