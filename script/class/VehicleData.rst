VehicleData
===========

Base properties shared by all Vehicles (FlyingVehicle, HoverVehicle, WheeledVehicle).

Inherit:
	:doc:`ShapeBaseData`

Description
-----------

This datablock defines properties shared by all Vehicle types, but should not be instantiated directly. Instead, set the desired properties in the FlyingVehicleData, HoverVehicleData or WheeledVehicleData datablock.

Damage
------

The VehicleData class extends the basic energy/damage functionality provided by ShapeBaseData to include damage from collisions, as well as particle emitters activated automatically when damage levels reach user specified thresholds.

The example below shows how to setup a Vehicle to:

Example::

	// damage from collisionscollDamageMultiplier = 0.05;
	collDamageThresholdVel = 15;
	
	// damage levelsdamageLevelTolerance[0] = 0.5;
	damageEmitter[0] = GraySmokeEmitter;     // emitter used when damage is >= 50%
	damageLevelTolerance[1] = 0.85;
	damageEmitter[1] = BlackSmokeEmitter;    // emitter used when damage is >= 85%
	damageEmitter[2] = DamageBubbleEmitter;  // emitter used instead of damageEmitter[0:1]
	// when offset point is underwater
	// emit offsets (used for all active damage level emitters)
	damageEmitterOffset[0] = "0.5 3 1";
	damageEmitterOffset[1] = "-0.5 3 1";
	numDmgEmitterAreas = 2;

Methods
-------

.. cpp:function:: void VehicleData::onEnterLiquid(Vehicle obj, float coverage, string type)

	Called when the vehicle enters liquid.

	:param obj: the Vehicle object
	:param coverage: percentage of the vehicle's bounding box covered by the liquid
	:param type: type of liquid the vehicle has entered

.. cpp:function:: void VehicleData::onLeaveLiquid(Vehicle obj, string type)

	Called when the vehicle leaves liquid.

	:param obj: the Vehicle object
	:param type: type of liquid the vehicle has left

Fields
------

.. cpp:member:: float  VehicleData::bodyFriction

	Collision friction coefficient. How well this object will slide against objects it collides with.

.. cpp:member:: float  VehicleData::bodyRestitution

	Collision 'bounciness'. Normally in the range 0 (not bouncy at all) to 1 (100% bounciness).

.. cpp:member:: float  VehicleData::cameraDecay

	How quickly the camera moves back towards the vehicle when stopped.

.. cpp:member:: float  VehicleData::cameraLag

	How much the camera lags behind the vehicle depending on vehicle speed. Increasing this value will make the camera fall further behind the vehicle as it accelerates away.

.. cpp:member:: float  VehicleData::cameraOffset

	Vertical (Z axis) height of the camera above the vehicle.

.. cpp:member:: bool  VehicleData::cameraRoll

	If true, the camera will roll with the vehicle. If false, the camera will always have the positive Z axis as up.

.. cpp:member:: float  VehicleData::collDamageMultiplier

	Damage to this vehicle after a collision (multiplied by collision velocity). Currently unused.

.. cpp:member:: float  VehicleData::collDamageThresholdVel

	Minimum collision velocity to cause damage to this vehicle. Currently unused.

.. cpp:member:: float  VehicleData::collisionTol

	Minimum distance between objects for them to be considered as colliding.

.. cpp:member:: float  VehicleData::contactTol

	Maximum relative velocity between objects for collisions to be resolved as contacts. Velocities greater than this are handled as collisions.

.. cpp:member:: ParticleEmitterData VehicleData::damageEmitter [3]

	Array of particle emitters used to generate damage (dust, smoke etc) effects. Currently, the first two emitters (indices 0 and 1) are used when the damage level exceeds the associated damageLevelTolerance. The 3rd emitter is used when the emitter point is underwater.

.. cpp:member:: Point3F  VehicleData::damageEmitterOffset [2]

	Object space "x y z" offsets used to emit particles for the active damageEmitter.

	Example::

		// damage levelsdamageLevelTolerance[0] = 0.5;
		damageEmitter[0] = SmokeEmitter;
		// emit offsets (used for all active damage level emitters)
		damageEmitterOffset[0] = "0.5 3 1";
		damageEmitterOffset[1] = "-0.5 3 1";
		numDmgEmitterAreas = 2;

.. cpp:member:: float  VehicleData::damageLevelTolerance [2]

	Damage levels (as a percentage of maxDamage) above which to begin emitting particles from the associated damageEmitter. Levels should be in order of increasing damage.

.. cpp:member:: ParticleEmitterData VehicleData::dustEmitter

	Dust particle emitter.

.. cpp:member:: float  VehicleData::dustHeight

	Height above ground at which to emit particles from the dustEmitter.

.. cpp:member:: SFXProfile VehicleData::exitingWater

	Sound to play when exiting the water.

.. cpp:member:: float  VehicleData::exitSplashSoundVelocity

	Minimum velocity when leaving the water for the exitingWater sound to play.

.. cpp:member:: SFXProfile VehicleData::hardImpactSound

	Sound to play on a 'hard' impact. This sound is played if the impact speed gt = hardImpactSpeed.

.. cpp:member:: float  VehicleData::hardImpactSpeed

	Minimum collision speed for the hardImpactSound to be played.

.. cpp:member:: float  VehicleData::hardSplashSoundVelocity

	Minimum velocity when entering the water for the imapactWaterHard sound to play.

.. cpp:member:: SFXProfile VehicleData::impactWaterEasy

	Sound to play when entering the water with speed gt = softSplashSoundVelocity and lt mediumSplashSoundVelocity.

.. cpp:member:: SFXProfile VehicleData::impactWaterHard

	Sound to play when entering the water with speed gt = hardSplashSoundVelocity.

.. cpp:member:: SFXProfile VehicleData::impactWaterMedium

	Sound to play when entering the water with speed gt = mediumSplashSoundVelocity and lt hardSplashSoundVelocity.

.. cpp:member:: int  VehicleData::integration

	Number of integration steps per tick. Increase this to improve simulation stability (also increases simulation processing time).

.. cpp:member:: float  VehicleData::jetEnergyDrain

	Energy amount to drain for each tick the vehicle is jetting. Once the vehicle's energy level reaches 0, it will no longer be able to jet.

.. cpp:member:: float  VehicleData::jetForce

	Additional force applied to the vehicle when it is jetting. For WheeledVehicles, the force is applied in the forward direction. For FlyingVehicles, the force is applied in the thrust direction.

.. cpp:member:: Point3F  VehicleData::massBox

	Define the box used to estimate the vehicle's moment of inertia. Currently only used by WheeledVehicle ; other vehicle types use a unit sphere to compute inertia.

.. cpp:member:: Point3F  VehicleData::massCenter

	Defines the vehicle's center of mass (offset from the origin of the model).

.. cpp:member:: float  VehicleData::maxDrag

	Maximum drag coefficient. Currently unused.

.. cpp:member:: float  VehicleData::maxSteeringAngle

	Maximum yaw (horizontal) and pitch (vertical) steering angle in radians.

.. cpp:member:: float  VehicleData::mediumSplashSoundVelocity

	Minimum velocity when entering the water for the imapactWaterMedium sound to play.

.. cpp:member:: float  VehicleData::minDrag

	Minimum drag coefficient. Currently only used by FlyingVehicle .

.. cpp:member:: float  VehicleData::minImpactSpeed

	Minimum collision speed for the onImpact callback to be invoked.

.. cpp:member:: float  VehicleData::minJetEnergy

	Minimum vehicle energy level to begin jetting.

.. cpp:member:: float  VehicleData::minRollSpeed

	Unused.

.. cpp:member:: float  VehicleData::numDmgEmitterAreas

	Number of damageEmitterOffset values to use for each damageEmitter.

.. cpp:member:: bool  VehicleData::powerSteering

	If true, steering does not auto-centre while the vehicle is being steered by its driver.

.. cpp:member:: SFXProfile VehicleData::softImpactSound

	Sound to play on a 'soft' impact. This sound is played if the impact speed is lt hardImpactSpeed and gt = softImpactSpeed.

.. cpp:member:: float  VehicleData::softImpactSpeed

	Minimum collision speed for the softImpactSound to be played.

.. cpp:member:: float  VehicleData::softSplashSoundVelocity

	Minimum velocity when entering the water for the imapactWaterEasy sound to play.

.. cpp:member:: ParticleEmitterData VehicleData::splashEmitter [2]

	Array of particle emitters used to generate splash effects.

.. cpp:member:: float  VehicleData::splashFreqMod

	Number of splash particles to generate based on vehicle speed. This value is multiplied by the current speed to determine how many particles to generate each frame.

.. cpp:member:: float  VehicleData::splashVelEpsilon

	Minimum speed when moving through water to generate splash particles.

.. cpp:member:: float  VehicleData::steeringReturn

	Rate at which the vehicle's steering returns to forwards when it is moving.

.. cpp:member:: float  VehicleData::steeringReturnSpeedScale

	Amount of effect the vehicle's speed has on its rate of steering return.

.. cpp:member:: float  VehicleData::triggerDustHeight

	Maximum height above surface to emit dust particles. If the vehicle is less than triggerDustHeight above a static surface with a material that has 'showDust' set to true, the vehicle will emit particles from the dustEmitter.

.. cpp:member:: SFXProfile VehicleData::waterWakeSound

	Looping sound to play while moving through the water.
