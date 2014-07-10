WayPoint
========

Special type of marker, distinguished by a name and team ID number.

Inherit:
	:doc:`MissionMarker`

Description
-----------

The original Torque engines were built from a multi-player game called Tribes. The Tribes series featured various team based game modes, such as capture the flag. The WayPoint class survived the conversion from game (Tribes) to game engine (Torque).

Essentially, this is a MissionMarker with the addition of two variables: markerName and team. Whenever a WayPoint is created, it is added to a unique global list called WayPointSet. You can iterate through this set, seeking out specific markers determined by their markerName and team ID. This avoids the overhead of constantly calling commandToClient and commandToServer to determine a WayPoint object's name, unique ID, etc.

Example::

	newWayPoint()
	{
	   team = "1";
	   dataBlock = "WayPointMarker";
	   position = "-0.0224786 1.53471 2.93219";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	   canSave = "1";
	   canSaveDynamicFields = "1";
	};

Fields
------

.. cpp:member:: caseString  WayPoint::markerName

	Unique name representing this waypoint.

.. cpp:member:: WayPointTeam  WayPoint::team

	Unique numerical ID assigned to this waypoint, or set of waypoints.
