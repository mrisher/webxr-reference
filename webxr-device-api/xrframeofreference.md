# XRFrameOfReference

The **`XRFrameOfReference`** interface provides information about the spatial point from which AR/VR measurements are made. An instance is passed to the \{\{jsxref("Promise")\}\} resolution returned by calling `xrSession.requestAnimationFrame()`.

## Properties

<dl>
  <dt>bounds</dt>
  <dd>Returns an instance of \{\{domxref("XRStageBounds")\}\}, which contains an array of \{\{domxref("XRStageBoundPoint")\}\} objects defining the border of the AR/XR stage.</dd>
  <dt>emulatedHeight</dt>
  <dd>TBD</dd>
</dl>

### Events

<dl>
  <dt>onboundschange</dt>
  <dd>Indicates that some value in the bounds array has changed.</dd>
</dl>

## Methods

None.

## Examples

The two examples below go together. The first shows how to get an `xrFrameOfReference` object. The second shows how to use it. Both examples leave out the complexity of drawing images to the AR/VR display.

## Getting an XRFrameOfReference Object

```javascript
function enterVRBtn_onClick() {
  vrDevice.requestSession(sessionOptions)
  .then(session => {
    let glContext = createWebGLContext({
      exclusive: true,
      compatibleXRDevice: session.device
    });

    // Set up rendering here. This could be implemented
    // in WebGL or some AR/VR framework.

    session.baseLayer = new XRWebGLLayer(session, glContext);
    session.requestFrameOfReference('eyeLevel')
    .then((xrFrameOfReference) => {
      // Do something with the frame of reference.
      })
    })
  });
}
```

### Using the XRFrameOfReference object

The example below shows how to use an `XRFrameOfReference` object to get an `xrDevicePose` object.

```javascript
// Full context of this snip is shown in the previous example
session.requestFrameOfReference('eyeLevel')
.then((xrFrameOfReference) => {
  let xrFrameOfRef = xrFrameOfReference;
  session.requestAnimationFrame(function onFrame(t, frame){
    frame.session.requestAnimationFrame(onFrame);
    glContext.bindFramebuffer(glContext.FRAMEBUFFER, session.baseLayer.framebuffer);
    glContext.clear(glContext.COLOR_BUFFER_BIT | glContext.DEPTH_BUFFER_BIT);
    let xrDevicePose = frame.getDevicePose(xrFrameOfRef);
    if (xrDevicePose) {
      for (let xrView of frame.views) {
        // Draw to the views.
      }
    }
  })
});
```

## Specifications

[XRFrameOfReference Interface](https://immersive-web.github.io/webxr/spec/latest/#xrframeofreference-interface)

## Browser Compatibility

| -- | -- | -- |
| Chrome 66 and later | VR use-cases only | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| Chrome 67 origin triaL | VR use-cases only | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
