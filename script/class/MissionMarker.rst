MissionMarker
=============

This is a base class for all "marker" related objets. It is a 3D representation of a point in the level.

Inherit:
	:doc:`ShapeBase`

Description
-----------

The main use of a MissionMarker is to represent a point in 3D space with a mesh and basic ShapeBase information. If you simply need to mark a spot in your level, with no overhead from additional fields, this is a useful object.

Example::

	newMissionMarker()
	{
	   dataBlock = "WayPointMarker";
	   position = "295.699 -171.817 280.124";
	   rotation = "0 0 -1 13.8204";
	   scale = "1 1 1";
	   isRenderEnabled = "true";
	   canSaveDynamicFields = "1";
	   enabled = "1";
	};

