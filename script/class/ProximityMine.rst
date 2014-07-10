ProximityMine
=============

A simple proximity mine.

Inherit:
	:doc:`Item`

Description
-----------

A simple proximity mine.

Proximity mines can be deployed using the world editor or thrown by an in-game object. Once armed, any Player or Vehicle object that moves within the mine's trigger area will cause it to explode.

Internally, the ProximityMine object transitions through the following states:

The shape used for the mine may optionally define the following sequences:

Example::

	datablock ProximityMineData( SimpleMine )
	{
	   // ShapeBaseData fields
	   category = "Weapon";
	   shapeFile = "art/shapes/weapons/misc/proximityMine.dts";
	
	   // ItemData fields
	   sticky = true;
	
	   // ProximityMineData fields
	   armingDelay = 0.5;
	   armingSound = MineArmedSound;
	
	   autoTriggerDelay = 0;
	   triggerOnOwner = true;
	   triggerRadius = 5.0;
	   triggerSpeed = 1.0;
	   triggerDelay = 0.5;
	   triggerSound = MineTriggeredSound;
	   explosion = RocketLauncherExplosion;
	
	   // dynamic fields
	   pickUpName = "Proximity Mines";
	   maxInventory = 20;
	
	   damageType = "MineDamage"; // type of damage applied to objects in radius
	   radiusDamage = 30;           // amount of damage to apply to objects in radius
	   damageRadius = 8;            // search radius to damage objects when exploding
	   areaImpulse = 2000;          // magnitude of impulse to apply to objects in radius
	};
	
	function ProximityMineData::onTriggered( %this, %obj, %target )
	{
	   echo( %this.name SPC "triggered by " @ %target.getClassName() );
	}
	
	function ProximityMineData::onExplode( %this, %obj, %position )
	{
	   // Damage objects within the mines damage radiusif ( %this.damageRadius > 0 )
	      radiusDamage( %obj.sourceObject, %position, %this.damageRadius, %this.radiusDamage, %this.damageType, %this.areaImpulse );
	}
	
	function ProximityMineData::damage( %this, %obj, %position, %source, %amount, %damageType )
	{
	   // Explode if any damage is applied to the mine
	   %obj.schedule(50 + getRandom(50), explode);
	}
	
	%obj = newProximityMine()
	{
	   dataBlock = SimpleMine;
	};


Methods
-------


.. cpp:function:: void ProximityMine::explode()

	Manually cause the mine to explode.
