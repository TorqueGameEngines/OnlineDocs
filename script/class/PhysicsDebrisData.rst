PhysicsDebrisData
=================

Defines the properties of a PhysicsDebris object.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines the properties of a PhysicsDebris object.


Fields
------

.. cpp:member:: float  PhysicsDebrisData::angularDamping

	Value that reduces an object's rotational velocity over time. Larger values will cause velocity to decay quicker.

.. cpp:member:: float  PhysicsDebrisData::angularSleepThreshold

	Minimum rotational velocity before the shape can be put to sleep. This should be a positive value. Shapes put to sleep will not be simulated in order to save system resources.

.. cpp:member:: float  PhysicsDebrisData::buoyancyDensity

	The density of this shape for purposes of calculating buoyant forces. The result of the calculated buoyancy is relative to the density of the WaterObject the PhysicsDebris is within.

.. cpp:member:: bool  PhysicsDebrisData::castShadows

	Determines if the shape's shadow should be cast onto the environment.

.. cpp:member:: float  PhysicsDebrisData::friction

	Coefficient of kinetic friction to be applied to the shape. Kinetic friction reduces the velocity of a moving object while it is in contact with a surface. A larger coefficient will result in a larger reduction in velocity. A shape's friction should be smaller than it's staticFriction, but greater than 0.

.. cpp:member:: float  PhysicsDebrisData::lifetime

	Base time, in seconds, that debris persists after time of creation.

.. cpp:member:: float  PhysicsDebrisData::lifetimeVariance

	Range of variation randomly applied to lifetime when debris is created. Represents the maximum amount of seconds that will be added or subtracted to a shape's base lifetime. A value of 0 will apply the same lifetime to each shape created.

.. cpp:member:: float  PhysicsDebrisData::linearDamping

	Value that reduces an object's linear velocity over time. Larger values will cause velocity to decay quicker.

.. cpp:member:: float  PhysicsDebrisData::linearSleepThreshold

	Minimum linear velocity before the shape can be put to sleep. This should be a positive value. Shapes put to sleep will not be simulated in order to save system resources.

.. cpp:member:: float  PhysicsDebrisData::mass

	Value representing the mass of the shape. A shape's mass influences the magnitude of any force applied to it.

.. cpp:member:: void  PhysicsDebrisData::preload

	Loads some information to have readily available at simulation time. Forces generation of shaders, materials, and other data used by the PhysicsDebris object. This function should be used while a level is loading in order to shorten the amount of time to create a PhysicsDebris in game.

.. cpp:member:: float  PhysicsDebrisData::restitution

	Bounce coeffecient applied to the shape in response to a collision. Restitution is a ratio of a shape's velocity before and after a collision. A value of 0 will zero out a shape's post-collision velocity, making it stop on contact. Larger values will remove less velocity after a collision, making it 'bounce' with greater force. Normal restitution values range between 0 and 1.0.

.. cpp:member:: filename  PhysicsDebrisData::shapeFile

	Path to the .DAE or .DTS file to use for this shape. Compatable with Live-Asset Reloading.

.. cpp:member:: float  PhysicsDebrisData::staticFriction

	Coefficient of static friction to be applied to the shape. Static friction determines the force needed to start moving an at-rest object in contact with a surface. If the force applied onto shape cannot overcome the force of static friction, the shape will remain at rest. A higher coefficient will require a larger force to start motion. This value should be both greater than 0 and the PhysicsDebrisData::friction .

.. cpp:member:: float  PhysicsDebrisData::waterDampingScale

	Scale to apply to linear and angular dampening while underwater.
