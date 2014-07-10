WaterPlane
==========

Represents a large body of water stretching to the horizon in all directions.

Inherit:
	:doc:`WaterObject`

Description
-----------

Represents a large body of water stretching to the horizon in all directions.

WaterPlane's position is defined only height, the z element of position, it is infinite in xy and depth. WaterPlane is designed to represent the ocean on an island scene and viewed from ground level; other uses may not be appropriate and a WaterBlock may be used.

Limitations:

Because WaterPlane cannot be projected exactly to the far-clip distance, other objects nearing this distance can have noticible artifacts as they clip through first the WaterPlane and then the far plane.

To avoid this large objects should be positioned such that they will not line up with the far-clip from vantage points the player is expected to be. In particular, your TerrainBlock should be completely contained by the far-clip distance.

Viewing WaterPlane from a high altitude with a tight far-clip distance will accentuate this limitation. WaterPlane is primarily designed to be viewed from ground level.


Fields
------


.. cpp:member:: float  WaterPlane::gridElementSize

	Duplicate of gridElementSize for backwards compatility.

.. cpp:member:: int  WaterPlane::gridSize

	Spacing between vertices in the WaterBlock mesh.
