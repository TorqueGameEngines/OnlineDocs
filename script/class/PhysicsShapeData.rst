PhysicsShapeData
================

Defines the properties of a PhysicsShape.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines the properties of a PhysicsShape.

Fields
------

.. cpp:member:: float  PhysicsShapeData::angularDamping

	Value that reduces an object's rotational velocity over time. Larger values will cause velocity to decay quicker.

.. cpp:member:: float  PhysicsShapeData::angularSleepThreshold

	Minimum rotational velocity before the shape can be put to sleep. This should be a positive value. Shapes put to sleep will not be simulated in order to save system resources.

.. cpp:member:: float  PhysicsShapeData::buoyancyDensity

	The density of the shape for calculating buoyant forces. The result of the calculated buoyancy is relative to the density of the WaterObject the PhysicsShape is within.

.. cpp:member:: PhysicsDebrisData PhysicsShapeData::Debris

	Name of a PhysicsDebrisData to spawn when this shape is destroyed (optional).

.. cpp:member:: PhysicsShapeData PhysicsShapeData::destroyedShape

	Name of a PhysicsShapeData to spawn when this shape is destroyed (optional).

.. cpp:member:: ExplosionData PhysicsShapeData::Explosion

	Name of an ExplosionData to spawn when this shape is destroyed (optional).

.. cpp:member:: float  PhysicsShapeData::friction

	Coefficient of kinetic friction to be applied to the shape. Kinetic friction reduces the velocity of a moving object while it is in contact with a surface. A higher coefficient will result in a larger velocity reduction. A shape's friction should be lower than it's staticFriction, but larger than 0.

.. cpp:member:: float  PhysicsShapeData::linearDamping

	Value that reduces an object's linear velocity over time. Larger values will cause velocity to decay quicker.

.. cpp:member:: float  PhysicsShapeData::linearSleepThreshold

	Minimum linear velocity before the shape can be put to sleep. This should be a positive value. Shapes put to sleep will not be simulated in order to save system resources.

.. cpp:member:: float  PhysicsShapeData::mass

	Value representing the mass of the shape. A shape's mass influences the magnitude of any force exerted on it. For example, a PhysicsShape with a large mass requires a much larger force to move than the same shape with a smaller mass.

.. cpp:member:: float  PhysicsShapeData::restitution

	Coeffecient of a bounce applied to the shape in response to a collision. Restitution is a ratio of a shape's velocity before and after a collision. A value of 0 will zero out a shape's post-collision velocity, making it stop on contact. Larger values will remove less velocity after a collision, making it 'bounce' with a greater force. Normal restitution values range between 0 and 1.0.

.. cpp:member:: filename  PhysicsShapeData::shapeName

	Path to the .DAE or .DTS file to use for this shape. Compatable with Live-Asset Reloading.

.. cpp:member:: PhysicsSimType PhysicsShapeData::simType

	Controls whether this shape is simulated on the server, client, or both physics simulations.

.. cpp:member:: float  PhysicsShapeData::staticFriction

	Coefficient of static friction to be applied to the shape. Static friction determines the force needed to start moving an at-rest object in contact with a surface. If the force applied onto shape cannot overcome the force of static friction, the shape will remain at rest. A larger coefficient will require a larger force to start motion. This value should be larger than zero and the physicsShape's friction.

.. cpp:member:: float  PhysicsShapeData::waterDampingScale

	Scale to apply to linear and angular dampening while underwater. Used with the waterViscosity of the
