# Glossary

**Note to reviewers:** Glossaries are not meant to provide full discussions of the concepts they define. They are intended to provide short, quick definitions for deciphering more complex content.

<dl>
  <dt>exclusive session</dt>
  <dd>An immersive presentation in which content is presented directly to the device.</dd>

  <dt>eye-level</dt>
  <dd>A room-scale frame of reference in which the coordinates' origin is the viewer's head.</dd>

  <dt>far depth</dt>
  <dd>The plane of the <a href="#viewing-frustum">viewing frustum</a> farthest form the eye.</dd>

  <dt>frame of reference</dt>
  <dd>The spatial point from which VR measurements are made. The WebXR spec supports <code>headModel</code>, <code>eyeLevel</code>, and <code>stage</code>.</dd>

  <dt>frustum</dt>
  <dd>See <a href="#viewing-frustum">viewing frustum</a>.</dd>

  <dt>head-model</dt>
  <dd>An orientation-only frame of reference in which the origin of the coordinate system is approximately the location of the viewer's head and does not change if the viewer moves. Use a head-model frame of reference when displaying images for which it is not necessary to change orientation such as, for example, 360 photos or videos.</dd>

  <dt>matrix</dt>
  <dd>TBD</dd>

  <dt>near depth</dt>
  <dd>The plane of the <a href="#viewing-frustum">viewing frustum</a> closest to the eye.</dd>

  <dt>non-exclusive session</dt>
  <dd>A presentation in which device tracking information is used to render content on a page.</dd>

  <dt>orientation-only tracking</dt>
  <dd>A type of tracking in which the device does not respond to head translation because the source material is intended to be viewed from a single vantage point. </dd>

  <dt>pose</dt>
  <dd>The position and orientation of a device in 3D space. A pose is always a matrix in the form of a Float32Array whose values are relative to the current coordinate system.</dd>

  <dt>pose matrix</dt>
  <dd>A transform that describes the position and orientation of the viewer's head that roughly correlates with the center point between the viewer's eyes.</dd>

  <dt>room scale</dt>
  <dd>See <a href="#stage">stage</a>.</dd>

  <dt>room-scale tracking</dt>
  <dd>A type of tracking in which the VR device can access details about the space in which it's being used. </dd>

  <dt id="stage">stage</dt>
  <dd>A room-scale frame of reference in which the coordinates' origin is implied to be the center of the room at floor level.</dd>
  <dd>A bounded, floor-level play space that a viewer can be expected to safely move within. Some AR/VR platforms refer to this as "room scale", or "standing space".</dd>

  <dt>standing space</dt>
  <dd>See <a href="#stage">stage</a>.</dd>

  <dt>transform</dt>
  <dd>An operation performed on a pose's coordinates to position or orient it. </dd>

  <dt id="viewing-frustum">viewing frustum</dt>
  <dd>The portion of a modeled 3D space that is visible to the eye. A frustum has the shape of a pyramid with the sliced-off top, where the narrow portion is closest to the eye. The top and the bottom of the pyramid are called the <em>near depth</em> and the <em>far depth</em>. The viewing frustum is sometimes called the field of view.</dd>

  <dt>view matrix</dt>
  <dd>A transform that describes the position and orientation of the viewer's eye.</dd>
</dl>
