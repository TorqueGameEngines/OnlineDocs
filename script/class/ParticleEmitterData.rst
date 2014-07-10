ParticleEmitterData
===================

.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines particle emission properties such as ejection angle, period and velocity for a ParticleEmitter.

Example::

	datablock ParticleEmitterData( GrenadeExpDustEmitter )
	{
	   ejectionPeriodMS = 1;
	   periodVarianceMS = 0;
	   ejectionVelocity = 15;
	   velocityVariance = 0.0;
	   ejectionOffset = 0.0;
	   thetaMin = 85;
	   thetaMax = 85;
	   phiReferenceVel = 0;
	   phiVariance = 360;
	   overrideAdvance = false;
	   lifetimeMS = 200;
	   particles = "GrenadeExpDust";
	};


Methods
-------


.. cpp:function:: void ParticleEmitterData::reload()

	Reloads the ParticleData datablocks and other fields used by this emitter.

	Example::

		// Get the editors current particle emitter
		%emitter = PE_EmitterEditor.currEmitter
		
		// Change a field value
		%emitter.setFieldValue( %propertyField, %value );
		
		// Reload this emitter
		%emitter.reload();

Fields
------


.. cpp:member:: Point3F  ParticleEmitterData::alignDirection

	The direction aligned particles should face, only valid if alignParticles is true.

.. cpp:member:: bool  ParticleEmitterData::alignParticles

	If true, particles always face along the axis defined by alignDirection.

.. cpp:member:: float  ParticleEmitterData::ambientFactor

	Used to generate the final particle color by controlling interpolation between the particle color and the particle color multiplied by the ambient light color.

.. cpp:member:: ParticleBlendStyle ParticleEmitterData::blendStyle

	String value that controls how emitted particles blend with the scene.

.. cpp:member:: float  ParticleEmitterData::ejectionOffset

	Distance along ejection Z axis from which to eject particles.

.. cpp:member:: float  ParticleEmitterData::ejectionOffsetVariance

	Distance Padding along ejection Z axis from which to eject particles.

.. cpp:member:: int  ParticleEmitterData::ejectionPeriodMS

	Time (in milliseconds) between each particle ejection.

.. cpp:member:: float  ParticleEmitterData::ejectionVelocity

	Particle ejection velocity.

.. cpp:member:: bool  ParticleEmitterData::highResOnly

	This particle system should not use the mixed-resolution renderer. If your particle system has large amounts of overdraw, consider disabling this option.

.. cpp:member:: int  ParticleEmitterData::lifetimeMS

	Lifetime of emitted particles (in milliseconds).

.. cpp:member:: int  ParticleEmitterData::lifetimeVarianceMS

	Variance in particle lifetime from 0 - lifetimeMS.

.. cpp:member:: bool  ParticleEmitterData::orientOnVelocity

	If true, particles will be oriented to face in the direction they are moving.

.. cpp:member:: bool  ParticleEmitterData::orientParticles

	If true, Particles will always face the camera.

.. cpp:member:: bool  ParticleEmitterData::overrideAdvance

	If false, particles emitted in the same frame have their positions adjusted. If true, adjustment is skipped and particles will clump together.

.. cpp:member:: string  ParticleEmitterData::particles

	List of space or TAB delimited ParticleData datablock names. A random one of these datablocks is selected each time a particle is emitted.

.. cpp:member:: int  ParticleEmitterData::periodVarianceMS

	Variance in ejection period, from 1 - ejectionPeriodMS.

.. cpp:member:: float  ParticleEmitterData::phiReferenceVel

	Reference angle, from the vertical plane, to eject particles from.

.. cpp:member:: float  ParticleEmitterData::phiVariance

	Variance from the reference angle, from 0 - 360.

.. cpp:member:: bool  ParticleEmitterData::renderReflection

	Controls whether particles are rendered onto reflective surfaces like water.

.. cpp:member:: bool  ParticleEmitterData::reverseOrder

	If true, reverses the normal draw order of particles. Particles are normally drawn from newest to oldest, or in Z order (furthest first) if sortParticles is true. Setting this field to true will reverse that order: oldest first, or nearest first if sortParticles is true.

.. cpp:member:: float  ParticleEmitterData::softnessDistance

	For soft particles, the distance (in meters) where particles will be faded based on the difference in depth between the particle and the scene geometry.

.. cpp:member:: bool  ParticleEmitterData::sortParticles

	If true, particles are sorted furthest to nearest.

.. cpp:member:: string  ParticleEmitterData::textureName

	Optional texture to override ParticleData::textureName .

.. cpp:member:: float  ParticleEmitterData::thetaMax

	Maximum angle, from the horizontal plane, to eject particles from.

.. cpp:member:: float  ParticleEmitterData::thetaMin

	Minimum angle, from the horizontal plane, to eject from.

.. cpp:member:: bool  ParticleEmitterData::useEmitterColors

	If true, use emitter specified colors instead of datablock colors. Useful for ShapeBase dust and WheeledVehicle wheel particle emitters that use the current material to control particle color.

.. cpp:member:: bool  ParticleEmitterData::useEmitterSizes

	If true, use emitter specified sizes instead of datablock sizes. Useful for Debris particle emitters that control the particle size.

.. cpp:member:: float  ParticleEmitterData::velocityVariance

	Variance for ejection velocity, from 0 - ejectionVelocity.
