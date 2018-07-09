# XRSession.getInputSources()

The `xrSession.getInputSources()` method of the WebXR Device API returns an array of <a href="xrinputsource">XRInputSource</a> objects representing tracked controllers.

## Syntax

```
var inputSources[] = xrSession.getInputSources()
```

### Parameters

None.

### Return value

An array of <a href="xrinputsource">XRInputSource</a> objects.

## Examples

The following example taken from Immersive Web's [input tracking sample](https://github.com/immersive-web/webxr-samples/blob/master/input-tracking.html) shows an `updateInputSource()` method, which uses `getInputSources()` to return an array of <a href="xrinputsource">XRInputSource</a> objects. The function then uses the first available input source to render representations of the input device in VR at appropriate locations. In the actual example, this function is called from within the `requestAnimationFrame()` callback. This insures the virtual positions of input devices are kept in sync with their physical counterparts.

```
function updateInputSources(xrSession, frame, frameOfRef) {
  // inputSources is an array of XRInputSource objects.
  let inputSources = xrSession.getInputSources();

  for (let inputSource of inputSources) {
    let inputPose = frame.getInputPose(inputSource, frameOfRef);

    if (!inputPose) {
      continue;
    }

    if (inputPose.gripMatrix) {
      // Use gripMatrix to render an image at an appropriate location.
    }

    if (inputPose.pointerMatrix) {
      if (inputSource.targetRayMode == 'pointing') {
        // Use pointerMatrix to render a pointer at an appropriate location.
      }
      // Render a cursor.
    }
  }
}
```

## Specifications

[`XRSession.requestFrameOfReference()`](https://immersive-web.github.io/webxr/spec/latest/#dom-xrsession-getinputsources]

## Browser Compatibility

See [Browser Compatibility](compatibility).
