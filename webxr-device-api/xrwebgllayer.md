# XRWebGLLayer

The **`XRWebGLLayer`** interface of the of the WebXR API is an <a href="xrlayer">XRLayer</a> subtype that allows WebGL to provide the bitmaps to be rendered to a device. Only one layer can be used at a time. It is set by passing an instance to <code><a href="xrsession">XRSession</a>.baseLayer</code> property.

## Properties

<dl>
  <dt>context</dt>
  <dd>Returns an instance of <a href="xrwebglrenderingcontext">XRWebGLRenderingContext</a> which will be either a <a href="https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext">WebGLRenderingContext</a> or a <a href="https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext">WebGL2RenderingContext</a>.</dd>

  <dt>antialias \{\{readonlyinline\}\}</dt>
  <dd>Indicates whether the current layer supports antialiasing which helps smooth an image by reducing its jagged edges.</dd>

  <dt>depth \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>stencil \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>alpha \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>multiview \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>framebuffer \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>framebufferWidth \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>

  <dt>framebufferHeight \{\{readonlyinline\}\}</dt>
  <dd>TBD</dd>
</dl>

## Methods

<dl>
  <dt>requestViewportScaling()</dt>
  <dd>Requests of resize of XRViewpoint by a supplied value that must between 0.0 and 1.0. Not all user agents will honor the scaling request. Consequently, you should query viewport values on each XR frame.</dd>
</dl>

## Examples

This example shows where in relation to session creation and starting the render loop that a layer should be set. The layer is set by setting `XRSession.baseLayer` to a new instance of `XRWebGLLayer`.

```javascript
// Do some Cottontail stuff.
let scene = new Scene();
scene.addNode(new CubeSea());

xrDevice.requestSession(sessionOptions)
.then(session => {
  // Use Cottontail's createWebGLContext() method.
  gl = createWebGLContext({
    // It needs an instance of XRDevice.
    compatibleXRDevice: session.device
  });
  // Use Cottontail's Renderer object.
  renderer = new Renderer(gl);
  scene.setRenderer(renderer);
  session.baseLayer = new XRWebGLLayer(session, gl);

  // Initialize the render loop.
})
```

## Specifications

[XRWebGLLayer Interface](https://immersive-web.github.io/webxr/spec/latest/#xrwebgllayer-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags. Requires Android O or later. |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
