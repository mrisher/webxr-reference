# Interacting with Input Devices

The WebXR Device API adopts a "point and click" approach to user input. With this approach every input source has a defined _pointer ray_ to indicate where an input device is pointing and events to indicate when something was selected. Your app draws the pointer ray and shows where it's pointed. When the user clicks the input device, events are fired&mdash;select, selectStart, and selectEnd, specifically. Your app determines what was clicked and responds appropriately.

Note: The demos that the sample code is drawn from rely on WebGL. To avoid turning this into a WebGL tutorial, it will use [Cottontail](https://github.com/immersive-web/webxr-samples/tree/master/js/cottontail), a simple WebGL framework used in the [samples from the Immersive Web Community Group](https://github.com/immersive-web/webxr-samples). This is also not a tutorial on Cottontail, so it may gloss over things for the benefit of focusing on WebXR.

## Tracking Input Devices

As stated, this API relies on a "point and click" approach to user input. For a user to click on something, your app has to know that the user is pointing at it.

This section explains how to track where the user is pointing. If you want more context or to step through working code, see the [Input Tracking sample](https://github.com/immersive-web/webxr-samples/blob/master/input-tracking.html) from the Immersive Web Community Group.

The process you're about to see should be done for every frame. In practice that means it should be part of the callback for `requestAnimationFrame()`.

The basic process is this.

On each presentation frame, iterate the input devices. For each input device:
1. Get its pose (position and orientation).
2. Update its representation on screen. This means updating both the virtual representation of the input device and the vector of the ray.

The `XRSession.getInputSources()` method returns an array `XRInputSource` objects, one for each of the available input devices. Iterate those devices.

```JavaScript
let inputSources = xrSession.getInputSources();
for (let xrInputSource of inputSources) {
  // Update the position of the input devices.
}
```

Next, get each device's input pose. If the call to `XRFrameOfReference.getInputPose()` doesn't return a pose, then move on to the next device.

```JavaScript
let inputSources = xrSession.getInputSources();
for (let xrInputSource of inputSources) {
  let inputPose = xrFrameOfRef.getInputPose(inputSource, xrFrameOfRef);
  if (!inputPose) {
    continue;
  }
  // Update the position of the input devices.
}
```
Finally use the pose's `gripMatrix` and `pointerMatrix` properties to render the device and it's ray at the current locations.

```JavaScript
let inputSources = xrSession.getInputSources();
for (let xrInputSource of inputSources) {
  let inputPose = xrFrameOfRef.getInputPose(inputSource, xrFrameOfRef);
  if (!inputPose) {
    continue;
  }
  if (inputPose.gripMatrix) {
    // Render a virtual version of the input device
    //   at the correct position and orientation.
  }
  if (inputPose.pointerMatrix) {
    // Draw a ray from the gripMatrix to the pointerMatrix.
  }
}
```

## Adding Select Events

When the user clicks a device, events on the `XRSession` object tell you that something was selected. This means that event handlers should be added as soon as the `XRSession` object is available. The promise returned by `requestSession()` is a good place to do this. The example adds all three event listeners, though you can use any or all as you see fit.

```JavaScript
xrDevice.requestSession(sessionOptions)
.then(xrSession => {
  xrSession.addEventListener('selectstart', onSelectStart);
  xrSession.addEventListener('selectend', onSelectEnd);
  xrSession.addEventListener('select', onSelect);
  // Create a graphics layer and initialize the render loop.
});
```

## What was Clicked?

Determining what was clicked comes down to two basic operations: getting the pose of the input device then determining what the pointer ray is intersecting. Everything else in the code example supports these two basic operations. If you want more context or to step through working code, see the [Input Selection sample](https://immersive-web.github.io/webxr-samples/input-selection.html) from the Immersive Web Community Group.

Start by getting the input pose. If the call to `getInputPose()` returns null, then move on.

```JavaScript
function onSelect(ev) {
  let inputPose = ev.frame.getInputPose(ev.inputSource, xrFrameOfRef);
  if (!inputPose) {
    return;
  }
  // Determine what was clicked.
}
```

Use the pose's `pointerMatrix` property to determine if anything was clicked. The code below does this by comparing the clicked object to the available objects. It's taken from the [Cottontail](https://github.com/immersive-web/webxr-samples/tree/master/js/cottontail) framework, which is used here to simplify the WebGL part of creating an immersive experience.

```JavaScript
function onSelect(ev) {
  let inputPose = ev.frame.getInputPose(ev.inputSource, xrFrameOfRef);
  if (!inputPose) {
    return;
  }
  if (inputPose.pointerMatrix) {
    let hitResult = scene.hitTest(inputPose.pointerMatrix)
    if (hitResult) {
      // Check to see if the hit result was one of our boxes.
      for (let box of boxes) {
        if (hitResult.node == box.node) {
          // Change the box color to something random.
          let uniforms = box.renderPrimitive.uniforms;
          uniforms.baseColorFactor.value = [Math.random(), Math.random(), Math.random(), 1.0];
        }
      }
    }
  }
}
```

## See Also

[Glossary](../glossary)
[Lifetime of an AR/VR Web Application](lifetime)
