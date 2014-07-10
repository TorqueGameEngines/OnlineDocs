TurretShape
===========

Base turret class.

Inherit:
	:doc:`Item`

Description
-----------

Base turret class.

Uses the TurretShapeData datablock for common properties.

The TurretShape class provides a player mountable turret. It also forms the base for AITurretShape, an AI controlled turret. It is based on the Item class, which allows turrets to be treated as any other Item by the Player, such as throwing smaller turrets. When used directly, TurretShape takes input moves from the player's GameConnection to rotate the turret and trigger its weapons.

A turret consists of two components. There is the TurretShape object (or AITurretShape), and then there are one or more ShapeBaseImageData objects that are mounted to the turret. The TurretShape provides the weapons platform that rotates towards a target. The ShapeBaseImageData provides the actual weapon that fires at the target. Any standard ShapeBaseImageData weapon may be used.

Shape File Nodes
----------------

The shape file used for the TurretShape needs to have a number of defined nodes. The first node is named 'heading'. The heading node is special in that it is controlled by the TurretShape code. This means that it should not be animated by the artist, nor should it have anything but the default transform applied to it. This doesn't stop the heading node's parent or its children from being animated, however.

The second special node is named 'pitch'. The pitch node is also controlled by the TurretShape code so it too should not be animated within the shape file. Typically the pitch node will be a child of the heading node, although it need not be a direct child. The pitch node is also optional if you don't want the TurretShape to pitch towards its target. In this case you may be doing something special with the mounted weapon to have its projectiles automatically aim towards the target.

The next set of nodes are weaponMount0 through weaponMount3. These provide up to four mounting points for weapons on the turret. Typically these are children of the pitch nodes, although they need not be direct children of that node. You do not need to have all of these weapon mount point nodes defined within the shape. Only as many as you need for the weapons. The mounted ShapeBaseImageData weapons' mountPoint node will mount to these nodes.

There are four optional nodes named pitch0 through pitch3 that may be used in special cases. These nodes are also controlled by the TurretShape code and have the same restrictions. Their rotation exactly matches that of the standard pitch node. These exist for mounted weapons that may not all rotate about the same x axis. For example, a turret may have two sets of weapons, one mounted above the other. These two sets of weapons could all share the same point of rotation (the pitch node) which means they'll rotate as a group. Or the top weapons could be attached to the pitch node while the bottom weapons could be attached to the pitch0 node. This makes the two sets of weapons rotate about their own centers and provides an entirely different look.

You could also use these additional pitchN nodes to animate some non-weapon attachments on the turret, such as a radar dish or targeting scope. TurretShape also supports four optional heading0 through heading3 nodes that operate in the same way as the pitchN nodes.

Weapon Mounting
---------------

TurretShape weapon mounting is done within the TurretShapeData::onAdd() script method. This method makes use of datablock fields that are only defined in script and are not passed along to the client. The first field is numWeaponMountPoints that defines the number of weapons that will be mounted and the number of weaponMountN nodes to expect within the turret's shape file.

The other fields that are required to mount weapons are the weapon[], weaponAmmo[] and weaponAmmoAmount[] arrays -- one of each per weapon to mount. The weapon[] array points to an ItemData datablock that defines the weapon (just like any Player weapon). The weaponAmmo[] array points to an ItemData datablock that defines the ammo to use for the weapon. Finally, the weaponAmmoAmount[] array is the quantity of ammo the turret has for that weapon.

As turrets use the same inventory system as players, you also need to define the maximum number of weapons and ammo that the turret may possess. Here is an example of setting up three weapons and their ammo for a turret (a TurretShapeData fragment):

Example::

	// Weapon mounting
	   numWeaponMountPoints = 3;
	
	   weapon[0] = TurretWeapon;
	   weaponAmmo[0] = BulletAmmo;
	   weaponAmmoAmount[0] = 10000;
	
	   weapon[1] = TurretWeaponB;
	   weaponAmmo[1] = BulletAmmo;
	   weaponAmmoAmount[1] = 10000;
	
	   weapon[2] = TurretWeapon;
	   weaponAmmo[2] = BulletAmmo;
	   weaponAmmoAmount[2] = 10000;
	
	   maxInv[TurretWeaponB] = 1;
	   maxInv[TurretWeapon] = 2;
	   maxInv[BulletAmmo] = 10000;

Mounted Weapon States
---------------------

There are a couple of things to be aware of so that an turret's mounted weapons play along with the turret's states, especially for AI turrets. Setting TurretShapeData::startLoaded to true indicates that all mounted weapons will start loaded when their state machines start up. A static turret placed with the World Editor would normally begin this way. Setting TurretShapeData::startLoaded to false causes all mounted weapons to not start in a loaded state. This can be used to have the mounted weapons begin in some folded state when a deployable turret is thrown by the player. When a thrown turret comes to rest and begins to deploy, all mounted weapons are automatically set to the loaded state so they may also unfold, start up, or show some other method that the weapon is becoming ready to fight. This could also be used for player mountable turrets so that the weapons come to life when a player mounts the turret.

The default scripts for AITurretShapeData also fires the first image generic trigger on all mounted weapons when the turret is destroyed. This shows up as stateTransitionGeneric0In within a weapon image's state machine. This allows for all weapons to show that they are destroyed or shutting down. Something similar could be done for general TurretShapeData turrets.

Weapons can also feed back to the turret they are mounted on. TurretShape supports the standard ShapeBaseImageData stateRecoil and will play the indicated animation, if available. You can also use ShapeBaseImageData's stateShapeSequence field to play a generic sequence on the turret at any time from a mounted weapon.

Player Mounting
---------------

Turrets act very similar to vehicles when it comes to player mounting. By default colliding with a turret causes the player to mount it, if the turret is free.

When it comes to firing the turret's weapons there are a number of methods that are triggered based on the weaponLinkType on the TurretShapeData datablock. Setting this field to FireTogether causes all weapons to fire at once based on the input from trigger 0. Using GroupedFire will make weaponMount0 and weaponMount2 mounted weapons fire on trigger 0, and weaponMount1 and weaponMount3 mounted weapons fire on trigger 1. Finally, IndividualFire will have each weaponMountN mounted weapons fire based on their own trigger (0 through 3). This provides exact control over which turret weapon will fire when there are multiple weapons mounted.

The player mounting callbacks are done using the TurretBaseData datablock on the server, and in a special case on the TurretBase object on the client. The server side makes use of the standard TurretBaseData::onMountObject() and TurretBaseData::onUnmountObject() callbacks. See those for more information.

When a player mounted turret is destroyed the TurretShapeData::damage() method will automatically kill all mounted players. To modify this behaviour -- such as only dismounting players from a destroyed turret -- you'll need to create your own damage() method for your turret's datablock.

On the client side the special turretMountCallback() callback function is called for the TurretShape object that is being mounted. This callback receives the SimObjectID of the turret object, the SimObjectID of the player doing the mounting or unmounting, and a Boolean set to true if mounting and false if unmounting. As this callback is made on the client, it allows the client to set up any action maps, make HUD changes, etc.

Example::

	// ----------------------------------------------------------------------------// Turret Support// ----------------------------------------------------------------------------// Called by the TurretShape class when a player mounts or unmounts it.// %turret = The turret that was mounted// %player = The player doing the mounting// %mounted = True if the turret was mounted, false if it was unmounted
	function turretMountCallback(%turret, %player, %mounted)
	{
	   echo ( "\c4turretMountCallback ->" @ %mounted );
	
	   if (%mounted)
	   {
	      // Push the action map
	      turretMap.push();
	   }
	   else
	   {
	      // Pop the action map
	      turretMap.pop();
	   }
	}

Turret Destruction
------------------

When a turret is destroyed the default TurretBaseData::onDestroyed() method is called. This causes the turret to sit in a Dead state for TurretBase::DestroyedFadeDelay milliseconds, and then the turret will fade away. If the turret is marked to respawn -- TurretShape::doRespawn() returns true -- then the turret is respawned after TurretShape::RespawnTime milliseconds. By default all turrets placed in the World Editor are marked to respawn.

Turret Optional Animation Sequences
-----------------------------------

If present in the TurretShape's shape, the optional 'heading' and 'pitch' sequences will be played as the turret rotates. These sequences are given a timeline position that corresponds to the turret's rotation within its minimum and maximum ranges. These sequences could be used to rotate wheels or gears on the turret as it rotates, for example.


Methods
-------


.. cpp:function:: bool TurretShape::doRespawn()

	Does the turret respawn after it has been destroyed.

	:return: True if the turret respawns. 

.. cpp:function:: bool TurretShape::getAllowManualFire()

	Get if the turret is allowed to fire through moves.

	:return: True if the turret is allowed to fire through moves. 

.. cpp:function:: bool TurretShape::getAllowManualRotation()

	Get if the turret is allowed to rotate through moves.

	:return: True if the turret is allowed to rotate through moves. 

.. cpp:function:: string TurretShape::getState()

	Get the name of the turret's current state. The state is one of the following: 
	
	* Dead - The TurretShape is destroyed.
	* Mounted - The TurretShape is mounted to an object such as a vehicle.
	* Ready - The TurretShape is free to move. The usual state.

	:return: The current state; one of: "Dead", "Mounted", "Ready" 

.. cpp:function:: Point3F TurretShape::getTurretEulerRotation()

	Get Euler rotation of this turret's heading and pitch nodes.

	:return: the orientation of the turret's heading and pitch nodes in the form of rotations around the X, Y and Z axes in degrees. 

.. cpp:function:: void TurretShape::setAllowManualFire(bool allow)

	Set if the turret is allowed to fire through moves.

	:param allow: If true then the turret may be fired through moves.

.. cpp:function:: void TurretShape::setAllowManualRotation(bool allow)

	Set if the turret is allowed to rotate through moves.

	:param allow: If true then the turret may be rotated through moves.

.. cpp:function:: void TurretShape::setTurretEulerRotation(Point3F rot)

	Set Euler rotation of this turret's heading and pitch nodes in degrees.

	:param rot: The rotation in degrees. The pitch is the X component and the heading is the Z component. The Y component is ignored.

Fields
------


.. cpp:member:: bool  TurretShape::respawn

	Respawn the turret after it has been destroyed. If true, the turret will respawn after it is destroyed.
