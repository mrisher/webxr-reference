# WebXR API

The WebXR Device API lets you create augmented reality and virtual reality web sites by providing access to input and output capabilities of AR/VR hardware. As of early 2018, examples include [Google’s Daydream](https://vr.google.com/daydream/), the [Oculus Rift](https://www3.oculus.com/rift/), the [Samsung Gear VR](http://www.samsung.com/global/galaxy/gear-vr/), the [HTC Vive](https://www.htcvive.com/), and [Windows Mixed Reality headsets](https://developer.microsoft.com/en-us/windows/mixed-reality).

## Concepts and Usage

Intro - TBD

### What's the X in XR mean?

There are many "&#95;&#95;&#95; reality" buzzwords flying around: _virtual reality_, _augmented reality_, _mixed reality_, etc.. It can be hard to keep track, even though there are many similarities between them. This API aims to provide foundational elements with which to do all of the above. Since the designers of the API don't want to be limited to just one facet of AR, VR, or anything in between, the "X" in "XR" is not part of an acronym, but an algebraic variable of sorts to refer to whatever a web developer needs or wants it to be.

### Exclusive versus Non-Exclusive Sessions

There are two types of sessions: exclusive sessions and non-exclusive sessions.

**Exclusive session:** An immersive presentation in which content is presented directly to the device. Entering an exclusive session requires a user gesture.

**Non-exclusive session:** A non-immersive presentation in which device tracking information is used to render content on a page. This is sometimes referred to as "magic window" mode. It enables the viewer to look around a scene by moving the device.

### Frame of Reference Types

A frame of reference describes the space or stage in which AR/VR content will be created. Each frame of reference implies two facts that you need to be aware of when drawing content.

* Where is the origin of the coordinate system?
* What happens to the origin when the viewer moves?

A frame of reference can be one of three types.

* `"headModel"`&mdash;The origin is approximately the location of the viewer's head and does not change if the viewer moves.
* `"eyeLevel"`&mdash;The origin is the viewer's head and moves with the viewer.
* `"stage"`&mdash;The origin is implied to be the center of the room at floor level and does not change if the viewer moves.

The `"eyeLevel"` and `"stage"` frames of reference are referred to as 'room scale' frames of reference.

### Poses

Although the term pose sounds as though it might be referring to the viewer, it does not. A pose actually refers to a device, specifically it's position and orientation in 3D space. A pose is represented by a matrix in the form of a `Float32Array` whose values are relative to the current coordinate system.

There are two types of poses in the WebXR Device API.

**Device pose**&mdash;The pose of the viewer, retrieved by calling `XRPresentationFrame.getDevicePose()`.
**Input pose**&mdash;The pose of the input device, retrieved by calling `XRPresentationFrame.getInputPose()`

### Matrices

Some WebXR objects return data in the form of matrices. WebXR matrices are always 4 by 4 and returned as 16 element `Float32Arrays` in column major order. They may be passed directly to WebGL's `uniformMatrix4fv()` method, used to create an equivalent `DOMMatrix`, or used with a variety of third-party math libraries. Values in WebXR matrices are always given in meters.

## Using the API

* [Lifetime of an AR/VR Web Application](lifetime)
* [Interacting with Input Devices](devices)
* [Requesting Device Permission](permissions)

## WebVR Device Interfaces

### Device Enumeration

<dl>
  <dt><a href="xr">XR</a></dt>
  <dd>Provides the means to query for attached AR/VR devices and receive events when device availability changes. A requested device is accessed through a returned `XRDevice` object.</dd>
  <dt><a href="xrdevice">XRDevice</a></dt>
  <dd>Represents a single AR/VR hardware device and provides methods for obtaining an `XRSession` object</dd>
</dl>

### Sessions

<dl>
  <dt><a href="xrsession">XRSession</a></dt>
  <dd>Provides the means to interact with an AR/VR device, providing features such as polling the device pose, getting information about the user's environment, and presenting imagery to the user.</dd>
  <dt><a href="xrsessionevent">XRSessionEvent</a></dt>
  <dd>The event type passed to all of the `XRSession` events, specifically, `onblur`, `onfocus`, `onresetpose`, and `onend`.</dd>
</dl>

### Frame Loop

<dl>
  <dt><a href="xrpresentationframe">XRPresentationFrame</a></dt>
  <dd>Provides all of the values needed to render a single frame of an AR/VR scene to the display represented by the `XRDevice` interface.</dd>
</dl>

### Coordinate Systems

<dl>
  <dt><a href="xrcoordinatesystem">XRCoordinateSystem</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrcoordinatesystemevent">XRCoordinateSystemEvent</a></dt>
  <dd>TBD</dd>
  <dt><a href="xrframeofreference">XRFrameOfReference</a></dt>
  <dd>Provides information about the spatial point from which AR/VR measurements are made.</dd>
  <dt><a href="xrstagebounds">XRStageBounds</a></dt>
  <dd>Provides an array of <a href="xrstageboundspoint">XRStageBoundsPoint</a> objects containing coordinates defining the area in which the user can be expected to safely move within (the safe space).</dd>
  <dt><a href="xrstageboundspoint">XRStageBoundsPoint</a></dt>
  <dd>Provides the y and z values of a stage bound coordinate. Stage bounds are the area in which an AR/VR user can be expected to safely move within.</dd>
</dl>

### Views

<dl>
  <dt><a href="xrview">XRView</a></dt>
  <dd>Describes a single view into an AR/VR scene. Each view corresponds to a display or portion of a display used by a device to present imagery to the user.</dd>
  <dt><a href="xrviewport">XRViewport</a></dt>
  <dd>Describes a viewport, or rectangular region, of a graphics surface.</dd>
</dl>

### Poses

<dl>
  <dt><a href="xrdevicepose">XRDevicePose</a></dt>
  <dd>Describes the position and orientation of an <a href="xrdevice">XRDevice</a> relative to the <a href="xrcoordinateSystem">XRCoordinateSystem</a> it was queried with. It also describes the view and projection matrices that should be used by the application to render a frame of an AR/VR scene.</dd>
</dl>

### Input

<dl>
  <dt><a href="xrinputsource">XRInputSource</a></dt>
  <dd>Returns information about the Web AR/VR control device being used. The control device is platform-specific and defines a primary action. A primary action is a trigger, touchpad, button, spoken command, or hand gesture that when performed produces selectstart, selectend, and select events.</dd>
  <dt><a href="xrinputpose">XRInputPose</a></dt>
  <dd>Returns information about the pose (position) of the input device in 3D space.</dd>
</dl>

### Layers

<dl>
  <dt><a href="xrlayer">XRLayer</a></dt>
  <dd>Defines a source of bitmap images and a description of how the image is to be rendered in the device. Do not use this interface directly. Rather use one of its subtypes. As of the first version of the [WebXR Device API](https://immersive-web.github.io/webxr/) only one subtype, `XRWebGLLayer` is supported.</dd>
  <dt><a href="xrwebgllayer">XRWebGLLayer</a></dt>
  <dd>An XRLayer subtype that allows WebGL to provide the bitmaps to be rendered to a device.</dd>
</dl>

### Canvas Rendering Context

<dl>
  <dt><a href="xr">XRPresentationContext</a></dt>
  <dd>A wrapper object for the \{\{domxref("HTMLCanvasElement")\}\} object on which AR or VR content will be drawn. To retrieve an instance of this object, call `getContext()` on a canvas object with the value `'xrpresent'`.</dd>
</dl>

### Partial Interfaces

<dl>
  <dt><a href="partial_navigator">navigator.xr</a></dt>
  <dd>Returns a new XR object.</dd>
  <dt><a href="partial_webglcontextattributes">WebGLRenderingContex.setCompatibleXRDevice()</a></dt>
  <dd>Sets an <a href="xrdevice">XRDevice</a> after a presentation context has been created.</dd>
</dl>

## Examples


## Specifications

[Latest](https://immersive-web.github.io/webxr/spec/latest/)

## Browser Compatibility

| -- | -- | -- |
| Chrome 66 and later | VR use-cases only | Enable the chrome://flags/#webxr flag. (The URL must be entered manually.) |
| Chrome 67 origin triaL | VR use-cases only | Enable the chrome://flags/#webxr flag *and* sign up for the origin trial ([explainer](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md), [sign-up form](http://bit.ly/OriginTrialSignup)). |

## See Also

[Glossary of AR/VR Terms](../glossary.md)
