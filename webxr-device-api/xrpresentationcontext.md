# XRPresentationContext

The `**XRPresentationContext**` interface of the WebXR API is a wrapper object for the \{\{domxref("HTMLCanvasElement")\}\} object on which AR or VR content will be drawn. To retrieve an instance of this object, call `getContext()` on a canvas object with the value `'xrpresent'`.

## Properties

<dl>
  <dt>canvas \{\{readonlyinline\}\}</dt>
  <dd>A reference to an \{\{domxref("HTMLCanvasElement")\}\} on which AR or VR content will be drawn.</dd>
</dl>

## Methods

None.

## Examples

The following example uses an instance of `XRPresentationContext` to query an XRDevice object for session support. Though this code tries to convey something of the full context where the interface is used, getting and using it comes down to this:

```javascript
xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
xrSessionOptions = {
  exclusive: true,
  outputContext: xrPresentationContext
}
xrDevice.supportsSession(xrSessionOptions)
.then(() => {
  // Do something else.
}0;
```

Here's the full example.

```javascript
let xrDevice = null;
let xrSessionOptions = null;
const htmlCanvasElement = document.querySelector("#vr");
const button = document.querySelector("#enterVR");
button.addEventListener('click', _enterVR);
button.style.display = "none";

navigator.xr.requestDevice()
.then(device => {
  if (device) {
    xrDevice = device;
    xrPresentationContext = htmlCanvasElement.getContext('xrpresent');
    xrSessionOptions = {
      exclusive: true,
      outputContext: xrPresentationContext
    }
    xrDevice.supportsSession(xrSessionOptions)
    .then(() => {
      // Exclusive sessions require a user gesture to enter AR/VR. Now that we
      // know we can get a session, show the 'Enter VR' button.
      button.style.display = "block";
    })
  }
});

function _enterVR() {
  xrDevice.requestSession(xrSessionOptions)
  .then(session => {
    // Continue on to the event loop.
  });
}
```

# Specifications

[XRFrameOfReference Interface](https://immersive-web.github.io/webxr/spec/latest/#xrpresentationcontext)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags. Requires Android O or later. |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
