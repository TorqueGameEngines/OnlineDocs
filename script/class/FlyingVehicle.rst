FlyingVehicle
=============

A flying vehicle.

Inherit:
	:doc:`Vehicle`

Description
-----------

The model used for the FlyingVehicle should contain the elements shown below. Only the collision mesh is actually required for the object to be added to the simulation, but particle emitters will not work unless the relevant nodes are present.

The example below shows the datablock required for a simple FlyingVehicle. The script should be executed on the server, and the vehicle can then be added to the simulation programmatically from the level startup scripts, or by selecting the JetFighter datablock from the World Editor (Library->ScriptedObjects->Vehicles).

Example::

	datablock FlyingVehicleData( JetFighter )
	{
	   category = "Vehicles";
	   shapeFile = "art/shapes/fighterjet.dae";
	
	   createHoverHeight       = 20;
	
	   // 3rd person camera settings
	   cameraRoll              = true;
	   cameraMaxDist           = 16;
	   cameraOffset            = 1.0;
	   cameraLag               =  0.1;
	   cameraDecay             = 1.25;
	
	   // Rigid Body
	   mass                    = 100;
	   massCenter              = "0 -0.2 0";
	   massBox                 = "0 0 0";
	   integration             = 3;
	   collisionTol            = 0.6;
	   contactTol              = 0.4;
	
	   bodyFriction            = 0;
	   bodyRestitution         = 0.8;
	   minRollSpeed            = 2000;
	   minImpactSpeed          = 5;
	   softImpactSpeed         = 3;
	   hardImpactSpeed         = 15;
	
	   drag                    = 0.25;
	   minDrag                 = 40;
	   rotationalDrag          = 20;
	
	   // Autostabilizer
	   maxAutoSpeed            = 6;
	   autoAngularForce        = 400;
	   autoLinearForce         = 300;
	   autoInputDamping        = 0.55;
	
	   // Maneuvering
	   maxSteeringAngle        = 3;
	   horizontalSurfaceForce  = 20;
	   verticalSurfaceForce    = 20;
	   maneuveringForce        = 6400;
	   steeringForce           = 500;
	   steeringRollForce       = 200;
	   rollForce               = 10;
	   hoverHeight             = 0.5;
	   createHoverHeight       = 0.5;
	   maxForwardSpeed         = 90;
	
	   // Vertical jetting
	   maxEnergy               = 100;
	   jetForce                = 3000;
	   minJetEnergy            = 28;
	   jetEnergyDrain          = 2.8;
	   vertThrustMultiple      = 3.0;
	
	   // Emitters
	   forwardJetEmitter       = FighterJettingEmitter;
	   backwardJetEmitter      = FighterJettingEmitter;
	   downJetEmitter          = FighterJettingEmitter;
	   trailEmitter            = FighterContrailEmitter;
	   minTrailSpeed           = 10;
	
	   // Sounds
	   engineSound             = FighterEngineSnd;
	   jetSound                = FighterJettingSnd;
	};
	
	// This function is executed when the FlyingVehicle object is added to the simulation.
	function JetFighter::onAdd( %this, %obj )
	{
	   Parent::onAdd( %this, %obj );
	
	   // Allow jetting energy to recharge over time
	   %obj.setRechargeRate( 2 );
	}


Methods
-------


.. cpp:function:: void FlyingVehicle::useCreateHeight(bool enabled)

	Set whether the vehicle should temporarily use the createHoverHeight specified in the datablock. This can help avoid problems with spawning.

	:param enabled: true to use the datablock createHoverHeight, false otherwise
