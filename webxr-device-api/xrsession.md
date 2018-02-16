# XRSession

TBD

## Properties

<dl>
  <dt>device</dt>
  <dd>A reference to the <a href="xrdevice.md">XRDevice</a> object on which the current session was created.</dd>
  <dt>exclusive</dt>
  <dd>A boolean indicating whether the current session is exclusive or non-exclusive.</dd>
  <dt>outputContext</dt>
  <dd>A refernce to the <a href="xrpresentationcontest.md">XRPresentationContext</a> object passed in the constructor which contains the {{domxref("HTMLCanvasElement")}} on which AR/VR images will be drawn.</dd>
  <dt>depthNear</dt>
  <dd>The near plane of the viewing frustum (field of view).</dd>
  <dt>depthFar</dt>
  <dd>The far plane of the viewing frustum (field of view).</dd>
  <dt>baseLayer</dt>
  <dd>A reference to an <a href="XRLayer">XRLayer</a> object, which is a source of bitmap images for rendering to the <a href="xrdevice.md">XRDevice</a> and a description for how to render them.</dd>
</dl>

### Events

<dl>
  <dt>onblur</dt>
  <dd>Indicates that the presentation to the display is paused by the user agent, operating system, OR VR hardware.</dd>
  </dd>
  <dt>onfocus</dt>
  <dd>Indicates that the presentation to the display was resumed by the user agent, operating system, or AR/VR hardware.</dd>
  <dt>onresetpose</dt>
  <dd>Indicates that the pose presented to the display has been reset.</dd>
  <dt>onend</dt>
  <dd>Indicates that presentation to the AR/VR device has stopped.</dd>
</dl>

## Methods

<dl>
  <dt>requestFrameOfReference()</dt>
  <dd>Gets the geometric attributes of a specified frame of reference.</dd>
  <dt>requestAnimationFrame()</dt>
  <dd>Requests that the user agent call a specified callback function to update an animation before the next repaint.</dd>
  <dt>cancelAnimationFrame()</dt>
  <dd>Cancels an animation request previously scheduled through a call to <code>requestAnimationFrame()</code>.</dd>
  <dt>end()</dt>
  <dd>Returns an empty {{jsxref("Promise")}} that ends the presentation to the device</dd>
</dl>

## Specifications

https://immersive-web.github.io/webxr/spec/latest/#xrsession-interface

## Browser Compatibility

* Chrome 66 or later.
