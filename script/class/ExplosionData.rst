ExplosionData
=============

: particleEmitters, debris, lighting and camera shake effects.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines the attributes of an Explosion: particleEmitters, debris, lighting and camera shake effects.


Fields
------


.. cpp:member:: Point3F  ExplosionData::camShakeAmp

	Amplitude of camera shaking, defined in the "X Y Z" axes. Set any value to 0 to disable shaking in that axis.

.. cpp:member:: float  ExplosionData::camShakeDuration

	Duration (in seconds) to shake the camera.

.. cpp:member:: float  ExplosionData::camShakeFalloff

	Falloff value for the camera shake.

.. cpp:member:: Point3F  ExplosionData::camShakeFreq

	Frequency of camera shaking, defined in the "X Y Z" axes.

.. cpp:member:: float  ExplosionData::camShakeRadius

	Radial distance that a camera's position must be within relative to the center of the explosion to be shaken.

.. cpp:member:: DebrisData ExplosionData::Debris

	List of DebrisData objects to spawn with this explosion.

.. cpp:member:: int  ExplosionData::debrisNum

	Number of debris objects to create.

.. cpp:member:: int  ExplosionData::debrisNumVariance

	Variance in the number of debris objects to create (must be from 0 - debrisNum).

.. cpp:member:: float  ExplosionData::debrisPhiMax

	Maximum reference angle, from the vertical plane, to eject debris from.

.. cpp:member:: float  ExplosionData::debrisPhiMin

	Minimum reference angle, from the vertical plane, to eject debris from.

.. cpp:member:: float  ExplosionData::debrisThetaMax

	Maximum angle, from the horizontal plane, to eject debris from.

.. cpp:member:: float  ExplosionData::debrisThetaMin

	Minimum angle, from the horizontal plane, to eject debris from.

.. cpp:member:: float  ExplosionData::debrisVelocity

	Velocity to toss debris at.

.. cpp:member:: float  ExplosionData::debrisVelocityVariance

	Variance in the debris initial velocity (must be gt = 0).

.. cpp:member:: int  ExplosionData::delayMS

	Amount of time, in milliseconds, to delay the start of the explosion effect from the creation of the Explosion object.

.. cpp:member:: int  ExplosionData::delayVariance

	Variance, in milliseconds, of delayMS.

.. cpp:member:: ParticleEmitterData ExplosionData::emitter [4]

	List of additional ParticleEmitterData objects to spawn with this explosion.

.. cpp:member:: Point3F  ExplosionData::explosionScale

	"X Y Z" scale factor applied to the explosionShape model at the start of the explosion.

.. cpp:member:: filename  ExplosionData::explosionShape

	Optional DTS or DAE shape to place at the center of the explosion. The ambient animation of this model will be played automatically at the start of the explosion.

.. cpp:member:: bool  ExplosionData::faceViewer

	Controls whether the visual effects of the explosion always face the camera.

.. cpp:member:: int  ExplosionData::lifetimeMS

	Lifetime, in milliseconds, of the Explosion object.

.. cpp:member:: int  ExplosionData::lifetimeVariance

	Variance, in milliseconds, of the lifetimeMS of the Explosion object.

.. cpp:member:: float  ExplosionData::lightEndBrightness

	Final brightness of the PointLight created by this explosion.

.. cpp:member:: ColorF  ExplosionData::lightEndColor

	Final color of the PointLight created by this explosion.

.. cpp:member:: float  ExplosionData::lightEndRadius

	Final radius of the PointLight created by this explosion.

.. cpp:member:: float  ExplosionData::lightNormalOffset

	Distance (in the explosion normal direction) of the PointLight position from the explosion center.

.. cpp:member:: float  ExplosionData::lightStartBrightness

	Initial brightness of the PointLight created by this explosion. Brightness is linearly interpolated from lightStartBrightness to lightEndBrightness over the lifetime of the explosion.

.. cpp:member:: ColorF  ExplosionData::lightStartColor

	Initial color of the PointLight created by this explosion. Color is linearly interpolated from lightStartColor to lightEndColor over the lifetime of the explosion.

.. cpp:member:: float  ExplosionData::lightStartRadius

	Initial radius of the PointLight created by this explosion. Radius is linearly interpolated from lightStartRadius to lightEndRadius over the lifetime of the explosion.

.. cpp:member:: float  ExplosionData::offset

	Offset distance (in a random direction) of the center of the explosion from the Explosion object position. Most often used to create some variance in position for subExplosion effects.

.. cpp:member:: int  ExplosionData::particleDensity

	Density of the particle cloud created at the start of the explosion.

.. cpp:member:: ParticleEmitterData ExplosionData::ParticleEmitter

	Emitter used to generate a cloud of particles at the start of the explosion. Explosions can generate two different particle effects. The first is a single burst of particles at the start of the explosion emitted in a spherical cloud using particleEmitter. The second effect spawns the list of ParticleEmitters given by the emitter[] field. These emitters generate particles in the normal way throughout the lifetime of the explosion.

.. cpp:member:: float  ExplosionData::particleRadius

	Radial distance from the explosion center at which cloud particles are emitted.

.. cpp:member:: float  ExplosionData::playSpeed

	Time scale at which to play the explosionShape ambient sequence.

.. cpp:member:: bool  ExplosionData::shakeCamera

	Controls whether the camera shakes during this explosion.

.. cpp:member:: Point3F  ExplosionData::sizes [4]

	"X Y Z" size keyframes used to scale the explosionShape model. The explosionShape (if defined) will be scaled using the times/sizes keyframes over the lifetime of the explosion.

.. cpp:member:: SFXTrack ExplosionData::soundProfile

	Non-looping sound effect that will be played at the start of the explosion.

.. cpp:member:: ExplosionData ExplosionData::subExplosion [5]

	List of additional ExplosionData objects to create at the start of the explosion.

.. cpp:member:: float  ExplosionData::times [4]

	Time keyframes used to scale the explosionShape model. Values should be in increasing order from 0.0 - 1.0, and correspond to the life of the Explosion where 0 is the beginning and 1 is the end of the explosion lifetime.
