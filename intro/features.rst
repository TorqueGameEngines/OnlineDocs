Features
========

Below is a summary of new features we have added to Torque 3D with the 1.2 release. Each summary includes further details on each new feature.

Teleporters
------------

Teleporters are Trigger objects that have a specific behaviour. You define a teleporter with a TriggerData datablock with some special fields defined::

   datablock TriggerData(TeleporterTrigger : DefaultTrigger)
   {
      // Amount of time, in milliseconds, to wait before allowing another
      // object to use this teleportat.
      teleporterCooldown = 0;
      
      // Amount to scale the object's exit velocity. Larger values will
      // propel the object with greater force.
      exitVelocityScale = 0;
      
      // If true, the object will be oriented to the front
      // of the exit teleporter. Otherwise the player will retain their original
      // orientation.
      reorientPlayer = true;
      
      // If true, the teleporter will only trigger if the object
      // enters the front of the teleporter.
      oneSided = false;
      
      // Effects to play at the entrance of the teleporter.
      entranceEffect = EntranceEffect;
      exiteffect = EntranceEffect;
      
      // 2D Sound to play for the client being teleported.
      teleportSound = TeleportSound;
      
   };
    
When you define a teleporter you also need to have an exit as defined by the instance's "exit" field, which is another object in the level -- usually another teleporter trigger. Also note that this just defines the trigger itself. If you want your teleporter to have a shape you'll need to add a shape object to the level, such as a TSStatic.

Weapon Clip System
-------------------

Weapons may now use the optional ammunition clip system.

To make use of the clip system each weapon needs to define two ItemData datablocks. The first is the clip itself, which needs to be part of the AmmoClip class. Here is an example::

   datablock ItemData(LurkerClip)
   {
      // Mission editor category
      category = "AmmoClip";
      
      className = "AmmoClip";
      
      // Basic Item properties
      shapeFile = "art/shapes/weapons/Lurker/TP_Lurker.DAE";
      mass = 1;
      elasticity = 0.2;
      friction = 0.6;
      
      // Dynamic properties defined by the scripts
      pickUpName = "Lurker clip";
      count = 1;
      maxInventory = 10;
   };

The "maxInventory" field indicates the maximum number of clips a player may carry of this type.

Then the ammunition itself needs to be defined as part of the Ammo class::

   datablock ItemData(LurkerAmmo)
   {
      // Mission editor category
      category = "Ammo";
      
      // Add the Ammo namespace as a parent.  The ammo namespace provides
      // common ammo related functions and hooks into the inventory system.
      className = "Ammo";
      
      // Basic Item properties
      shapeFile = "art/shapes/weapons/Lurker/TP_Lurker.DAE";
      mass = 1;
      elasticity = 0.2;
      friction = 0.6;
      
      // Dynamic properties defined by the scripts
      pickUpName = "Lurker ammo";
      maxInventory = 30;
      clip = LurkerClip;
   };

The "maxInventory" field indicates the maximum number of bullets a clip may hold. The "clip" field points back to the clip that holds this ammo.

Finally, you add both the clip and the ammo to the weapon's datablock::

   datablock ShapeBaseImageData(LurkerWeaponImage)
   {
      ...
      
      // Projectiles and Ammo.
      item = Lurker;
      ammo = LurkerAmmo;
      clip = LurkerClip;
      
      ...
   };
    
When you build out the player's datablock you have to add both the weapon and the clip as items the player may carry. You don't need to add the ammo::

   datablock PlayerData(DefaultPlayerData)
   {
      ...
      
      maxInv[Lurker] = 1;
      maxInv[LurkerClip] = 20;
      
      ...
   };

However, when you actually add the weapon and clip to the player during GameCore::loadOut() you'll want to also add the ammunition. This will start the weapon as loaded::

   function GameCore::loadOut(%game, %player)
   {
      ...
      
      // Set up inventory and weapon cycles
      %player.clearWeaponCycle();
      
      %player.setInventory(Lurker, 1);
      %player.setInventory(LurkerClip, %player.maxInventory(LurkerClip));
      %player.setInventory(LurkerAmmo, %player.maxInventory(LurkerAmmo));
      %player.addToWeaponCycle(Lurker);
      
      ...
   }

By default the weapon system will recover any ammunition that is left in a clip when the player manually reloads. Many games operate in this way. If you wish to have any ammunition that is in a clip when the clip is removed to be discarded see the WeaponImage::clearAmmoClip() method and comment out the line indicated.

Per-Player Weapon Cycling
--------------------------

Weapon cycling is no longer set up globally -- it is set up for each player instance. This allows for different players to have different weapon load outs, such as a Soldier with his set of guns and an Alien with its own set of guns.

Often you set up a player's weapon cycling in GameCore::loadOut() but it can occur at any time on the server. The weapon cycling methods themselves are defined in script/server/weapon.cs against the ShapeBase class (which Player inherits from).

When starting to build the weapon cycling list you call clearWeaponCycle() on the player, which clears out any existing list. You then call addToWeaponCycle() on the player for each weapon Item class that you wich the player to cycle through. The order in which the weapons are added to the list is the same order that the player will cycle through them.

Behind the scenes ShapeBase::cycleWeapon() is called on the player whenever the weapons should be cycled. The direction to cycle is passed into this method to move up or down the list.

Multiple Projectiles Per Shot
------------------------------

Weapons may fire multiple projectiles per shot. A shot gun is a good example.

To have multiple projectiles a weapon defines the "projectileNum" field and sets it to a value greater than 1. And if a weapon has a projectile spread defined (with the "projectileSpread" field) then each projectile has its own calculated spread trajectory.


New Damage Reporting
---------------------

Starting with 1.2 T3D supports custom death messages based on the type of damage that killed the player. To set this up you need to define a sendMsgClientKilled_XXX function that provides the death message, where XXX is the damage type. For example, the proximity mine has the following defined for the MineDamage damage type as defined in the mine's datablock::

   // Customized kill message for deaths caused by proximity mines
   function sendMsgClientKilled_MineDamage( %msgType, %client, %sourceClient, %damLoc )
   {
      if ( %sourceClient $= "" )             // editor placed mine
         messageAll( %msgType, '%1 was blown up!', %client.playerName );
      else if ( %sourceClient == %client )   // own mine
         messageAll( %msgType, '%1 stepped on his own mine!', %client.playerName );
      else                                   // enemy placed mine
         messageAll( %msgType, '%1 was blown up by %2!', %client.playerName, 
               %sourceClient.playerName );
   }

This system allows for very specific messages to be sent to all clients. The system has custom death messages set up for Impact, Suicide and a Default (a catch all) damage type.

The Asset Pipeline
-------------------

Characters in T3D can be setup to use different weapon animations and share those animations between different skinned meshes with the same skeleton hierarchy. So a standard T3D character would have COLLADA files for the character’s skinned mesh and skinned skeleton as well as for the character’s animations with just the skeleton for each weapon pose. The animations can be exported individually or combined in one .dae file that is split up through the shape editor.

For more information, see the Torque 3D Character Primer from the Artist Guide.
