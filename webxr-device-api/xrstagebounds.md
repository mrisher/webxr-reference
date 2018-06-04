# XRStageBounds

The **`XRStageBounds`** interface of the WebXR API provides an array of <a href="xrstageboundspoint">XRStageBoundsPoint</a> objects containing coordinates defining the area in which the user can be expected to safely move within (the safe space).

## Properties

<dl>
  <dt>geometry</dt>
  <dd>An array of <a href="xrstageboundspoint">XRStageBoundsPoint</a> objects containing coordinates defining the area in which the user can be expected to safely move within.</dd>
</dl>

## Methods

None.

## Specifications

[XRStageBounds Interface](https://immersive-web.github.io/webxr/spec/latest/#xrstagebounds-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
