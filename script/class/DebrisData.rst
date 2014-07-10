DebrisData
==========

Stores properties for an individual debris type.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Stores properties for an individual debris type.

DebrisData defines the base properties for a Debris object. Typically you'll want a Debris object to consist of a shape and possibly up to two particle emitters. The DebrisData datablock provides the definition for these items, along with physical properties and how a Debris object will react to other game objects, such as water and terrain.

Example::

	datablock DebrisData(GrenadeDebris)
	{
	   shapeFile = "art/shapes/weapons/ramrifle/debris.dts";
	   emitters[0] = GrenadeDebrisFireEmitter;
	   elasticity = 0.4;
	   friction = 0.25;
	   numBounces = 3;
	   bounceVariance = 1;
	   explodeOnMaxBounce = false;
	   staticOnMaxBounce = false;
	   snapOnMaxBounce = false;
	   minSpinSpeed = 200;
	   maxSpinSpeed = 600;
	   lifetime = 4;
	   lifetimeVariance = 1.5;
	   velocity = 15;
	   velocityVariance = 5;
	   fade = true;
	   useRadiusMass = true;
	   baseRadius = 0.3;
	   gravModifier = 1.0;
	   terminalVelocity = 20;
	   ignoreWater = false;
	};


Fields
------


.. cpp:member:: float  DebrisData::baseRadius

	Radius at which the standard elasticity and friction apply. Only used when useRaduisMass is true.

.. cpp:member:: int  DebrisData::bounceVariance

	Allowed variance in the value of numBounces. Must be less than numBounces.

.. cpp:member:: float  DebrisData::elasticity

	A floating-point value specifying how 'bouncy' this object is. Must be in the range of -10 to 10.

.. cpp:member:: ParticleEmitterData DebrisData::emitters [2]

	List of particle emitters to spawn along with this debris object. These are optional. You could have Debris made up of only a shape.

.. cpp:member:: bool  DebrisData::explodeOnMaxBounce

	If true, this debris object will explode after it has bounced max times. Be sure to provide an ExplosionData datablock for this to take effect.

.. cpp:member:: ExplosionData DebrisData::Explosion

	ExplosionData to spawn along with this debris object. This is optional as not all Debris explode.

.. cpp:member:: bool  DebrisData::fade

	If true, this debris object will fade out when destroyed. This fade occurs over the last second of the Debris' lifetime.

.. cpp:member:: float  DebrisData::friction

	A floating-point value specifying how much velocity is lost to impact and sliding friction. Must be in the range of -10 to 10.

.. cpp:member:: float  DebrisData::gravModifier

	How much gravity affects debris.

.. cpp:member:: bool  DebrisData::ignoreWater

	If true, this debris object will not collide with water, acting as if the water is not there.

.. cpp:member:: float  DebrisData::lifetime

	Amount of time until this debris object is destroyed. Must be in the range of 0 to 1000.

.. cpp:member:: float  DebrisData::lifetimeVariance

	Allowed variance in the value of lifetime. Must be less than lifetime.

.. cpp:member:: float  DebrisData::maxSpinSpeed

	Maximum speed that this debris object will rotate. Must be in the range of -10000 to 10000.

.. cpp:member:: float  DebrisData::minSpinSpeed

	Minimum speed that this debris object will rotate. Must be in the range of -10000 to 1000, and must be less than maxSpinSpeed.

.. cpp:member:: int  DebrisData::numBounces

	How many times to allow this debris object to bounce until it either explodes, becomes static or snaps (defined in explodeOnMaxBounce, staticOnMaxBounce, snapOnMaxBounce). Must be within the range of 0 to 10000.

.. cpp:member:: filename  DebrisData::shapeFile

	Object model to use for this debris object. This shape is optional. You could have Debris made up of only particles.

.. cpp:member:: bool  DebrisData::snapOnMaxBounce

	If true, this debris object will snap into a resting position on the last bounce.

.. cpp:member:: bool  DebrisData::staticOnMaxBounce

	If true, this debris object becomes static after it has bounced max times.

.. cpp:member:: float  DebrisData::terminalVelocity

	Max velocity magnitude.

.. cpp:member:: string  DebrisData::texture

	Texture imagemap to use for this debris object. Not used any more.

.. cpp:member:: bool  DebrisData::useRadiusMass

	Use mass calculations based on radius. Allows for the adjustment of elasticity and friction based on the Debris size.

.. cpp:member:: float  DebrisData::velocity

	Speed at which this debris object will move.

.. cpp:member:: float  DebrisData::velocityVariance

	Allowed variance in the value of velocity. Must be less than velocity.
