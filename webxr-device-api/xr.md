# XR

TBD

## Properties

None.

### Event Handlers

<dl>
  <dt>ondevicechange</dt>
  <dd>TBD</dd>
</dl>

## Examples

The following example finds the XR interface on navigator and prints
information about it to the console.

```javascript
navigator.xr.requestDevice()
  .then(xrDevice => {
    // Get information about the available device.
    console.log("Is the device external? " + device.external;);
  })
  .catch(error => {
    console.error("Unable to find an XR device. " + err);
  })
```
