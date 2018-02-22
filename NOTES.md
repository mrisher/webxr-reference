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
