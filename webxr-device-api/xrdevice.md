# XRDevice

The `**XRDevice**` interface of the WebXR API provides information about a AR/VR device and methods for obtaining an <a href="xrsession.md">XRSession</a> object. Once a session is obtained, subsequent interactions with the hardware are done through it.

## Properties

<dl>
  <dt>external</dt>
  <dd>Indicates whether the device hardware is a separate physical display from the system's main display.</dd>
</dl>

## Methods

<dl>
  <dt>supportsSession(options)</dt>
  <dd>Returns an empty promise that resolves if the requested options are available from the device. Valid options are
  <ul>
    <li><code>exclusive</code>: Indicates whether an exclusive session is desired.</li>
    <li><code>outputContext</code>: A reference to an <a href="xrpresentationcontest.md">XRPresentationContext</a> object.</li>
  </ul>
  </dd>
  <dt>requestSession(options)</dt>
  <dd>Returns a {{jsxref("Promise")}} that resolves with an <a href="xrsession.md">XRSession</a> object meeting the requested options.</dd>
</dl>

## Examples

This example shows that retrieving a device is a prerequisite for retrieving a session. Note that the code below should only be used for non-exclusive sessions. A user gesture is required to request an exclusive session. For an example, see the <a href="xrsession.md">XRSession</a> interface.

```javascript
const xrPC = someCanvas.getContext('xrpresent');
const sessionOptions = {
  exclusive: false,
  outputContext: xrPC
}

navigator.xr.requestDevice()
.then(device => {
  device.requestSession(sessionOptions)
  .then(session => {
    //Do something with the session.
  })
});
```

## Specifications

https://immersive-web.github.io/webxr/spec/latest/#xrdevice-interface

## Browser Compatibility

* Chrome 66 or later.
