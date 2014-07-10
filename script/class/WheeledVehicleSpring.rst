WheeledVehicleSpring
====================

Defines the properties of a WheeledVehicle spring.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Defines the properties of a WheeledVehicle spring.

Fields
------

.. cpp:member:: float  WheeledVehicleSpring::antiSwayForce

	Force applied to equalize extension of the spring on the opposite wheel. This force helps to keep the suspension balanced when opposite wheels are at different heights.

.. cpp:member:: float  WheeledVehicleSpring::damping

	Force applied to slow changes to the extension of this spring. Increasing this makes the suspension stiffer which can help stabilise bouncy vehicles.

.. cpp:member:: float  WheeledVehicleSpring::force

	Maximum spring force (when compressed to minimum length, 0). Increasing this will make the vehicle suspension ride higher (for a given vehicle mass), and also make the vehicle more bouncy when landing jumps.

.. cpp:member:: float  WheeledVehicleSpring::length

	Maximum spring length. ie. how far the wheel can extend from the root hub position. This should be set to the vertical (Z) distance the hub travels in the associated spring animation.
