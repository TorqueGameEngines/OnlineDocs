WheeledVehicle
==============

A wheeled vehicle.

Inherit:
	:doc:`Vehicle`

Description
-----------

A multi-wheeled vehicle.

The model used for the WheeledVehicle should contain the elements shown below. Only the collision mesh and hub nodes are actually required for the object to be added to the simulation, but the suspension will look strange if the spring animations are not present.

Collision mesh
	A convex collision mesh at detail size -1.

Hub nodes
	The model must contain a node for each wheel called hubN, where N is a an integer value starting from 0. For example, a four wheeled vehicle would have nodes: hub0, hub1, hub2, and hub3. The wheel model (specified by WheeledVehicleTire) is positioned at the hub node, and automatically rotated to the right orientation (whether on the left or right side of the vehicle).

Spring animations
	To visualise the suspension action, the vehicle model should contain a non-cyclic animation sequence for each wheel that animates the appropriate hub node from t=0 (fully compressed to t=1 (fully extended). The sequences must be called springN, where N matches the wheel hub index.

Steering animation
	Optional non-cyclic animation called 'steering' that animates from t=0 (full right) to t=0.5 (center) to t=1 (full left)."

Brakelight animation
	Optional non-cyclic animation called 'brakeLight' that animates from t=0 (off) to t=1 (braking). This is usually a 2-frame animation controlling the visibility of a quad or mesh to represent each brake light.

The example below shows the datablocks required for a simple 4-wheeled vehicle. The script should be executed on the server, and the vehicle can then be added to the simulation programmatically from the level startup scripts, or by selecting the MyCar datablock from the World Editor (Library->ScriptedObjects->Vehicles).

Example::

	datablock WheeledVehicleTire( MyCarTire )
	{
	   shapeFile = "art/shapes/wheel.dts";
	   staticFriction = 4.2;
	   kineticFriction = 1.0;
	
	   lateralForce = 18000;
	   lateralDamping = 6000;
	   lateralRelaxation = 1;
	
	   longitudinalForce = 18000;
	   longitudinalDamping = 4000;
	   longitudinalRelaxation = 1;
	   radius = 0.61;
	};
	
	datablock WheeledVehicleSpring( MyCarSpring )
	{
	   length = 0.5;
	   force = 2800;
	   damping = 3600;
	   antiSwayForce = 3;
	};
	
	datablock WheeledVehicleData( MyCar )
	{
	   category = "Vehicles";
	   shapeFile = "art/shapes/car.dts";
	
	   maxSteeringAngle = 0.585;
	
	   // 3rd person camera settings
	   cameraRoll = false;
	   cameraMaxDist = 7.8;
	   cameraOffset = 1.0;
	   cameraLag = 0.3;
	   cameraDecay = 1.25;
	
	   useEyePoint = true;
	
	   // Rigid Body
	   mass = "400";
	   massCenter = "0 -0.2 0";
	   massBox = "0 0 0";
	
	   drag = 0.6;
	   bodyFriction = 0.6;
	   bodyRestitution = 0.4;
	   minImpactSpeed = 5;
	   softImpactSpeed = 5;
	   hardImpactSpeed = 15;
	   integration = 8;
	   collisionTol = 0.05;
	   contactTol = 0.4;
	
	   // Engine
	   engineTorque = 4300;
	   engineBrake = 5000;
	   brakeTorque = 10000;
	   maxWheelSpeed = 50;
	
	   // Energy
	   maxEnergy = 100;
	   jetForce = 3000;
	   minJetEnergy = 30;
	   jetEnergyDrain = 2;
	
	   // Sounds
	   engineSound = CarEngineSnd;
	   squealSound = CarSquealSnd;
	   softImpactSound = SoftImpactSnd;
	   hardImpactSound = HardImpactSnd;
	
	   // Particles
	   tireEmitter = "CarTireEmitter";
	   dustEmitter = "CarTireEmitter";
	   dustHeight = "1";
	};
	
	// This function is executed when the WheeledVehicle object is added to the// simulation.
	function MyCar::onAdd( %this, %obj )
	{
	   Parent::onAdd( %this, %obj );
	
	   // Setup the car with some tires & springsfor ( %i = %obj.getWheelCount() - 1; %i >= 0; %i-- )
	   {
	      %obj.setWheelTire( %i,MyCarTire );
	      %obj.setWheelSpring( %i, MyCarSpring );
	      %obj.setWheelPowered( %i, true );
	   }
	
	   // Steer with the front tires only
	   %obj.setWheelSteering( 0, 1 );
	   %obj.setWheelSteering( 1, 1 );
	}

Methods
-------

.. cpp:function:: int WheeledVehicle::getWheelCount()

	Get the number of wheels on this vehicle.

	:return: the number of wheels (equal to the number of hub nodes defined in the model) 

.. cpp:function:: bool WheeledVehicle::setWheelPowered(int wheel, bool powered)

	Set whether the wheel is powered (has torque applied from the engine). A rear wheel drive car for example would set the front wheels to false, and the rear wheels to true.

	:param wheel: index of the wheel to set (hub node #)
	:param powered: flag indicating whether to power the wheel or not

	:return: true if successful, false if failed 

.. cpp:function:: bool WheeledVehicle::setWheelSpring(int wheel, WheeledVehicleSpring spring)

	Set the WheeledVehicleSpring datablock for this wheel.

	:param wheel: index of the wheel to set (hub node #)
	:param spring: WheeledVehicleSpring datablock

	:return: true if successful, false if failed

	Example::

		%obj.setWheelSpring( 0, FrontSpring );

.. cpp:function:: bool WheeledVehicle::setWheelSteering(int wheel, float steering)

	Set how much the wheel is affected by steering. The steering factor controls how much the wheel is rotated by the vehicle steering. For example, most cars would have their front wheels set to 1.0, and their rear wheels set to 0 since only the front wheels should turn. Negative values will turn the wheel in the opposite direction to the steering angle.

	:param wheel: index of the wheel to set (hub node #)
	:param steering: steering factor from -1 (full inverse) to 1 (full)

	:return: true if successful, false if failed 

.. cpp:function:: bool WheeledVehicle::setWheelTire(int wheel, WheeledVehicleTire tire)

	Set the WheeledVehicleTire datablock for this wheel.

	:param wheel: index of the wheel to set (hub node #)
	:param tire: WheeledVehicleTire datablock

	:return: true if successful, false if failed

	Example::

		%obj.setWheelTire( 0, FrontTire );
