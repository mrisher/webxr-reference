# XRDevice

The **`XRDevice`** interface of the WebXR API represents a single AR/VR hardware device and provides methods for obtaining an <a href="xrsession">XRSession</a> object. Once a session is obtained, subsequent interactions with the hardware are done through it.

A hardware devices generally fall into the following categories:

* On desktop clients, a headset peripheral.
* On mobile clients, the mobile device itself and used with a viewer harness such as Google Daydream Viewer or Samsung Gear VR.
* Devices without stereo-presentation capabilities but with more advanced tracking, such as ARCore/ARKit-compatible devices.

__Note:__ The specification does not mandate how the API should behave when multiple devices are found. If this is a concern for your use case, you should test multiple device scenarios on several browsers and adapt your application to the results.

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
    <li><code>outputContext</code>: A reference to an <a href="xrpresentationcontext">XRPresentationContext</a> object.</li>
  </ul>
  </dd>
  <dt>requestSession(options)</dt>
  <dd>Returns a \{\{jsxref("Promise")\}\} that resolves with an <a href="xrsession">XRSession</a> object meeting the requested options.</dd>
</dl>

## Examples

This example shows that retrieving a device is a prerequisite for retrieving a session. Note that the code below should only be used for non-exclusive sessions. A user gesture is required to request an exclusive session. For an example, see the <a href="xrsession">XRSession</a> interface.

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

[XRDevice Interface](https://immersive-web.github.io/webxr/spec/latest/#xrdevice-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags. Requires Android O or later. |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
