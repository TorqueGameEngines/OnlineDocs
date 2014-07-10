fxShapeReplicator
=================

An emitter for objects to replicate across an area.

Inherit:
	:doc:`SceneObject`

Description
-----------

An emitter for objects to replicate across an area.


Fields
------


.. cpp:member:: bool  fxShapeReplicator::AlignToTerrain

	Align shapes to surface normal when set.

.. cpp:member:: int  fxShapeReplicator::AllowedTerrainSlope

	Maximum surface angle allowed for shape instances.

.. cpp:member:: bool  fxShapeReplicator::AllowOnStatics

	Shapes will be placed on Static shapes when set.

.. cpp:member:: bool  fxShapeReplicator::AllowOnTerrain

	Shapes will be placed on terrain when set.

.. cpp:member:: bool  fxShapeReplicator::AllowOnWater

	Shapes will be placed on/under water when set.

.. cpp:member:: bool  fxShapeReplicator::AllowWaterSurface

	Shapes will be placed on water when set. Requires AllowOnWater.

.. cpp:member:: bool  fxShapeReplicator::HideReplications

	Replicated shapes are hidden when set to true.

.. cpp:member:: int  fxShapeReplicator::InnerRadiusX

	Placement area inner radius on the X axis.

.. cpp:member:: int  fxShapeReplicator::InnerRadiusY

	Placement area inner radius on the Y axis.

.. cpp:member:: bool  fxShapeReplicator::Interactions

	Allow physics interactions with shapes.

.. cpp:member:: int  fxShapeReplicator::OffsetZ

	Offset shapes by this amount vertically.

.. cpp:member:: int  fxShapeReplicator::OuterRadiusX

	Placement area outer radius on the X axis.

.. cpp:member:: int  fxShapeReplicator::OuterRadiusY

	Placement area outer radius on the Y axis.

.. cpp:member:: int  fxShapeReplicator::PlacementAreaHeight

	Height of the placement ring in world units.

.. cpp:member:: ColorF  fxShapeReplicator::PlacementColour

	Color of the placement ring.

.. cpp:member:: int  fxShapeReplicator::seed

	Random seed for shape placement.

.. cpp:member:: int  fxShapeReplicator::ShapeCount

	Maximum shape instance count.

.. cpp:member:: filename  fxShapeReplicator::shapeFile

	Filename of shape to replicate.

.. cpp:member:: int  fxShapeReplicator::ShapeRetries

	Number of times to try placing a shape instance before giving up.

.. cpp:member:: Point3F  fxShapeReplicator::ShapeRotateMax

	Maximum shape rotation angles.

.. cpp:member:: Point3F  fxShapeReplicator::ShapeRotateMin

	Minimum shape rotation angles.

.. cpp:member:: Point3F  fxShapeReplicator::ShapeScaleMax

	Maximum shape scale.

.. cpp:member:: Point3F  fxShapeReplicator::ShapeScaleMin

	Minimum shape scale.

.. cpp:member:: bool  fxShapeReplicator::ShowPlacementArea

	Draw placement rings when set to true.

.. cpp:member:: Point3F  fxShapeReplicator::TerrainAlignment

	Surface normals will be multiplied by these values when AlignToTerrain is enabled.
