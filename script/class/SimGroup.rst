SimGroup
========

A collection of SimObjects that are owned by the group.

Inherit:
	:doc:`SimSet`

Description
-----------

A SimGroup is a stricter form of SimSet. SimObjects may only be a member of a single SimGroup at a time. The SimGroup will automatically enforce the single-group-membership rule (ie. adding an object to a SimGroup will cause it to be removed from its current SimGroup, if any).

Deleting a SimGroup will also delete all SimObjects in the SimGroup.

Example::

	// Create a SimGroup for particle emittersnewSimGroup(Emitters)
	{
	   canSaveDynamicFields = "1";
	
	   newParticleEmitterNode(CrystalEmmiter) {
	      active = "1";
	      emitter = "dustEmitter";
	      velocity = "1";
	      dataBlock = "GenericSmokeEmitterNode";
	      position = "-61.6276 2.1142 4.45027";
	      rotation = "1 0 0 0";
	      scale = "1 1 1";
	      canSaveDynamicFields = "1";
	   };
	
	   newParticleEmitterNode(Steam1) {
	      active = "1";
	      emitter = "SlowSteamEmitter";
	      velocity = "1";
	      dataBlock = "GenericSmokeEmitterNode";
	      position = "-25.0458 1.55289 2.51308";
	      rotation = "1 0 0 0";
	      scale = "1 1 1";
	      canSaveDynamicFields = "1";
	   };
	};

