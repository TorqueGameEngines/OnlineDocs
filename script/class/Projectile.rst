Projectile
==========

class for properties of individual projectiles.

Inherit:
	:doc:`GameBase`

Description
-----------

Base projectile class. Uses the ProjectileData class for properties of individual projectiles.


Methods
-------


.. cpp:function:: void Projectile::presimulate(float seconds)

	Updates the projectile's positional and collision information. This function will first delete the projectile if it is a server object and is outside it's ProjectileData::lifetime . Also responsible for applying gravity, determining collisions, triggering explosions, emitting trail particles, and calculating bounces if necessary.

	:param seconds: Amount of time, in seconds since the simulation's start, to advance.

	Example::

		// Tell the projectile to process a simulation event, and provide the amount of time// that has passed since the simulation began.
		%seconds = 2.0;
		%projectile.presimulate(%seconds);

Fields
------


.. cpp:member:: Point3F  Projectile::initialPosition

	Starting position for the projectile.

.. cpp:member:: Point3F  Projectile::initialVelocity

	Starting velocity for the projectile.

.. cpp:member:: int  Projectile::sourceObject

	ID number of the object that fired the projectile.

.. cpp:member:: int  Projectile::sourceSlot

	The sourceObject's weapon slot that the projectile originates from.
