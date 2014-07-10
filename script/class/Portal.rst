Portal
======

An object that provides a "window" into a zone, allowing a viewer to see what's rendered in the zone.

Inherit:
	:doc:`Zone`

Description
-----------

A portal is an object that connects zones such that the content of one zone becomes visible in the other when looking through the portal.

Each portal is a full zone which is divided into two sides by the portal plane that intersects it. This intersection polygon is shown in red in the editor. Either of the sides of a portal can be connected to one or more zones.

A connection from a specific portal side to a zone is made in either of two ways:

#. By moving a Zone object to intersect with the portal at the respective side. While usually it makes sense for this overlap to be small, the connection is established correctly as long as the center of the Zone object that should connect is on the correct side of the portal plane.
#. By the respective side of the portal free of Zone objects that would connect to it. In this case, given that the other side is connected to one or more Zones, the portal will automatically connect itself to the outdoor "zone" which implicitly is present in any level.

From this, it follows that there are two types of portals:

Exterior Portals
	An exterior portal is one that is connected to one or more Zone objects on one side and to the outdoor zone at the other side. This kind of portal is most useful for covering transitions from outdoor spaces to indoor spaces.

Interior Portals
	An interior portal is one that is connected to one or more Zone objects on both sides. This kind of portal is most useful for covering transitions between indoor spaces

Strictly speaking, there is a third type of portal called an "invalid portal". This is a portal that is not connected to a Zone object on either side in which case the portal serves no use.

Portals in Torque are bidirectional meaning that they connect zones both ways and you can look through the portal's front side as well as through its back-side.

Like Zones, Portals can either be box-shaped or use custom convex polyhedral shapes.

Portals will usually be created in the editor but can, of course, also be created in script code as such:

Example::

	// Example declaration of a Portal.
	// This will create a box-shaped portal.
	newPortal( PortalToTestZone )
	{
	   position = "12.8467 -4.02246 14.8017";
	    rotation = "0 0 -1 97.5085";
	    scale = "1 0.25 1";
	    canSave = "1";
	    canSaveDynamicFields = "1";
	};

.. note::

	Keep in mind that zones and portals are more or less strictly a scene optimization mechanism meant to improve render times.

Methods
-------

.. cpp:function:: bool Portal::isExteriorPortal()

	Test whether the portal connects interior zones to the outdoor zone.

	:return: True if the portal is an exterior portal. 

.. cpp:function:: bool Portal::isInteriorPortal()

	Test whether the portal connects interior zones only.

	:return: True if the portal is an interior portal. 

Fields
------

.. cpp:member:: bool  Portal::backSidePassable

	Whether one can view through the back-side of the portal.

.. cpp:member:: bool  Portal::frontSidePassable

	Whether one can view through the front-side of the portal.
