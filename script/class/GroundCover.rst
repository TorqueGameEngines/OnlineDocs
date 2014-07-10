GroundCover
===========

Covers the ground in a field of objects (IE: Grass, Flowers, etc).

Inherit:
	:doc:`SceneObject`

Description
-----------

Covers the ground in a field of objects (IE: Grass, Flowers, etc).


Fields
------


.. cpp:member:: RectF  GroundCover::billboardUVs [8]

	Subset material UV coordinates for this cover billboard.

.. cpp:member:: float  GroundCover::clumpExponent [8]

	An exponent used to bias between the minimum and maximum clump counts for a particular clump.

.. cpp:member:: float  GroundCover::clumpRadius [8]

	The maximum clump radius.

.. cpp:member:: float  GroundCover::dissolveRadius

	This is less than or equal to radius and defines when fading of cover elements begins.

.. cpp:member:: int  GroundCover::gridSize

	The number of cells per axis in the grid.

.. cpp:member:: bool  GroundCover::invertLayer [8]

	Indicates that the terrain material index given in 'layer' is an exclusion mask.

.. cpp:member:: string  GroundCover::layer [8]

	Terrain material name to limit coverage to, or blank to not limit.

.. cpp:member:: bool  GroundCover::lockFrustum

	Debug parameter for locking the culling frustum which will freeze the cover generation.

.. cpp:member:: string  GroundCover::Material

	Material used by all GroundCover segments.

.. cpp:member:: float  GroundCover::maxBillboardTiltAngle

	The maximum amout of degrees the billboard will tilt down to match the camera.

.. cpp:member:: int  GroundCover::maxClumpCount [8]

	The maximum amount of elements in a clump.

.. cpp:member:: int  GroundCover::maxElements

	The maximum amount of cover elements to include in the grid at any one time.

.. cpp:member:: float  GroundCover::maxElevation [8]

	The maximum world space elevation for placement.

.. cpp:member:: float  GroundCover::maxSlope [8]

	The maximum slope angle in degrees for placement.

.. cpp:member:: int  GroundCover::minClumpCount [8]

	The minimum amount of elements in a clump.

.. cpp:member:: float  GroundCover::minElevation [8]

	The minimum world space elevation for placement.

.. cpp:member:: bool  GroundCover::noBillboards

	Debug parameter for turning off billboard rendering.

.. cpp:member:: bool  GroundCover::noShapes

	Debug parameter for turning off shape rendering.

.. cpp:member:: float  GroundCover::probability [8]

	The probability of one cover type verses another (relative to all cover types).

.. cpp:member:: float  GroundCover::radius

	Outer generation radius from the current camera position.

.. cpp:member:: float  GroundCover::reflectScale

	Scales the various culling radii when rendering a reflection. Typically for water.

.. cpp:member:: bool  GroundCover::renderCells

	Debug parameter for displaying the grid cells.

.. cpp:member:: int  GroundCover::seed

	This RNG seed is saved and sent to clients for generating the same cover.

.. cpp:member:: float  GroundCover::shapeCullRadius

	This is the distance at which DTS elements are completely culled out.

.. cpp:member:: filename  GroundCover::shapeFilename [8]

	The cover shape filename. [Optional].

.. cpp:member:: bool  GroundCover::shapesCastShadows

	Whether DTS elements should cast shadows or not.

.. cpp:member:: float  GroundCover::sizeExponent [8]

	An exponent used to bias between the minimum and maximum random sizes.

.. cpp:member:: float  GroundCover::sizeMax [8]

	The maximum random size of this cover type.

.. cpp:member:: float  GroundCover::sizeMin [8]

	The minimum random size for each cover type.

.. cpp:member:: Point2F  GroundCover::windDirection

	The direction of the wind.

.. cpp:member:: float  GroundCover::windGustFrequency

	Controls how often the wind gust peaks per second.

.. cpp:member:: float  GroundCover::windGustLength

	The length in meters between peaks in the wind gust.

.. cpp:member:: float  GroundCover::windGustStrength

	The maximum distance in meters that the peak wind gust will displace an element.

.. cpp:member:: float  GroundCover::windScale [8]

	The wind effect scale.

.. cpp:member:: float  GroundCover::windTurbulenceFrequency

	Controls the overall rapidity of the wind turbulence.

.. cpp:member:: float  GroundCover::windTurbulenceStrength

	The maximum distance in meters that the turbulence can displace a ground cover element.

.. cpp:member:: float  GroundCover::zOffset

	Offset along the Z axis to render the ground cover.
