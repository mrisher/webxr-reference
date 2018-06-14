# XRSessionEvent

The **`XRSessionEvent`** interface of the of the WebXR API is the event type passed to all of the <a href="xrsession">XRSession<a> events, specifically, `onblur`, `onfocus`, `onresetpose`, and `onend`.

## Constructor

<dl>
  <dt>XRSessionEvent()</dt>
  <dd>Constructs a new `XRSessionEvent`.</dd>
</dl>

## Properties

<dl>
  <dt>session</dt>
  <dd>Returns a reference to the `XRSession` object on which the event ocurred.</dd>
</dl>

## Methods

None.

## Specifications

[XRSessionEvent Interface](https://immersive-web.github.io/webxr/spec/latest/#xrsessionevent-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags. Requires Android O or later. |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
