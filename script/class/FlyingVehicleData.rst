FlyingVehicleData
=================

Defines the properties of a FlyingVehicle.

Inherit:
	:doc:`VehicleData`

Description
-----------

Defines the properties of a FlyingVehicle.

Fields
------

.. cpp:member:: float  FlyingVehicleData::autoAngularForce

	Corrective torque applied to level out the vehicle when moving at less than maxAutoSpeed. The torque is inversely proportional to vehicle speed.

.. cpp:member:: float  FlyingVehicleData::autoInputDamping

	Scale factor applied to steering input if speed is less than maxAutoSpeed to.improve handling at very low speeds. Smaller values make steering less sensitive.

.. cpp:member:: float  FlyingVehicleData::autoLinearForce

	Corrective force applied to slow the vehicle when moving at less than maxAutoSpeed. The force is inversely proportional to vehicle speed.

.. cpp:member:: ParticleEmitterData FlyingVehicleData::backwardJetEmitter

	Emitter to generate particles for backward jet thrust. Backward jet thrust particles are emitted from model nodes JetNozzleX and JetNozzleY.

.. cpp:member:: float  FlyingVehicleData::createHoverHeight

	The vehicle's height off the ground when useCreateHeight is active. This can help avoid problems with spawning the vehicle.

.. cpp:member:: ParticleEmitterData FlyingVehicleData::downJetEmitter

	Emitter to generate particles for downward jet thrust. Downward jet thrust particles are emitted from model nodes JetNozzle2 and JetNozzle3.

.. cpp:member:: SFXProfile FlyingVehicleData::engineSound

	Looping engine sound.

.. cpp:member:: ParticleEmitterData FlyingVehicleData::forwardJetEmitter

	Emitter to generate particles for forward jet thrust. Forward jet thrust particles are emitted from model nodes JetNozzle0 and JetNozzle1.

.. cpp:member:: float  FlyingVehicleData::horizontalSurfaceForce

	Damping force in the opposite direction to sideways velocity. Provides "bite" into the wind for climbing/diving and turning).

.. cpp:member:: float  FlyingVehicleData::hoverHeight

	The vehicle's height off the ground when at rest.

.. cpp:member:: SFXProfile FlyingVehicleData::jetSound

	Looping sound to play while the vehicle is jetting.

.. cpp:member:: float  FlyingVehicleData::maneuveringForce

	Maximum X and Y (horizontal plane) maneuvering force. The actual force applied depends on the current thrust.

.. cpp:member:: float  FlyingVehicleData::maxAutoSpeed

	Maximum speed for automatic vehicle control assistance - vehicles travelling at speeds above this value do not get control assitance.

.. cpp:member:: float  FlyingVehicleData::minTrailSpeed

	Minimum speed at which to start generating contrail particles.

.. cpp:member:: float  FlyingVehicleData::rollForce

	Damping torque against rolling maneuvers (rotation about the y-axis), proportional to linear velocity. Acts to adjust roll to a stable position over time as the vehicle moves.

.. cpp:member:: float  FlyingVehicleData::rotationalDrag

	Rotational drag factor (slows vehicle rotation speed in all axes).

.. cpp:member:: float  FlyingVehicleData::steeringForce

	Maximum X and Z (sideways and vertical) steering force. The actual force applied depends on the current steering input.

.. cpp:member:: float  FlyingVehicleData::steeringRollForce

	Roll force induced by sideways steering input value (controls how much the vehicle rolls when turning).

.. cpp:member:: ParticleEmitterData FlyingVehicleData::trailEmitter

	Emitter to generate contrail particles from model nodes contrail0 - contrail3.

.. cpp:member:: float  FlyingVehicleData::verticalSurfaceForce

	Damping force in the opposite direction to vertical velocity. Controls side slip; lower numbers give more slide.

.. cpp:member:: float  FlyingVehicleData::vertThrustMultiple

	Multiplier applied to the jetForce (defined in VehicleData ) when thrusting vertically.
