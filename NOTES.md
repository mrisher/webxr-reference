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

## Possible How-to Topics

* 360° and 3D video.
* Object and data visualizations.
* Artistic experiences.
