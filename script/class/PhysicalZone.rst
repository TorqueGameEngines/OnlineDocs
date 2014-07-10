PhysicalZone
============

Physical Zones are areas that modify the player's gravity and/or velocity and/or applied force.

Inherit:
	:doc:`SceneObject`

Description
-----------

The datablock properties determine how the physics, velocity and applied forces affect a player who enters this zone.

Example::

	newPhysicalZone(Team1JumpPad) {
	velocityMod = "1";gravityMod = "0";
	appliedForce = "0 0 20000";
	polyhedron = "0.0000000 0.0000000 0.0000000 1.0000000 0.0000000 0.0000000 0.0000000 -1.0000000 0.0000000 0.0000000 0.0000000 1.0000000";
	position = "273.559 -166.371 249.856";
	rotation = "0 0 1 13.0216";
	scale = "8 4.95 28.31";
	isRenderEnabled = "true";
	canSaveDynamicFields = "1";
	enabled = "1";
	};

Methods
-------

.. cpp:function:: void PhysicalZone::activate()

	Activate the physical zone's effects.

	Example::

		// Activate effects for a specific physical zone.
		%thisPhysicalZone.activate();

.. cpp:function:: void PhysicalZone::deactivate()

	Deactivate the physical zone's effects.

	Example::

		// Deactivate effects for a specific physical zone.
		%thisPhysicalZone.deactivate();

Fields
------

.. cpp:member:: Point3F  PhysicalZone::appliedForce

	Three-element floating point value representing forces in three axes to apply to objects entering PhysicalZone .

.. cpp:member:: float  PhysicalZone::gravityMod

	Gravity in PhysicalZone . Multiplies against standard gravity.

.. cpp:member:: floatList  PhysicalZone::polyhedron

	The polyhedron type is really a quadrilateral and consists of a cornerpoint followed by three vectors representing the edges extending from the corner.

.. cpp:member:: bool  PhysicalZone::renderZones  [static]

	If true, a box will render around the location of all PhysicalZones.

.. cpp:member:: float  PhysicalZone::velocityMod

	Multiply velocity of objects entering zone by this value every tick.
