MissionMarkerData
=================

A very basic class containing information used by MissionMarker objects for rendering.

Inherit:
	:doc:`ShapeBaseData`

Description
-----------

MissionMarkerData, is an extremely barebones class derived from ShapeBaseData. It is solely used by MissionMarker classes (such as SpawnSphere), so that you can see the object while editing a level.

Example::

	datablock MissionMarkerData(SpawnSphereMarker)
	{
	   category = "Misc";
	   shapeFile = "core/art/shapes/octahedron.dts";
	};

