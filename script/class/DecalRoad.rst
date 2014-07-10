DecalRoad
=========

A strip shaped decal defined by spine nodes which clips against Terrain objects.

Inherit:
	:doc:`SceneObject`

Description
-----------

A strip shaped decal defined by spine nodes which clips against Terrain objects.

DecalRoad is for representing a road or path ( or other inventive things ) across a TerrainBlock. It renders as a decal and is therefore only for features that do not need geometric depth.

The Material assigned to DecalRoad should tile vertically.


Methods
-------


.. cpp:function:: void DecalRoad::postApply()

	Intended as a helper to developers and editor scripts. Force trigger an inspectPostApply. This will transmit the material and other fields ( not including nodes ) to client objects.

.. cpp:function:: void DecalRoad::regenerate()

	Intended as a helper to developers and editor scripts. Force DecalRoad to update it's spline and reclip geometry.

Fields
------


.. cpp:member:: float  DecalRoad::breakAngle

	Angle in degrees - DecalRoad will subdivided the spline if its curve is greater than this threshold.

.. cpp:member:: bool  DecalRoad::discardAll  [static]

	For use by the Decal Editor.

.. cpp:member:: bool  DecalRoad::EditorOpen  [static]

	For use by the Decal Editor.

.. cpp:member:: string  DecalRoad::Material

	Material used for rendering.

.. cpp:member:: string  DecalRoad::Node

	Do not modify, for internal use.

.. cpp:member:: int  DecalRoad::renderPriority

	DecalRoad(s) are rendered in descending renderPriority order.

.. cpp:member:: bool  DecalRoad::showBatches  [static]

	For use by the Decal Editor.

.. cpp:member:: bool  DecalRoad::showRoad  [static]

	For use by the Decal Editor.

.. cpp:member:: bool  DecalRoad::showSpline  [static]

	For use by the Decal Editor.

.. cpp:member:: float  DecalRoad::textureLength

	The length in meters of textures mapped to the DecalRoad .

.. cpp:member:: int  DecalRoad::updateDelay  [static]

	For use by the Decal Editor.

.. cpp:member:: bool  DecalRoad::wireframe  [static]

	For use by the Decal Editor.
