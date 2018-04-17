# XRInputSource

The **`XRInputSource`** interface of the of the WebXR API returns information about the Web AR/VR control device being used. The control device is platform-specific and defines a primary action. A primary action is a trigger, touchpad, button, spoken command, or hand gesture that when performed produces <a href="selectstart">selectstart</a>, <a href="selectend">selectend</a>, and <a href="select">select</a> events.

## Properties

<dl>
  <dt>handedness</dt>
  <dd>One of <code>"left"</code>, <code>"right"</code>, or <code>""</code> (empty string).</dd>
  <dt>pointerOrigin</dt>
  <dd>One of <code>"head"</code>, <code>"hand"</code>, or <code>"screen"</code></dd>
</dl>

## Methods

None.

## Examples

The following example taken from Immersive Web's [input tracking sample](https://github.com/immersive-web/webxr-samples/blob/master/input-tracking.html) uses `XRSession.getInputSources()` to get an array of `XRInputSource` objects. It then uses the first available input source to render representations of the input device in VR at appropriate locations. In the actual example, this function is called from within the `requestAnimationFrame()` callback. This insures the virtual positions of input devices are kept in sync with their physical counterparts.

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
      if (inputSource.pointerOrigin == 'hand') {
        // Use pointerMatrix to render a pointer at an appropriate location.
      }
      // Render a cursor.
    }
  }
}
```

# Specifications

[XRFrameOfReference Interface](https://immersive-web.github.io/webxr/#xrinputsource-interface)

## Browser Compatibility

* Chrome 66 or later.
