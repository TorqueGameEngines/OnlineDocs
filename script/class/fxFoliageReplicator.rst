fxFoliageReplicator
===================

An emitter to replicate fxFoliageItem objects across an area.

Inherit:
	:doc:`SceneObject`

Description
-----------

An emitter to replicate fxFoliageItem objects across an area.


Fields
------


.. cpp:member:: int  fxFoliageReplicator::AllowedTerrainSlope

	Maximum surface angle allowed for foliage instances.

.. cpp:member:: bool  fxFoliageReplicator::AllowOnStatics

	Foliage will be placed on Static shapes when set.

.. cpp:member:: bool  fxFoliageReplicator::AllowOnTerrain

	Foliage will be placed on terrain when set.

.. cpp:member:: bool  fxFoliageReplicator::AllowOnWater

	Foliage will be placed on/under water when set.

.. cpp:member:: bool  fxFoliageReplicator::AllowWaterSurface

	Foliage will be placed on water when set. Requires AllowOnWater.

.. cpp:member:: float  fxFoliageReplicator::AlphaCutoff

	Minimum alpha value allowed on foliage instances.

.. cpp:member:: int  fxFoliageReplicator::CullResolution

	Minimum size of culling bins. Must be gt = 8 and lt = OuterRadius.

.. cpp:member:: float  fxFoliageReplicator::DebugBoxHeight

	Height multiplier for drawn culling bins.

.. cpp:member:: float  fxFoliageReplicator::FadeInRegion

	Region beyond ViewDistance where foliage fades in/out.

.. cpp:member:: float  fxFoliageReplicator::FadeOutRegion

	Region before ViewClosest where foliage fades in/out.

.. cpp:member:: bool  fxFoliageReplicator::FixAspectRatio

	Maintain aspect ratio of image if true. This option ignores MaxWidth.

.. cpp:member:: bool  fxFoliageReplicator::FixSizeToMax

	Use only MaxWidth and MaxHeight for billboard size. Ignores MinWidth and MinHeight.

.. cpp:member:: int  fxFoliageReplicator::FoliageCount

	Maximum foliage instance count.

.. cpp:member:: filename  fxFoliageReplicator::FoliageFile

	Image file for the foliage texture.

.. cpp:member:: int  fxFoliageReplicator::FoliageRetries

	Number of times to try placing a foliage instance before giving up.

.. cpp:member:: float  fxFoliageReplicator::GroundAlpha

	Alpha of the foliage at ground level. 0 = transparent, 1 = opaque.

.. cpp:member:: bool  fxFoliageReplicator::HideFoliage

	Foliage is hidden when set to true.

.. cpp:member:: int  fxFoliageReplicator::InnerRadiusX

	Placement area inner radius on the X axis.

.. cpp:member:: int  fxFoliageReplicator::InnerRadiusY

	Placement area inner radius on the Y axis.

.. cpp:member:: bool  fxFoliageReplicator::LightOn

	Foliage should be illuminated with changing lights when true.

.. cpp:member:: bool  fxFoliageReplicator::LightSync

	Foliage instances have the same lighting when set and LightOn is set.

.. cpp:member:: float  fxFoliageReplicator::lightTime

	Time before foliage illumination cycle repeats.

.. cpp:member:: float  fxFoliageReplicator::MaxHeight

	Maximum height of foliage billboards.

.. cpp:member:: float  fxFoliageReplicator::MaxLuminance

	Maximum luminance for foliage instances.

.. cpp:member:: float  fxFoliageReplicator::MaxSwayTime

	Maximum sway cycle time in seconds.

.. cpp:member:: float  fxFoliageReplicator::MaxWidth

	Maximum width of foliage billboards.

.. cpp:member:: float  fxFoliageReplicator::MinHeight

	Minimum height of foliage billboards.

.. cpp:member:: float  fxFoliageReplicator::MinLuminance

	Minimum luminance for foliage instances.

.. cpp:member:: float  fxFoliageReplicator::MinSwayTime

	Minumum sway cycle time in seconds.

.. cpp:member:: float  fxFoliageReplicator::MinWidth

	Minimum width of foliage billboards.

.. cpp:member:: float  fxFoliageReplicator::OffsetZ

	Offset billboards by this amount vertically.

.. cpp:member:: int  fxFoliageReplicator::OuterRadiusX

	Placement area outer radius on the X axis.

.. cpp:member:: int  fxFoliageReplicator::OuterRadiusY

	Placement area outer radius on the Y axis.

.. cpp:member:: int  fxFoliageReplicator::PlacementAreaHeight

	Height of the placement ring in world units.

.. cpp:member:: ColorF  fxFoliageReplicator::PlacementColour

	Color of the placement ring.

.. cpp:member:: bool  fxFoliageReplicator::RandomFlip

	Randomly flip billboards left-to-right.

.. cpp:member:: int  fxFoliageReplicator::seed

	Random seed for foliage placement.

.. cpp:member:: bool  fxFoliageReplicator::ShowPlacementArea

	Draw placement rings when set to true.

.. cpp:member:: float  fxFoliageReplicator::SwayMagFront

	Front-to-back sway magnitude.

.. cpp:member:: float  fxFoliageReplicator::SwayMagSide

	Left-to-right sway magnitude.

.. cpp:member:: bool  fxFoliageReplicator::SwayOn

	Foliage should sway randomly when true.

.. cpp:member:: bool  fxFoliageReplicator::SwaySync

	Foliage instances should sway together when true and SwayOn is enabled.

.. cpp:member:: bool  fxFoliageReplicator::UseCulling

	Use culling bins when enabled.

.. cpp:member:: bool  fxFoliageReplicator::UseDebugInfo

	Culling bins are drawn when set to true.

.. cpp:member:: bool  fxFoliageReplicator::useTrueBillboards

	Use camera facing billboards ( including the z axis ).

.. cpp:member:: float  fxFoliageReplicator::ViewClosest

	Minimum distance from camera where foliage appears.

.. cpp:member:: float  fxFoliageReplicator::ViewDistance

	Maximum distance from camera where foliage appears.
