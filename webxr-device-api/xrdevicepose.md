# XRDevicePose

The **`XRDevicePose`** of the WebXR Device API describes the position and orientation of an <a href="xrdevice">XRDevice</a> relative to the <a href="xrcoordinateSystem">XRCoordinateSystem</a> it was queried with. It also describes the view and projection matrices that should be used by the application to render a frame of an AR/VR scene.

## Properties

<dl>
  <dt>poseModelMatrix</dt>
  <dd>TBD</dd>
</dl>

## Methods

<dl>
  <dt>getViewMatrix()</dt>
  <dd>Takes an <a href="xrview">XRView</a> object and returns a matrix describing the view transform to be used when rendering the passed <a href="xrview">XRView</a>. The matrices represent the inverse of the model matrix of the associated viewpoint.</dd>
</dl>

## Examples

TBD

```
function onDrawFrame(timestamp, xrFrame) {
  // Do we have an active session?
  if (xrSession) {
    let pose = xrFrame.getDevicePose(xrFrameOfRef);
    gl.bindFramebuffer(xrSession.baseLayer.framebuffer);

    for (let view of xrFrame.views) {
      let viewport = xrSession.baseLayer.getViewport(view);
      gl.viewport(viewport.x, viewport.y, viewport.width, viewport.height);
      drawScene(view, pose);
    }

    // Request the next animation callback
    xrSession.requestAnimationFrame(onDrawFrame);
  } else {
    // No session available, so render a default mono view.
    gl.viewport(0, 0, glCanvas.width, glCanvas.height);
    drawScene();

    // Request the next window callback
    window.requestAnimationFrame(onDrawFrame);
  }
}

function drawScene(view, pose) {
  let viewMatrix = null;
  let projectionMatrix = null;
  if (view) {
    viewMatrix = pose.getViewMatrix(view);
    projectionMatrix = view.projectionMatrix;
  } else {
    viewMatrix = defaultViewMatrix;
    projectionMatrix = defaultProjectionMatrix;
  }
}
```

## Specifications

[XRDevicePose Interface](https://immersive-web.github.io/webxr/spec/latest/#xrdevicepose-interface)

## Browser Compatibility

* Chrome 66 or later
