# XRDevice

TBD

## Properties

<dl>
  <dt>external</dt>
  <dd>TBD</dd>
</dl>

## Methods

<dl>
  <dt>supportsSession(options)</dt>
  <dd>Returns an empty promise that resolves if the requested options are available from the device. Valid options are
  <ul>
    <li><code>exclusive</code>: Indicates whether an exclusive session is desired.</li>
    <li><code>outputContext</code>: A reference to an <a href="xrpresentationcontest.md">XRPresentationContext</a> object.</li>
  </ul>
  </dd>
  <dt>requestSession(options)</dt>
  <dd>Returns a {{jsxref("Promise")}} that resolves with an <a href="xrsession.md">XRSession</a> object meeting the requested options.</dd>
</dl>

## Examples

```javascript
const xrPC = window.XRPresentationContext;
const sessionsOptions = {
  exclusive: true,
  outputContext: xrPC
}

navigator.xr.requestDevice()
.then(device => {
  device.supportsSession(sessionOptions)
  .then( () => {
    device.requestSession(sessionOptions)
    .then(session => {
      //Do something with the session.
    })
  })
});
```
