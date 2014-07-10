Zone
====

An object that represents an interior space.

Inherit:
	:doc:`SceneObject`

Description
-----------

A zone is an invisible volume that encloses an interior space. All objects that have their world space axis-aligned bounding boxes (AABBs) intersect the zone's volume are assigned to the zone. This assignment happens automatically as objects are placed and transformed. Also, assignment is not exclusive meaning that an object can be assigned to many zones at the same time if it intersects all of them.

In itself, the volume of a zone is fully sealed off from the outside. This means that while viewing the scene from inside the volume, only objects assigned to the zone are rendered while when viewing the scene from outside the volume, objects exclusively only assigned the zone are not rendered.

Usually, you will want to connect zones to each other by means of portals. A portal overlapping with a zone

Example::

	// Example declaration of a Zone.  This creates a box-shaped zone.newZone( TestZone )
	{
	   position = "3.61793 -1.01945 14.7442";
	   rotation = "1 0 0 0";
	   scale = "10 10 10";
	};

Zone Groups
-----------

Normally, Zones will not connect to each other when they overlap. This means that if viewing the scene from one zone, the contents of the other zone will not be visible except when there is a portal connecting the zones. However, sometimes it is convenient to represent a single interior space through a combination of Zones so that when any of these zones is visible, all other zones that are part of the same interior space are visible. This is possible by employing "zone groups".

Methods
-------

.. cpp:function:: void Zone::dumpZoneState(bool updateFirst)

	Dump a list of all objects assigned to the zone to the console as well as a list of all connected zone spaces.

	:param updateFirst: Whether to update the contents of the zone before dumping. Since zoning states of objects are updated on demand, the zone contents can be outdated.

.. cpp:function:: int Zone::getZoneId()

	Get the unique numeric ID of the zone in its scene.

	:return: The ID of the zone. 

Fields
------

.. cpp:member:: ColorF  Zone::ambientLightColor

	Color of ambient lighting in this zone. Only used if useAmbientLightColor is true.

.. cpp:member:: string  Zone::edge

	For internal use only.

.. cpp:member:: string  Zone::plane

	For internal use only.

.. cpp:member:: string  Zone::point

	For internal use only.

.. cpp:member:: SFXAmbience Zone::soundAmbience

	Ambient sound environment for the space.

.. cpp:member:: bool  Zone::useAmbientLightColor

	Whether to use ambientLightColor for ambient lighting in this zone or the global ambient color.

.. cpp:member:: int  Zone::zoneGroup

	ID of group the zone is part of.
