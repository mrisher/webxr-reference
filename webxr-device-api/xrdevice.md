# XRDevice

The XRDevice interface of the WebXR API provides information about a AR/VR device and methods for obtaining an AR/VR session.

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

### Creating a Non-exclusive Session

The following demonstrates using the API with a non-exclusive session. A non-exclusive session is one in which device tracking information is used to render content on a page.

```javascript
const xrPC = someCanvas.getContext('xrpresent');
const sessionsOptions = {
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

### Creating an Exclusive session

The process for creating an exclusive session is a little more complex because entering an exclusive session requires a user gesture. In this example, a button for entering AR/VR is initially hidden. A call to `supportsSession()` determines whether exclusive sessions are supported and makes an "Enter VR" button visible if they are.

```javascript
const xrPC = someCanvas.getContext('xrpresent');
const sessionsOptions = {
  exclusive: true,
  outputContext: xrPC
}
let vrDevice;

const vrButton = document.querySelector("#enterVR");
vrButton.addEventListener('click', enterVR);

navigator.xr.requestDevice()
.then(device => {
  vrDevice = device;
  device.supportsSession(sessionOptions)
  .then(session => {
    vrButton.style.display = "block";
  })
  .catch(err => {
    console.error("This browser/device combination does not support exclusive sessions.", err);
  })
})

function enterVR() {
  vrDevice.requestSession(sessionOptions)
  .then(session => {
    //Do something with the session.
  });
}
```

## Specifications

https://immersive-web.github.io/webxr/spec/latest/#xrdevice-interface

## Browser Compatibility

* Chrome 66 or later.
