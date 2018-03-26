# XR

The **`XR`** interface of the of the WebXR API provides the means to query for attached AR/VR devices and receive events when device availability changes. A requested device is accessed through a returned <a href="xrdevice">XRDevice</a> object.

## Properties

None.

### Event Handlers

<dl>
  <dt>ondevicechange</dt>
  <dd>Called with a standard Event whenever device availability changes. To get a reference to the device, call <code>requestDevice()</code>. </dd>
</dl>

## methods

<dl>
  <dt>requestDevice()</dt>
  <dd>Returns a \{\{jsxref("Promise")\}\} that resolves with an <a href="xrdevice">XRDevice</a> object that provides information about an AR/VR device and methods for obtaining an <a href="xrsession.md">XRSession</a> object.</dd>
</dl>

## Examples

The following example uses the `ondevicechange` event to discover when a new device is available, then calls `requestDevice()` to retrieve it.

```javascript
navigator.xr.addEventListener('devicechange', () => {
  navigator.xr.requestDevice()
  .then(device => {
    // device is of type XRDevice. Use it to get an XRSession object.
  })
})
```

## Specifications

[XR Interface](https://immersive-web.github.io/webxr/spec/latest/#xr-interface)

## Browser Compatibility

* Chrome 66 or later
