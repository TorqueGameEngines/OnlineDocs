RigidShapeData
==============

Physics object.

Inherit:
	:doc:`ShapeBaseData`

Description
-----------

Defines the physics properties for an individual RigidShapeData physics object.

Example::

	   datablock RigidShapeData( BouncingBoulder )
	   {
	      category = "RigidShape";
	
	      shapeFile = "~/data/shapes/boulder/boulder.dts";
	      emap = true;
	
	      // Rigid Bodymass = 500;
	      massCenter = "0 0 0";    // Center of mass for rigid bodymass
	      Box = "0 0 0";         // Size of box used for moment of inertia,
	                             // if zero it defaults to object bounding box
	      drag = 0.2;                // Drag coefficientbodyFriction = 0.2;
	      bodyRestitution = 0.1;
	      minImpactSpeed = 5;        // Impacts over this invoke the script callback
	      softImpactSpeed = 5;       // Play SoftImpact Sound
	      hardImpactSpeed = 15;      // Play HardImpact Sound
	      integration = 4;           // Physics integration: TickSec/Rate
	      collisionTol = 0.1;        // Collision distance 
	      tolerancecontactTol = 0.1; // Contact velocity toleranceminRollSpeed = 10;
	
	      maxDrag = 0.5;
	      minDrag = 0.01;
	
	      dustHeight = 10;
	
	      dragForce = 0.05;
	      vertFactor = 0.05;
	   };

Fields
------

.. cpp:member:: float  RigidShapeData::bodyFriction

	How much friction this object has. Lower values will cause the object to appear to be more slippery.

.. cpp:member:: float  RigidShapeData::bodyRestitution

	The percentage of kinetic energy kept by this object in a collision.

.. cpp:member:: float  RigidShapeData::cameraDecay

	Scalar rate at which the third person camera offset decays, per tick.

.. cpp:member:: float  RigidShapeData::cameraLag

	Scalar amount by which the third person camera lags the object, relative to the object's linear velocity.

.. cpp:member:: float  RigidShapeData::cameraOffset

	The vertical offset of the object's camera.

.. cpp:member:: bool  RigidShapeData::cameraRoll

	Specifies whether the camera's rotation matrix, and the render eye transform are multiplied during camera updates.

.. cpp:member:: float  RigidShapeData::collisionTol

	Collision distance tolerance.

.. cpp:member:: float  RigidShapeData::contactTol

	Contact velocity tolerance.

.. cpp:member:: float  RigidShapeData::dragForce

	Used to simulate the constant drag acting on the object.

.. cpp:member:: ParticleEmitterData RigidShapeData::dustEmitter

	Array of pointers to ParticleEmitterData datablocks which will be used to emit particles at object/terrain contact point.

.. cpp:member:: float  RigidShapeData::dustHeight

	Height of dust effects.

.. cpp:member:: ParticleEmitterData RigidShapeData::dustTrailEmitter

	Particle emitter used to create a dust trail for the moving object.

.. cpp:member:: SFXTrack RigidShapeData::exitingWater

	The AudioProfile will be used to produce sounds when emerging from water.

.. cpp:member:: float  RigidShapeData::exitSplashSoundVelocity

	The minimum velocity at which the exit splash sound will be played when emerging from water.

.. cpp:member:: SFXTrack RigidShapeData::hardImpactSound

	Sound to play when body impacts with at least hardImpactSpeed.

.. cpp:member:: float  RigidShapeData::hardImpactSpeed

	Minimum speed at which the object must be travelling for the hard impact sound to be played.

.. cpp:member:: float  RigidShapeData::hardSplashSoundVelocity

	The minimum velocity at which the hard splash sound will be played when impacting water.

.. cpp:member:: SFXTrack RigidShapeData::impactWaterEasy

	The AudioProfile will be used to produce sounds when a soft impact with water occurs.

.. cpp:member:: SFXTrack RigidShapeData::impactWaterHard

	The AudioProfile will be used to produce sounds when a hard impact with water occurs.

.. cpp:member:: SFXTrack RigidShapeData::impactWaterMedium

	The AudioProfile will be used to produce sounds when a medium impact with water occurs.

.. cpp:member:: int  RigidShapeData::integration

	Number of physics steps to process per tick.

.. cpp:member:: Point3F  RigidShapeData::massBox

	Size of inertial box.

.. cpp:member:: Point3F  RigidShapeData::massCenter

	Center of mass for rigid body.

.. cpp:member:: float  RigidShapeData::maxDrag

	Maximum drag available to this object.

.. cpp:member:: float  RigidShapeData::mediumSplashSoundVelocity

	The minimum velocity at which the medium splash sound will be played when impacting water.

.. cpp:member:: float  RigidShapeData::minDrag

	Minimum drag available to this object.

.. cpp:member:: float  RigidShapeData::minImpactSpeed

	Minimum collision speed to classify collision as impact (triggers onImpact on server object).

.. cpp:member:: float  RigidShapeData::minRollSpeed


.. cpp:member:: SFXTrack RigidShapeData::softImpactSound

	Sound to play when body impacts with at least softImageSpeed but less than hardImpactSpeed.

.. cpp:member:: float  RigidShapeData::softImpactSpeed

	Minimum speed at which this object must be travelling for the soft impact sound to be played.

.. cpp:member:: float  RigidShapeData::softSplashSoundVelocity

	The minimum velocity at which the soft splash sound will be played when impacting water.

.. cpp:member:: ParticleEmitterData RigidShapeData::splashEmitter [2]

	Array of pointers to ParticleEmitterData datablocks which will generate splash effects.

.. cpp:member:: float  RigidShapeData::splashFreqMod

	The simulated frequency modulation of a splash generated by this object. Multiplied along with speed and time elapsed when determining splash emition rate.

.. cpp:member:: float  RigidShapeData::splashVelEpsilon

	The threshold speed at which we consider the object's movement to have stopped when updating splash effects.

.. cpp:member:: float  RigidShapeData::triggerDustHeight

	Maximum height from the ground at which the object will generate dust.

.. cpp:member:: float  RigidShapeData::vertFactor

	The scalar applied to the vertical portion of the velocity drag acting on a object.

.. cpp:member:: SFXTrack RigidShapeData::waterWakeSound

	The AudioProfile will be used to produce sounds when a water wake is displayed.
