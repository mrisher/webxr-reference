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

## Specifications

https://immersive-web.github.io/webxr/spec/latest/#xrframeofreference-interface

## Browser Compatibility

* Chrome 66 or later.
