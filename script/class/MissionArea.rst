MissionArea
===========

Level object which defines the boundaries of the level.

Inherit:
	:doc:`NetObject`

Description
-----------

This is a simple box with starting points, width, depth, and height. It does not have any default functionality. Instead, when objects hit the boundaries certain script callbacks will be made allowing you to control the reaction.

Example::

	newMissionArea(GlobalMissionArea)
	{
	     Area = "-152 -352 1008 864";
	     flightCeiling = "300";
	     flightCeilingRange = "20";
	     canSaveDynamicFields = "1";
	       enabled = "1";
	       TypeBool locked = "false";
	};

Methods
-------

.. cpp:function:: string MissionArea::getArea()

	Returns 4 fields: starting x, starting y, extents x, extents y.

.. cpp:function:: void MissionArea::postApply()

	Intended as a helper to developers and editor scripts. Force trigger an inspectPostApply. This will transmit material and other fields ( not including nodes ) to client objects.

.. cpp:function:: void MissionArea::setArea(int x, int y, int width, int height)

	Defines the size of the MissionArea param x Starting X coordinate position for MissionArea param y Starting Y coordinate position for MissionArea param width New width of the MissionArea param height New height of the MissionArea

Fields
------

.. cpp:member:: RectI  MissionArea::area

	Four corners (X1, X2, Y1, Y2) that makes up the level's boundaries.

.. cpp:member:: float  MissionArea::flightCeiling

	Represents the top of the mission area, used by FlyingVehicle .

.. cpp:member:: float  MissionArea::flightCeilingRange

	Distance from ceiling before FlyingVehicle thrust is cut off.
