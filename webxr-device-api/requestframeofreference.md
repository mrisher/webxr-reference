# XRSession.requestAnimationFrame()

The `xrSession.requestAnimationFrame()` method of the WebXR Device API requests a frame of reference of a specific type and returns a \{\{jsxref("Promise")\}\} that resolves with an <a href="xrframeofreference.md">XRFrameOfReference</a> object.

## Syntax

```
var promise = xrSession.requestAnimationFrame(type, options)
```

### Parameters

<dl>
  <dt>type</dt>
  <dd>One of the following:
    <ul>
      <li><code>"headModel"</code>: The device estimates the position of the headset based on the assumptions that the viewer is sitting in one place only moving the head and neck and has a head and neck of roughly average human proportions. Some VR systems refer to head model and neck model. In practice this means movement is mostly rotation, but with some small amount of translation to aid in comfort.</li>
      <li><code>"eyeLevel"</code>:</li>
      <li><code>"stage"</code>:</li>
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

## Specifications

[`XRSession.requestFrameOfReference()`](https://immersive-web.github.io/webxr/spec/latest/#dom-xrsession-requestframeofreference]

## Browser Compatibility

* Chrome 66 or later.
