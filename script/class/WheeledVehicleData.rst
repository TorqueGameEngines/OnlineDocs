WheeledVehicleData
==================

Defines the properties of a WheeledVehicle.

Inherit:
	:doc:`VehicleData`

Description
-----------

Defines the properties of a WheeledVehicle.

Fields
------

.. cpp:member:: float  WheeledVehicleData::brakeTorque

	Torque applied when braking. This controls how fast the vehicle will stop when the brakes are applied.

.. cpp:member:: float  WheeledVehicleData::engineBrake

	Braking torque applied by the engine when the throttle and brake are both 0. This controls how quickly the vehicle will coast to a stop.

.. cpp:member:: SFXTrack WheeledVehicleData::engineSound

	Looping engine sound. The pitch is dynamically adjusted based on the current engine RPM

.. cpp:member:: float  WheeledVehicleData::engineTorque

	Torque available from the engine at 100% throttle. This controls vehicle acceleration. ie. how fast it will reach maximum speed.

.. cpp:member:: SFXTrack WheeledVehicleData::jetSound

	Looping sound played when the vehicle is jetting.

.. cpp:member:: float  WheeledVehicleData::maxWheelSpeed

	Maximum linear velocity of each wheel. This caps the maximum speed of the vehicle.

.. cpp:member:: SFXTrack WheeledVehicleData::squealSound

	Looping sound played while any of the wheels is slipping. The volume is dynamically adjusted based on how much the wheels are slipping.

.. cpp:member:: ParticleEmitterData WheeledVehicleData::tireEmitter

	ParticleEmitterData datablock used to generate particles from each wheel when the vehicle is moving and the wheel is in contact with the ground.

.. cpp:member:: SFXTrack WheeledVehicleData::WheelImpactSound

	Sound played when the wheels impact the ground. Currently unused.
