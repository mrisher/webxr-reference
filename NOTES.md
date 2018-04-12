# Notes

## Things the MDN conversion script will need to do.

**Convert &lt;dt> element contents and anchor tags to kumascript link.**

Original
```
<dt>ondevicechange</dt>
<a href="xrsession.md">XRSession</a>
```

Converted
```
<dt>{{domxref('XR.ondevicechange')}}</dt>
{{domxref("XRSession")}}
```

**Convert links to other MDN pages.**

Original
```
<a href="https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext">WebGLRenderingContext<a>
```

Converted
```
{{domxref("WebGLRenderingContext")}}
```
## Concepts and Usage

<a href="webxr-device-api/index">This section</a> will eventually answer the following questions:

[x] How do I get a device (`XRDevice`), a session (`XRSession`), a context (`XRPresentationContext`) etc.?
[x] How is XR functionality advertised to the viewer?
[] What is a presentation loop and how do I implement it?
[] What happens to the device object during navigation?
[] What do I do differently to get AR (as opposed to VR)?

## Possible How-to Topics

* 360° and 3D video.
* Object and data visualizations.
* Artistic experiences.
