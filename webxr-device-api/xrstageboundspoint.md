# XRStageBoundsPoint

The **`XRStageBoundsPoint`** interface of the WebXR API provides the x and z values of a stage bound coordinate. Stage bounds are the area in which an AR/VR user can be expected to safely move within.

## Properties

<dl>
  <dt>x</dt>
  <dd>The position along the x axis of a stage bound point.</dd>
  <dt>z</dt>
  <dd>The position along the z axis of a stage bound point.</dd>
</dl>

## Methods

None.

## Specifications

[XRStageBoundsPoint Interface](https://immersive-web.github.io/webxr/spec/latest/#xrstageboundspoint)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
