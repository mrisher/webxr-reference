# XRLayer

The **`XRLayer`** interface of the of the WebXR API defines a source of bitmap images and a description of how the image is to be rendered in the device. Do not use this interface directly. Rather use one of its subtypes. As of the first version of the [WebXR Device API](https://immersive-web.github.io/webxr/) only one subtype, <a href="xrwebgllayer">XRWebGLLayer</a> is supported. Only one layer can be used at a time. It is set by passing an instance to <code><a href="xrsession">XRSession</a>.baseLayer</code> property.

## Properties

None.

## Methods

None.

## Examples

See its child class, <a href="xrwebgllayer">XRWebGLLayer</a> for an example of using an `XRLayer` subclass.

# Specifications

[XRFrameOfReference Interface](https://immersive-web.github.io/webxr/spec/latest/#xrlayer-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
