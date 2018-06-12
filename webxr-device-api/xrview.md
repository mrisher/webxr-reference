# XRView

The **`XRView`** interface of the of the WebXR API describes a single view into an AR/VR scene. Each view corresponds to a display or portion of a display used by a device to present imagery to the user. Views are used to retrieve all the information necessary to render content that is well aligned to the view's physical output properties, including the field of view, eye offset, and other optical properties.

## Properties

<dl>
  <dt>eye</dt>
  <dd>TBD</dd>
  <dt>projectionMatrix</dt>
  <dd>TBD</dd>
</dl>

## Methods

<dl>
  <dt>layer</dt>
  <dd>TBD</dd>
</dl>

## Specifications

[XRView Interface](https://immersive-web.github.io/webxr/spec/latest/#xrview-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
