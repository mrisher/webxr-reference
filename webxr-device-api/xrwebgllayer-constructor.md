# WebGLLayer()

The <strong><code>XRWebGLLayer</code></strong> constructor creates a new {{domxref("XRWebGLLayer")}} object which which is an <a href="xrlayer">XRLayer</a> subtype that allows WebGL to provide the bitmaps to be rendered to a device. Only one layer can be used at a time. It is set by passing an instance of `XRWebGLLayer` or one of its siblings to <code><a href="xrsession">XRSession</a>.baseLayer</code> property.

## Syntax

<pre class="syntaxbox">var <var>xrWebGLLayer</var> = new XRWebGLLayer(<var>session</var>, <var>context</var>[, <var>options</var>])</pre>

### Parameters

<dl>
  <dt><em>session</em></dt>
  <dd>TBD</dd>
 <dt><em>context</em></dt>
 <dd></dd>
 <dt><em>options</em> {{optional_inline}}</dt>
 <dd> Options are as follows:
 <ul>
  <li><code>antialias</code>: TBD The default is <code>true</code>.</li>
  <li><code>depth</code>: TBD The default is <code>true</code>.</li>
  <li><code>stencil</code>: TBD The default is <code>false</code>.</li>
  <li><code>alpha</code>: TBD The default is <code>true</code>.</li>
  <li><code>multiview</code>: TBD The default is <code>false</code>.</li>
  <li><code>framebufferScaleFactor</code>: Indicates the desired frame buffer scale. The default is 1.</li>
 </ul>
 </dd>
</dl>

## Specifications

[XRWebGLLayer Interface](https://immersive-web.github.io/webxr/spec/latest/#dom-xrwebgllayer-xrwebgllayer)

## Browser Compatibility

See [Browser Compatibility](compatibility).
