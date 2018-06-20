# XRInputSource

The **`XRInputSource`** interface of the of the WebXR API returns information about the pose (position) of the input device in 3D space.

## Properties

<dl>
  <dt>emulatedPosition \{\{readonlyinline\}\}</dt>
  <dd>A {{jsxref("Boolean")}} that returns <code>true</code> when the information provided by the other properties are estimations.</dd>
  <dt>gripMatrix \{\{readonlyinline\}\}</dt>
  <dd>Returns a matrix containing the coordinates where a virtual version of the input device should be rendered.</dd>
  <dt>pointerMatrix \{\{readonlyinline\}\}</dt>
  <dd>Returns a matrix containing the coordinates of the pointer's origin. Its value differs based on the type of input source that produces it. The device type is returned by <code>XRInputSource.pointerOrigin</code>.
  <table>
    <thead>
      <tr>
        <th><code>pointerOrigin</code> value</th>
        <th>Coordinates origin</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>'head'</code></td>
        <td>The pointer ray originates at the user's head.</td>
      </tr>
      <tr>
        <td><code>'hand'</code></td>
        <td>The pointer ray originates from a hand-held device.</td>
      </tr>
      <tr>
        <td><code>'screen'</code></td>
        <td>The input source was an interaction with the 2D canvas of a non-exclusive session, such as a mouse click or touch event.</td>
      </tr>
    </tbody>
  </table>
  </dd>
</dl>

## Methods

None.

## Examples



# Specifications

[XRFrameOfReference Interface](https://immersive-web.github.io/webxr/#xrinputpose-interface)

## Browser Compatibility

See [Browser Compatibility](compatibility).
