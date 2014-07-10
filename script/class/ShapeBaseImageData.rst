ShapeBaseImageData
==================

object.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Represents geometry to be mounted to a ShapeBase object.

Unlike other datablocks, ShapeBaseImageData does not have a base class associated with it. Instead, this datablock is an abstraction of geometry that can only be mounted to a ShapeBase object and is only used by a ShapBase object.

The most common use for ShapeBaseImageData objects (referred to as Images hereafter) is for weapons carried by a Player or Vehicle object, and much of the functionality provided by the Image is aimed at that use-case. Images include a powerful state machine to control animations, sounds, script callbacks, and state transitions. This state system is downloaded to the client so that clients can predict state changes and animate accordingly.

The following example - a grenade launcher weapon - demonstates the flexibility of the system. The weapon includes states and transitions to handle the normal ready->fire->reload->ready loop as well as noammo->dryfire for firing when the weapon is out of ammo.

Example::

	datablock ShapeBaseImageData( GrenadeLauncherImage )
	{
	   // Basic properties
	   shapefile = "art/shapes/weapons/ramrifle/base.dts";
	
	   // Specify mount point & offset for 3rd person, and eye offset// for first person rendering.mountPoint = 0;
	   offset = "0.0 0.0 0.1";
	   eyeOffset = "0.25 0.4 -0.4";
	
	   // Add the WeaponImage namespace as a parent, WeaponImage namespace// provides some hooks into the inventory system.className = "WeaponImage";
	
	   // Projectile and Ammo.
	   item = GrenadeLauncher;
	   ammo = GrenadeLauncherAmmo;
	   projectile = GrenadeLauncherProjectile;
	   wetProjectile = GrenadeWetProjectile;
	   projectileType = Projectile;
	
	   // Shell casingscasing = GrenadeLauncherShellCasing;
	   shellExitDir = "1.0 0.3 1.0";
	   shellExitOffset = "0.15 -0.56 -0.1";
	   shellExitVariance = 15.0;
	   shellVelocity = 3.0;
	
	   // Let there be light - NoLight, ConstantLight, PulsingLight, WeaponFireLight.lightType = "WeaponFireLight";
	   lightColor = "1.0 1.0 0.9";
	   lightDuration = 200;
	   lightRadius = 20;
	
	
	   // Initial start up statestateName[0] = "Preactivate";
	   stateTransitionOnLoaded[0] = "Activate";
	   stateTransitionOnNoAmmo[0] = "NoAmmo";
	
	   // Activating the gun.// Called when the weapon is first mounted and there is ammo.stateName[1] = "Activate";
	   stateTransitionOnTimeout[1] = "Ready";
	   stateTimeoutValue[1] = 0.6;
	   stateSequence[1] = "Activate";
	
	   // Ready to fire, just waiting for the triggerstateName[2] = "Ready";
	   stateTransitionOnNoAmmo[2] = "NoAmmo";
	   stateTransitionOnTriggerDown[2] = "CheckWet";
	   stateSequence[2] = "Ready";
	
	   // Fire the weapon. Calls the fire script which does the actual work.stateName[3] = "Fire";
	   stateTransitionOnTimeout[3] = "PostFire";
	   stateTimeoutValue[3] = 0.4;
	   stateFire[3] = true;
	   stateAllowImageChange[3] = false;
	   stateSequence[3] = "Fire";
	   stateScript[3] = "onFire";
	   stateSound[3] = GrenadeLauncherFireSound;
	
	   // Check ammostateName[4] = "PostFire";
	   stateTransitionOnAmmo[4] = "Reload";
	   stateTransitionOnNoAmmo[4] = "NoAmmo";
	
	   // Play the reload animation, and transition back into Ready statestateName[5] = "Reload";
	   stateTransitionOnTimeout[5] = "Ready";
	   stateTimeoutValue[5] = 0.2;
	   stateAllowImageChange[5] = false;
	   stateSequence[5] = "Reload";
	   stateEjectShell[5] = false; // set to true to enable shell casing ejectstateSound[5] = GrenadeLauncherReloadSound;
	
	   // No ammo in the weapon, just idle until something shows up.// Play the dry fire sound if the trigger iS pulled.stateName[6] = "NoAmmo";
	   stateTransitionOnAmmo[6] = "Reload";
	   stateSequence[6] = "NoAmmo";
	   stateTransitionOnTriggerDown[6] = "DryFire";
	
	   // No ammo dry firestateName[7] = "DryFire";
	   stateTimeoutValue[7] = 1.0;
	   stateTransitionOnTimeout[7] = "NoAmmo";
	   stateSound[7] = GrenadeLauncherFireEmptySound;
	
	   // Check if wetstateName[8] = "CheckWet";
	   stateTransitionOnWet[8] = "WetFire";
	   stateTransitionOnNotWet[8] = "Fire";
	
	   // Wet firestateName[9] = "WetFire";
	   stateTransitionOnTimeout[9] = "PostFire";
	   stateTimeoutValue[9] = 0.4;
	   stateFire[9] = true;
	   stateAllowImageChange[9] = false;
	   stateSequence[9] = "Fire";
	   stateScript[9] = "onWetFire";
	   stateSound[9] = GrenadeLauncherFireSound;
	};

Images are mounted into a slot on the target ShapeBase derrived object as shown below.

Example::

	$WeaponSlot = 0;
	
	...
	
	// Use a weapon by mounting it onto the given ShapeBase derrived object.// %data is the weapon whose .image member points to its ShapeBaseImageData datablock// %obj is the object to mount the weapon on
	function Weapon::onUse( %data, %obj )
	{
	   // Default behavior for all weapons is to mount it into the objects weapon// slot, as defined by $WeaponSlot here, and is usually slot 0. We begin by// checking if the requested weapon is already mounted.if ( %obj.getMountedImage($WeaponSlot) != %data.image.getId() )
	   {
	      // The requested weapon is not mounted on $WeaponSlot so mount it now.
	      %obj.mountImage( %data.image, $WeaponSlot );
	   }
	}

Weapon Shape Nodes
------------------

The DTS or DAE model used for the Image has the following requirements:

Weapon Muzzle Flash
-------------------

When the Image is used as a weapon, a sequence can be added to display a muzzle flash when the weapon is fired (if stateSequenceRandomFlash is set to true for the firing state). The name of the muzzle flash sequence is the same as the state sequence (eg. fire), but with '_vis' appended (eg. fire_vis).

In the example below, the muzzle flash is made up of three quads; one facing the player, and two crossed quads pointing out of the weapon so viewers perpendicular to the player will also see the flash.

The visibility of the muzzle flash mesh is animated on for 1 frame then off for 1 frame as shown below, but any Torque supported animation method could be used as well. For example, the node the quads are attached to could be rotated or scaled, or the mesh Material could be animated (UV or frame) to provide further variation.

First Person Shape [Optional]
-----------------------------

The ShapeBaseImageData supports an optional shape that is displayed when the player is in a first person view. This shape is defined using the shapeFileFP property. You also must set an eyeOffset or make use of an eye mount node for this shape to be used in a first person view.

Having this second shape defined provides for more flexibility between 3rd person (and what other players see) and 1st person views. In a typical first person shooter the 3rd person weapon is not as detailed and supports a limited number of animation sequences. Just enough for the other players in the game to get a sense of what the player is doing. Then the 1st person weapon has a lot more detail, such as moving parts, etc. It may also have some arms and hands incldued that are animated when reloading the weapon and other actions. Only the player holding the weapon sees all of this.

There are a number of things to keep in mind if you make use of shapeFileFP:

Animation Sequence Transitions
------------------------------

Starting with T3D 1.2 control is now given over transitioning from one image state's sequence to another state's sequence. The new state "stateSequenceTransitionIn" and "stateSequenceTransitionOut" flags dictate if the current state's sequence should be transitioned into when changing to the current state, or transitioned out of when switching to a new state. However, there are times when you don't want to do an animation sequence transition regardless of which state you are coming from. An example of this is the traditional "Fire" state. A Fire state should play immediately and not be transitioned into. In these cases a state may set the "stateSequenceNeverTransition" flag. With that set a state's sequence will begin to play immediately.

Animation Sequence Selection
----------------------------

When it comes to choosing what sequence to play on the mounted image there are now some new rules. Under 1.1 when an image state requested a named sequence that is found on the mounted image and played -- its action sequence. This still occurs under 1.2. However, it is now possible to modify the name of the sequence to play based on some prefixes. PlayerData now has two additional, optional fields: imageAnimPrefix and imageAnimPrefixFP. Just like how these same fields on ShapeBaseImageData can modify when sequences are played on the player based on what is mounted (see Player class documentation), these two PlayerData fields can modify what sequence is played on the mounted image based on the mounting player. This becomes especially useful when combined with 1st person arms -- although here we're just talking about weapons/mounted images.

Let's suppose we have two types of player: Soldier and Alien. We may want each type of player to use the same weapon slightly differently (or even radically differently, such as the Alien holding the weapon upside down). We use the "Soldier" anim prefix in the soldier's datablock and the "Alien" prefix in the alien's datablock. Now when looking up the sequence for a weapon's fire state -- usually called "fire" by convention -- the appropriate prefix is added first. And if that prefixed sequence is not found, then we fall back to the standard sequence name. So the soldier's sequence name search looks like this:

and the alien's sequence name search looks like this:

This gives the artist greater control over how the weapons look. And because there are separate prefixes possible on PlayerData for 1st person and 3rd person you can mix and match as appropriate. So you could set a prefix for 1st person, but leave it blank for 3rd person (don't do anything special in 3rd person).

Another way that an image state's sequence name could be modified is through the new ShapeBase::setImageScriptAnimPrefix() method. This allows you to insert an additional prefix into the name look up. The current scripts pass along the player's current pose name, but anything could be passed in based on game play. This can be even more useful with the 1st person arms. You could then have a weapon idle state when swimming that moves the weapon (and 1st person arms) in a gentle swim motion. When you combine the PlayerData prefix with the script anim prefix and finally with the image state sequence name, you end up with the following sequence name search pattern (the first found is used):

Whenever ShapeBase::setImageScriptAnimPrefix() is called there is a transition from the currently playing state sequence into the new script prefixed animation sequence. In our example, this allows for a transition from walking to swimming for the weapon. The new ShapeBaseImageData scriptAnimationTransitionTime controls how long to take for this transition.

eyeMount Node [Optional]
------------------------

As with 1.1 the placement of the 1st person image may be set with the eyeOffset parameter. Now with 1.2 the 1st person image may be placed based on a node in the 1st person DTS/DAE shape, the "eyeMount" node. When the ShapeBaseImageData's useEyeNode parameter is made true, the image is effectively mounted to the 3rd person player's "eye" node, locking it into place. This allows the artist in their 3D application to precisely place the 1st person weapon in view when their 3D app's camera is placed on the eyeMount node and has the same field of view as Torque. This is very handy when animating the 1st person weapon, especially with 1st person arms.

Also with 1.2 an image that is placed with the eyeMount node may have an "eye" node defined. When found the player's camera is mounted to the image's "eye" node rather than the 3rd person player's "eye" node. This allows for animating the camera such as during a fire sequence.

Allowing for this much control does have a potential down side. In order for a weapon to fire correctly on the server it needs to have its muzzle point at the correct location. If a weapon's root pose (without animation) doesn't have its muzzle point at roughly the same location as when the weapon is fired, then the new ShapeBaseImageData "animateOnServer" flag should be set. When set the server will perform all state machine animation to ensure the muzzle point is at the correct location when required. This puts an extra strain on the server. If care is taken when building the weapons such that the root pose is close enough to the fire pose, then you can safely leave the "animateOnServer" flag off and not have to worry about the extra server load.

Special State Triggers
----------------------

Starting with 1.2 there are now a number of new triggers that may be set for a ShapeBaseImageData's state machine to react to. These provide greater game play control over an image's state flow. The first are the "stateTransitionOnMotion" and "stateTransitionOnNoMotion" triggers. This trigger occurs whenever the mounting ShapeBase (usually a Player) has x, y or z motion applied through the Move structure. From a Player perspective this means whenever the user moves their player forwards, backwards or strafes. That has been used to provide weapons a slight bobbing appearance (using an animation sequence) when the weapon is idle. Fire and Reload states don't usually make use of these triggers to keep those actions solid.

There has always been a target trigger for ShapeBaseImageData but under 1.1 it was not possible to set it, nor was it used. Starting with 1.2 you can now set the target trigger in script using ShapeBase::setImageTargetState() and use stateTransitionOnTarget and stateTransitionOnNoTarget for whatever game play reasons are required.

Finally, there are four new generic triggers that may be set from script and used for whatever purpose the game play imposes. These are "stateTransitionGeneric0In", "stateTransitionGeneric1In", etc. and "stateTransitionGeneric0Out", "stateTransition1Out" etc. The FPS Tutorial weapons use the first generic trigger to indicate that the player is sprinting and switch to a Sprint state to prevent firing of the weapon. Other possible uses are for iron sights.

Special States
--------------

The client and server move through a ShapeBaseImageData's state machine independantly according to various triggers, timeouts, etc. The client is not normally told to move to a specific state when the server does. However, there are three instances where the client is told by the server to immediately jump to a given state. This ensures that the client's experience matches the server at key moments. As such, only one of each of these states may exist in a single ShapeBaseImageData state machine at a time.

The fire state is the first such state. It is indicated by setting the state's "stateFire" flag to true. This is the state immediately jumped to when the weapon begins to fire.

The alternate fire state is the second forced jump point (new in 1.2). It is indicated by setting the state's "stateAlternateFire" flag to true. Not all weapons have an alternate fire state. In fact most games treat a weapon's alternate fire as a separate weapon altogether.

The reload state is the last special state (new in 1.2). It is indicated by setting the state's "stateReload" flag to true. This state is triggered if the weapon makes use of the new 1.2 ammo clip system and the weapon is reloading a clip, either automatically or manually triggered by the client.


Methods
-------


.. cpp:function:: void ShapeBaseImageData::onMount(ShapeBase obj, int slot, float dt)

	Called when the Image is first mounted to the object.

	:param obj: object that this Image has been mounted to
	:param slot: Image mount slot on the object
	:param dt: time remaining in this Image update

.. cpp:function:: void ShapeBaseImageData::onUnmount(ShapeBase obj, int slot, float dt)

	Called when the Image is unmounted from the object.

	:param obj: object that this Image has been unmounted from
	:param slot: Image mount slot on the object
	:param dt: time remaining in this Image update

Fields
------


.. cpp:member:: bool  ShapeBaseImageData::accuFire

	Flag to control whether the Image's aim is automatically converged with the crosshair. Currently unused.

.. cpp:member:: bool  ShapeBaseImageData::animateAllShapes

	Indicates that all shapes should be animated in sync. When multiple shapes are defined for this image datablock, each of them are automatically animated in step with each other. This allows for easy switching between between shapes when some other condition changes, such as going from first person to third person, and keeping their look consistent. If you know that you'll never switch between shapes on the fly, such as players only being allowed in a first person view, then you could set this to false to save some calculations. There are other circumstances internal to the engine that determine that only the current shape should be animated rather than all defined shapes. In those cases, this property is ignored.

.. cpp:member:: bool  ShapeBaseImageData::animateOnServer

	Indicates that the image should be animated on the server. In most cases you'll want this set if you're using useEyeNode. You may also want to set this if the muzzlePoint is animated while it shoots. You can set this to false even if these previous cases are true if the image's shape is set up in the correct position and orientation in the 'root' pose and none of the nodes are animated at key times, such as the muzzlePoint essentially remaining at the same position at the start of the fire state (it could animate just fine after the projectile is away as the muzzle vector is only calculated at the start of the state). You'll also want to set this to true if you're animating the camera using the image's 'eye' node -- unless the movement is very subtle and doesn't need to be reflected on the server.

.. cpp:member:: Point3F  ShapeBaseImageData::camShakeAmp

	Amplitude of the camera shaking effect.

.. cpp:member:: Point3F  ShapeBaseImageData::camShakeFreq

	Frequency of the camera shaking effect.

.. cpp:member:: DebrisData ShapeBaseImageData::casing

	DebrisData datablock to use for ejected casings.

.. cpp:member:: bool  ShapeBaseImageData::cloakable

	Whether this Image can be cloaked. Currently unused.

.. cpp:member:: bool  ShapeBaseImageData::computeCRC

	If true, verify that the CRC of the client's Image matches the server's CRC for the Image when loaded by the client.

.. cpp:member:: bool  ShapeBaseImageData::correctMuzzleVector

	Flag to adjust the aiming vector to the eye's LOS point when in 1st person view.

.. cpp:member:: bool  ShapeBaseImageData::correctMuzzleVectorTP

	Flag to adjust the aiming vector to the camera's LOS point when in 3rd person view.

.. cpp:member:: bool  ShapeBaseImageData::emap

	Whether to enable environment mapping on this Image.

.. cpp:member:: MatrixPosition  ShapeBaseImageData::eyeOffset

	"X Y Z" translation offset from the ShapeBase model's eye node. When in first person view, this is the offset from the eye node to place the gun. This gives the gun a fixed point in space, typical of a lot of FPS games.

.. cpp:member:: MatrixRotation  ShapeBaseImageData::eyeRotation

	"X Y Z ANGLE" rotation offset from the ShapeBase model's eye node. When in first person view, this is the rotation from the eye node to place the gun.

.. cpp:member:: bool  ShapeBaseImageData::firstPerson

	Set to true to render the image in first person.

.. cpp:member:: caseString  ShapeBaseImageData::imageAnimPrefix

	Passed along to the mounting shape to modify animation sequences played in third person. [optional].

.. cpp:member:: caseString  ShapeBaseImageData::imageAnimPrefixFP

	Passed along to the mounting shape to modify animation sequences played in first person. [optional].

.. cpp:member:: float  ShapeBaseImageData::lightBrightness

	Brightness of the light this Image emits. Only valid for WeaponFireLight.

.. cpp:member:: ColorF  ShapeBaseImageData::lightColor

	The color of light this Image emits.

.. cpp:member:: int  ShapeBaseImageData::lightDuration

	Duration in SimTime of Pulsing and WeaponFire type lights.

.. cpp:member:: float  ShapeBaseImageData::lightRadius

	Radius of the light this Image emits.

.. cpp:member:: ShapeBaseImageLightType ShapeBaseImageData::lightType

	The type of light this Image emits.

.. cpp:member:: float  ShapeBaseImageData::mass

	Mass of this Image. This is added to the total mass of the ShapeBase object.

.. cpp:member:: int  ShapeBaseImageData::maxConcurrentSounds

	Maximum number of sounds this Image can play at a time. Any value lt = 0 indicates that it can play an infinite number of sounds.

.. cpp:member:: float  ShapeBaseImageData::minEnergy

	Minimum Image energy for it to be operable.

.. cpp:member:: int  ShapeBaseImageData::mountPoint

	Mount node # to mount this Image to. This should correspond to a mount# node on the ShapeBase derived object we are mounting to.

.. cpp:member:: MatrixPosition  ShapeBaseImageData::offset

	"X Y Z" translation offset from this Image's mountPoint node to attach to. Defaults to "0 0 0". ie. attach this Image's mountPoint node to the ShapeBase model's mount# node without any offset.

.. cpp:member:: ProjectileData ShapeBaseImageData::Projectile

	The projectile fired by this Image.

.. cpp:member:: MatrixRotation  ShapeBaseImageData::rotation

	"X Y Z ANGLE" rotation offset from this Image's mountPoint node to attach to. Defaults to "0 0 0". ie. attach this Image's mountPoint node to the ShapeBase model's mount# node without any additional rotation.

.. cpp:member:: float  ShapeBaseImageData::scriptAnimTransitionTime

	The amount of time to transition between the previous sequence and new sequence when the script prefix has changed. When setImageScriptAnimPrefix() is used on a ShapeBase that has this image mounted, the image will attempt to switch to the new animation sequence based on the given script prefix. This is the amount of time it takes to transition from the previously playing animation sequence tothe new script prefix-based animation sequence.

.. cpp:member:: bool  ShapeBaseImageData::shakeCamera

	Flag indicating whether the camera should shake when this Image fires.

.. cpp:member:: filename  ShapeBaseImageData::shapeFile

	The DTS or DAE model to use for this Image.

.. cpp:member:: filename  ShapeBaseImageData::shapeFileFP

	The DTS or DAE model to use for this Image when in first person. This is an optional parameter that also requires either eyeOffset or useEyeNode to be set. If none of these conditions is met then shapeFile will be used for all cases. Typically you set a first person image for a weapon that includes the player's arms attached to it for animating while firing, reloading, etc. This is typical of many FPS games.

.. cpp:member:: Point3F  ShapeBaseImageData::shellExitDir

	Vector direction to eject shell casings.

.. cpp:member:: float  ShapeBaseImageData::shellExitVariance

	Variance (in degrees) from the shellExitDir vector to eject casings.

.. cpp:member:: float  ShapeBaseImageData::shellVelocity

	Speed at which to eject casings.

.. cpp:member:: bool  ShapeBaseImageData::stateAllowImageChange [31]

	If false, other Images will temporarily be blocked from mounting while the state machine is executing the tasks in this state. For instance, if we have a rocket launcher, the player shouldn't be able to switch out while firing. So, you'd set stateAllowImageChange to false in firing states, and true the rest of the time.

.. cpp:member:: bool  ShapeBaseImageData::stateAlternateFire [31]

	The first state with this set to true is the state entered by the client when it receives the 'altFire' event.

.. cpp:member:: bool  ShapeBaseImageData::stateDirection [31]

	Direction of the animation to play in this state. True is forward, false is backward.

.. cpp:member:: bool  ShapeBaseImageData::stateEjectShell [31]

	If true, a shell casing will be ejected in this state.

.. cpp:member:: ParticleEmitterData ShapeBaseImageData::stateEmitter [31]

	Emitter to generate particles in this state (from muzzle point or specified node).

.. cpp:member:: string  ShapeBaseImageData::stateEmitterNode [31]

	Name of the node to emit particles from.

.. cpp:member:: float  ShapeBaseImageData::stateEmitterTime [31]

	How long (in seconds) to emit particles on entry to this state.

.. cpp:member:: float  ShapeBaseImageData::stateEnergyDrain [31]

	Amount of energy to subtract from the Image in this state. Energy is drained at stateEnergyDrain units/tick as long as we are in this state.

.. cpp:member:: bool  ShapeBaseImageData::stateFire [31]

	The first state with this set to true is the state entered by the client when it receives the 'fire' event.

.. cpp:member:: bool  ShapeBaseImageData::stateIgnoreLoadedForReady [31]

	If set to true, and both ready and loaded transitions are true, the ready transition will be taken instead of the loaded transition. A state is 'ready' if pressing the fire trigger in that state would transition to the fire state.

.. cpp:member:: ShapeBaseImageLoadedState ShapeBaseImageData::stateLoadedFlag [31]

	Set the loaded state of the Image. 
	
	* IgnoreLoaded: Don't change Image loaded state.
	* Loaded: Set Image loaded state to true.
	* NotLoaded: Set Image loaded state to false.

.. cpp:member:: caseString  ShapeBaseImageData::stateName [31]

	Name of this state.

.. cpp:member:: ShapeBaseImageRecoilState ShapeBaseImageData::stateRecoil [31]

	Type of recoil sequence to play on the ShapeBase object on entry to this state. 
	
	* NoRecoil: Do not play a recoil sequence.
	* LightRecoil: Play the light_recoil sequence.
	* MediumRecoil: Play the medium_recoil sequence.
	* HeavyRecoil: Play the heavy_recoil sequence.

.. cpp:member:: bool  ShapeBaseImageData::stateReload [31]

	The first state with this set to true is the state entered by the client when it receives the 'reload' event.

.. cpp:member:: bool  ShapeBaseImageData::stateScaleAnimation [31]

	If true, the timeScale of the stateSequence animation will be adjusted such that the sequence plays for stateTimeoutValue seconds.

.. cpp:member:: bool  ShapeBaseImageData::stateScaleAnimationFP [31]

	If true, the timeScale of the first person stateSequence animation will be adjusted such that the sequence plays for stateTimeoutValue seconds.

.. cpp:member:: bool  ShapeBaseImageData::stateScaleShapeSequence [31]

	Indicates if the sequence to be played on the mounting shape should be scaled to the length of the state.

.. cpp:member:: caseString  ShapeBaseImageData::stateScript [31]

	Method to execute on entering this state. Scoped to this image class name, then ShapeBaseImageData . The script callback function takes the same arguments as the onMount callback.

.. cpp:member:: string  ShapeBaseImageData::stateSequence [31]

	Name of the sequence to play on entry to this state.

.. cpp:member:: bool  ShapeBaseImageData::stateSequenceNeverTransition [31]

	Never allow a transition to this sequence. Often used for a fire sequence.

.. cpp:member:: bool  ShapeBaseImageData::stateSequenceRandomFlash [31]

	If true, the muzzle flash sequence will be played while in this state. The name of the muzzle flash sequence is the same as stateSequence, with "_vis" at the end.

.. cpp:member:: bool  ShapeBaseImageData::stateSequenceTransitionIn [31]

	Do we transition to the state's sequence when we enter the state?

.. cpp:member:: bool  ShapeBaseImageData::stateSequenceTransitionOut [31]

	Do we transition to the new state's sequence when we leave the state?

.. cpp:member:: float  ShapeBaseImageData::stateSequenceTransitionTime [31]

	The time to transition in or out of a sequence.

.. cpp:member:: string  ShapeBaseImageData::stateShapeSequence [31]

	Name of the sequence that is played on the mounting shape.

.. cpp:member:: SFXTrack ShapeBaseImageData::stateSound [31]

	Sound to play on entry to this state.

.. cpp:member:: ShapeBaseImageSpinState ShapeBaseImageData::stateSpinThread [31]

	Controls how fast the 'spin' animation sequence will be played in this state. 
	
	* Ignore: No change to the spin sequence.
	* Stop: Stops the spin sequence at its current position.
	* SpinUp: Increase spin sequence timeScale from 0 (on state entry) to 1 (after stateTimeoutValue seconds).
	* SpinDown: Decrease spin sequence timeScale from 1 (on state entry) to 0 (after stateTimeoutValue seconds).
	* FullSpeed: Resume the spin sequence playback at its current position with timeScale=1.

.. cpp:member:: float  ShapeBaseImageData::stateTimeoutValue [31]

	Time in seconds to wait before transitioning to stateTransitionOnTimeout.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric0In [31]

	Name of the state to transition to when the generic trigger 0 state changes to true.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric0Out [31]

	Name of the state to transition to when the generic trigger 0 state changes to false.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric1In [31]

	Name of the state to transition to when the generic trigger 1 state changes to true.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric1Out [31]

	Name of the state to transition to when the generic trigger 1 state changes to false.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric2In [31]

	Name of the state to transition to when the generic trigger 2 state changes to true.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric2Out [31]

	Name of the state to transition to when the generic trigger 2 state changes to false.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric3In [31]

	Name of the state to transition to when the generic trigger 3 state changes to true.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionGeneric3Out [31]

	Name of the state to transition to when the generic trigger 3 state changes to false.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnAltTriggerDown [31]

	Name of the state to transition to when the alt trigger state of the Image changes to false (alt fire button up).

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnAltTriggerUp [31]

	Name of the state to transition to when the alt trigger state of the Image changes to true (alt fire button down).

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnAmmo [31]

	Name of the state to transition to when the ammo state of the Image changes to true.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnLoaded [31]

	Name of the state to transition to when the loaded state of the Image changes to 'Loaded'.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnMotion [31]

	Name of the state to transition to when the Player moves.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnNoAmmo [31]

	Name of the state to transition to when the ammo state of the Image changes to false.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnNoMotion [31]

	Name of the state to transition to when the Player stops moving.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnNoTarget [31]

	Name of the state to transition to when the Image loses a target.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnNotLoaded [31]

	Name of the state to transition to when the loaded state of the Image changes to 'Empty'.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnNotWet [31]

	Name of the state to transition to when the Image exits the water.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnTarget [31]

	Name of the state to transition to when the Image gains a target.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnTimeout [31]

	Name of the state to transition to when we have been in this state for stateTimeoutValue seconds.

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnTriggerDown [31]

	Name of the state to transition to when the trigger state of the Image changes to false (fire button released).

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnTriggerUp [31]

	Name of the state to transition to when the trigger state of the Image changes to true (fire button down).

.. cpp:member:: string  ShapeBaseImageData::stateTransitionOnWet [31]

	Name of the state to transition to when the Image enters the water.

.. cpp:member:: bool  ShapeBaseImageData::stateWaitForTimeout [31]

	If false, this state ignores stateTimeoutValue and transitions immediately if other transition conditions are met.

.. cpp:member:: bool  ShapeBaseImageData::useEyeNode

	Mount image using image's eyeMount node and place the camera at the image's eye node (or at the eyeMount node if the eye node is missing). When in first person view, if an 'eyeMount' node is present in the image's shape, this indicates that the image should mount eyeMount node to Player eye node for image placement. The Player's camera should also mount to the image's eye node to inherit any animation (or the eyeMount node if the image doesn't have an eye node).

.. cpp:member:: bool  ShapeBaseImageData::useRemainderDT

	If true, allow multiple timeout transitions to occur within a single tick (useful if states have a very small timeout).

.. cpp:member:: bool  ShapeBaseImageData::usesEnergy

	Flag indicating whether this Image uses energy instead of ammo. The energy level comes from the ShapeBase object we're mounted to.
