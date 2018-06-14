# XRSession

The **`XRSession`** interface of the WebXR API provides the means to interact with an AR/VR device, providing features such as polling the device pose, getting information about the user's environment, and presenting imagery to the user.

## Properties

<dl>
  <dt>device</dt>
  <dd>A reference to the <a href="xrdevice.md">XRDevice</a> object on which the current session was created.</dd>

  <dt>exclusive</dt>
  <dd>A boolean indicating whether the current session is exclusive or non-exclusive.</dd>

  <dt>outputContext</dt>
  <dd>A refernce to the <a href="xrpresentationcontest.md">XRPresentationContext</a> object passed in the constructor which contains the \{\{domxref("HTMLCanvasElement")\}\} on which AR/VR images will be drawn.</dd>

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
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that the presentation to the display was paused by the user agent, operating system, or VR hardware.</dd>
  <dt>onfocus</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that the presentation to the display was resumed by the user agent, operating system, or AR/VR hardware.</dd>
  <dt>onresetpose</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that the pose presented to the display has been reset.</dd>
  <dt>onend</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that presentation to the AR/VR device has stopped.</dd>
  <dt>onselect</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that an input device has activated and release.</dd>
  <dt>onselectend</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that an input device has been released.</dd>
  <dt>onselectstart</dt>
  <dd>An <a href="xrsessionevent">XRSessionEvent</a> indicating that an input device has been activated.</dd>
</dl>

## Methods

<dl>
  <dt><a href="getinputsources">getinputsources()</a></dt>
  <dd>Returns an array of <a href="xrinputsource">XRInputSource</a> objects representing tracked controllers.</dd>

  <dt><a href="requestframeofreference">requestFrameOfReference()</a></dt>
  <dd>Gets the geometric attributes of a specified frame of reference. A type must be specified, one of `"headModel"`, `"eyeLevel"`, or `"stage"`.</dd>

  <dt>requestAnimationFrame()</dt>
  <dd>Tells the browser that you want to paint one frame of an animation at which time the browser will call the supplied callback function. The callback function must have the following interface.<br/><br/>
  <code>callbackFunction(time, frame)</code><br/><br/>
  Note that the <code>time</code> parameter is provided for <code>window.requestAnimationFrame()</code> and will always be <code>0</code>.
  </dd>

  <dt>requestHitTest()</dt>
  <dd>Returns a promise that resolves with an array of <code>XRHitResult</code> objects if a ray cast into a scene intersects a surface. This method takes three arguments that define the ray cast: <code>origin</code>, <code>direction</code>, and <code>frameOfReference</code>. The <code>origin</code>, and <code>direction</code> arguments are both 3D vectors that will be normalized to a length of 1. The <code>frameOfReference</code> argument is the session's frame of reference.

  <dt>cancelAnimationFrame()</dt>
  <dd>Cancels an animation request previously scheduled through a call to <code>requestAnimationFrame()</code>.</dd>

  <dt>end()</dt>
  <dd>Returns an empty \{\{jsxref("Promise")\}\} that ends the presentation to the device</dd>
</dl>

## Examples

### Creating a Non-exclusive Session

The following demonstrates using the API with a non-exclusive session. A non-exclusive session is one in which device tracking information is used to render content on a page.

```javascript
const xrPC = someCanvas.getContext('xrpresent');
// sessionOptions.exclusive may be left out since it defaults
// to false. It's shown here for clarity.
const sessionOptions = {
  exclusive: false,
  outputContext: xrPC
}

navigator.xr.requestDevice()
.then(device => {
  device.requestSession(sessionOptions)
  .then(session => {
    //Do something with the session.
  })
});
```

### Creating an Exclusive session

The process for creating an exclusive session is a little more complex because entering an exclusive session requires a user gesture. In this example, a button for entering AR/VR is initially hidden. A call to `supportsSession()` determines whether exclusive sessions are supported and makes an "Enter VR" button visible if they are.

```javascript
const xrPC = someCanvas.getContext('xrpresent');
const sessionsOptions = {
  exclusive: true,
  outputContext: xrPC
}
let vrDevice;

const vrButton = document.querySelector("#enterVR");
vrButton.addEventListener('click', enterVR);

navigator.xr.requestDevice()
.then(device => {
  vrDevice = device;
  device.supportsSession(sessionOptions)
  .then(() => {
    vrButton.style.display = "block";
  })
  .catch(err => {
    console.error("This browser/device combination does not support exclusive sessions.", err);
  })
})

function enterVR() {
  vrDevice.requestSession(sessionOptions)
  .then(session => {
    //Do something with the session.
  });
}
```

## Specifications

[XRSession Interface](https://immersive-web.github.io/webxr/spec/latest/#xrsession-interface)

## Browser Compatibility

| -- | -- | -- |
| AR hit test support | Chrome Canary for the foreseeable future. | Enable the #webxr and #webxr-hit-test flags under chrome://flags. Requires Android O or later. |
| VR use cases | Chrome 66 and later | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| VR use cases | Chrome 67 origin trial | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |
