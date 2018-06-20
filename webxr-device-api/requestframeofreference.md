# XRSession.requestFrameOfReference()

The `xrSession.requestFrameOfReference()` method of the WebXR Device API requests a frame of reference of a specific type and returns a \{\{jsxref("Promise")\}\} that resolves with an <a href="xrframeofreference.md">XRFrameOfReference</a> object.

## Syntax

```
var promise = xrSession.requestFrameOfReference(type, options)
```

### Parameters

<dl>
  <dt>type</dt>
  <dd>One of the following:
    <ul>
      <li><code>"head-model"</code>: The origin is approximately the location of the viewer's head and does not change if the viewer moves.</li>
      <li><code>"eye-level"</code>: The origin is the viewer's head and moves with the viewer.</li>
      <li><code>"stage"</code>: The origin is implied to be the center of the room at floor level and does not change if the viewer moves.</li>
    </ul>
  </dd>
  <dt>options \{\{optional_inline\}\}</dt>
  <dd>An object containing frame of reference creation options. Valid options are:
    <ul>
      <li><code>disableStageEmulation</code>:</li>
      <li><code>stageEmulationHeight</code>:</li>
    </ul>
  </dd>
</dl>

### Return value

A \{\{jsxref("Promise")\}\} that resolves with an <a href="xrframeofreference.md">XRFrameOfReference</a> object.

## Examples

The following example requests an eye-level frame of reference. If and only if the promise resolves it calls `requestAnimationFrame()` to start the render loop.

```javascript
let xrFrameOfRef = null;

xrDevice.requestSession(sessionOptions)
.then(session => {
  // Set up Cottontail and get an XRWebGLLayer.

  session.requestFrameOfReference('eye-level')
  .then((frameOfRef) => {
    xrFrameOfRef = frameOfRef;
    session.requestAnimationFrame(onFrame)
  })
})

function onFrame(time, frame) {
  // Continue the render loop.
}
```

## Specifications

[`XRSession.requestFrameOfReference()`](https://immersive-web.github.io/webxr/spec/latest/#dom-xrsession-requestframeofreference]

## Browser Compatibility

See [Browser Compatibility](compatibility).
