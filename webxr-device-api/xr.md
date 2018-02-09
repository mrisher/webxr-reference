# XR

The XRDevice interface of the WebXR API is the entry point to the API, providing the means to query for attached devices and receive events when device availability changes.

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
  <dd>TBD</dd>
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

https://immersive-web.github.io/webxr/spec/latest/#xr-interface

## Browser Compatibility

* Chrome 66 or later
