Proximity Mines
*****************

Detailed Description
======================

A simple proximity mine.

Proximity mines can be deployed using the world editor or thrown by an in-game object. Once armed, any Player or Vehicle object that moves within the mine's trigger area will cause it to explode.

Internally, the ProximityMine object transitions through the following states:

#. **Thrown**: Mine has been thrown, but has not yet attached to a surface
#. **Deployed**: Mine has attached to a surface but is not yet armed. Start playing the armingSound and *armed* sequence.
#. **Armed**: Mine is armed and will trigger if a Vehicle or Player object moves within the trigger area.
#. **Triggered**: Mine has been triggered and will explode soon. Invoke the onTriggered callback, and start playing the triggerSound and triggered sequence.
#. **Exploded**: Mine has exploded and will be deleted on the server shortly. Invoke the onExplode callback on the server and generate the explosion effects on the client.

.. note:: Proximity mines with the static field set to true will start in the **Armed** state. Use this for mines placed with the World Editor.

The shape used for the mine may optionally define the following sequences:

**armed**
    Sequence to play when the mine is deployed, but before it becomes active and triggerable (armingDelay should be set appropriately).
    
**triggered**
    Sequence to play when the mine is triggered, just before it explodes (triggerDelay should be set appropriately). 

**Example**::

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
       // Damage objects within the mine's damage radius
       if ( %this.damageRadius > 0 )
          radiusDamage( %obj.sourceObject, %position, %this.damageRadius, 
          %this.radiusDamage, %this.damageType, %this.areaImpulse );
    }

    function ProximityMineData::damage( %this, %obj, %position, %source, %amount, %damageType )
    {
       // Explode if any damage is applied to the mine
       %obj.schedule(50 + getRandom(50), explode);
    }

    %obj = new ProximityMine()
    {
       dataBlock = SimpleMine;
    };
                    

**See also**:
    ProximityMineData 

Member Function Documentation
===============================

.. cpp:function:: void ProximityMine::explode ( )  	

    Manually cause the mine to explode.
