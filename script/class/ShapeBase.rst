ShapeBase
=========

A scriptable, renderable shape.

Inherit:
	:doc:`GameBase`

Description
-----------

A scriptable, renderable shape.

ShapeBase is the renderable shape from which most of the scriptable, game objects are derived, including the Player, Vehicle and Item classes. ShapeBase provides collision detection, audio channels, and animation as well as damage (and damage states), energy, and the ability to mount Images and objects.

ShapeBase objects are not normally instantiated in the scene; derived classes such as Player, WheeledVehicle, and, StaticShape are used instead. But ShapeBase (and the associated datablock, ShapeBaseData) may be used to provide functionality common to all derived objects.

A ShapeBase object consists of a DTS or DAE shape file. This file has the following requirements:

Nodes



Sequences Indicating Condition



Detail Levels

Control Object
--------------

Generally in a Torque game, each client is in control of a single game object (such as a Player in an FPS game, or a WheeledVehicle in a racing game). In a game where the client has control over multiple objects (such as units in an RTS), the control object may be the Camera that determines the client's view of the world (although in general, the client's camera object does not need to be the same as the control object).

The object controlled by the client is important for several reasons:

Energy/Damage
-------------

ShapeBase includes basic enery and damage systems that may be used by derived classes as required. For example, the Player class uses energy to determine whether the character is capabable of running and jumping, which can be used to mimic the character getting tired and having to rest before continuing. The Player class also uses the damage system PlayerData::onDestroyed callback to trigger a death animation. The Vehicle classes use the current damage level to trigger particle emitters, so a vehicle could progressively generate more smoke as it becomes more damaged.

ShapeBase also includes parameters to 'blow up' the object when it is Destroyed (damage level above ShapeBaseData::destroyedLevel). Blowing up an object can generate an explosion and debris, as well as exclude the object from rendering.

Parameters to control the object's energy and damage functionality can be found in the ShapeBaseData datablock.


Methods
-------


.. cpp:function:: void ShapeBase::applyDamage(float amount)

	Increment the current damage level by the specified amount.

	:param amount: value to add to current damage level

.. cpp:function:: bool ShapeBase::applyImpulse(Point3F pos, Point3F vec)

	Apply an impulse to the object.

	:param pos: world position of the impulse
	:param vec: impulse momentum (velocity * mass)

	:return: true 

.. cpp:function:: void ShapeBase::applyRepair(float amount)

	Repair damage by the specified amount. Note that the damage level is only reduced by repairRate per tick, so it may take several ticks for the total repair to complete.

	:param amount: total repair value (subtracted from damage level over time)

.. cpp:function:: void ShapeBase::blowUp()

	Explodes an object into pieces.

.. cpp:function:: bool ShapeBase::canCloak()

	Check if this object can cloak.

	:return: true 

.. cpp:function:: void ShapeBase::changeMaterial(string mapTo, Material oldMat, Material newMat)

	Change one of the materials on the shape. This method changes materials per mapTo with others. The material that is being replaced is mapped to unmapped_mat as a part of this transition.

	:param mapTo: the name of the material target to remap (from getTargetName)
	:param oldMat: the old Material that was mapped
	:param newMat: the new Material to map

	Example::

		// remap the first material in the shape
		%mapTo = %obj.getTargetName( 0 );
		%obj.changeMaterial( %mapTo, 0, MyMaterial );

.. cpp:function:: bool ShapeBase::destroyThread(int slot)

	Destroy an animation thread, which prevents it from playing.

	:param slot: thread slot to destroy

	:return: true if successful, false if failed

.. cpp:function:: void ShapeBase::dumpMeshVisibility()

	Print a list of visible and hidden meshes in the shape to the console for debugging purposes.

.. cpp:function:: Point3F ShapeBase::getAIRepairPoint()

	Get the position at which the AI should stand to repair things. If the shape defines a node called "AIRepairNode", this method will return the current world position of that node, otherwise "0 0 0".

	:return: the AI repair position 

.. cpp:function:: float ShapeBase::getCameraFov()

	Returns the vertical field of view in degrees for this object if used as a camera.

	:return: ShapeBaseData::cameraDefaultFov

.. cpp:function:: int ShapeBase::getControllingClient()

	Get the client (if any) that controls this object. The controlling client is the one that will send moves to us to act on.

	:return: , or 0 if this object is not controlled by any client. 

.. cpp:function:: int ShapeBase::getControllingObject()

	Get the object (if any) that controls this object.

	:return:  object, or 0 if this object is not controlled by another object. 

.. cpp:function:: float ShapeBase::getDamageFlash()

	Get the damage flash level.

	:return: flash level 

.. cpp:function:: float ShapeBase::getDamageLevel()

	Get the object's current damage level.

	:return: damage level 

.. cpp:function:: float ShapeBase::getDamagePercent()

	Get the object's current damage level as a percentage of maxDamage.

	:return: damageLevel / datablock.maxDamage 

.. cpp:function:: string ShapeBase::getDamageState()

	Get the object's damage state.

	:return: the damage state; one of "Enabled", "Disabled", "Destroyed" 

.. cpp:function:: float ShapeBase::getDefaultCameraFov()

	Returns the default vertical field of view in degrees for this object if used as a camera.

	:return: Default FOV 

.. cpp:function:: float ShapeBase::getEnergyLevel()

	Get the object's current energy level.

	:return: energy level 

.. cpp:function:: float ShapeBase::getEnergyPercent()

	Get the object's current energy level as a percentage of maxEnergy.

	:return: energyLevel / datablock.maxEnergy 

.. cpp:function:: Point3F ShapeBase::getEyePoint()

	Get the position of the 'eye' for this object. If the object model has a node called 'eye', this method will return that node's current world position, otherwise it will return the object's current world position.

	:return: the eye position for this object 

.. cpp:function:: TransformF ShapeBase::getEyeTransform()

	Get the 'eye' transform for this object. If the object model has a node called 'eye', this method will return that node's current transform, otherwise it will return the object's current transform.

	:return: the eye transform for this object 

.. cpp:function:: VectorF ShapeBase::getEyeVector()

	Get the forward direction of the 'eye' for this object. If the object model has a node called 'eye', this method will return that node's current forward direction vector, otherwise it will return the object's current forward direction vector.

	:return: the eye vector for this object 

.. cpp:function:: bool ShapeBase::getImageAltTrigger(int slot)

	Get the alt trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current alt trigger state 

.. cpp:function:: bool ShapeBase::getImageAmmo(int slot)

	Get the ammo state of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current ammo state 

.. cpp:function:: bool ShapeBase::getImageGenericTrigger(int slot, int trigger)

	Get the generic trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to query
	:param trigger: Generic trigger number

	:return: the Image's current generic trigger state 

.. cpp:function:: bool ShapeBase::getImageLoaded(int slot)

	Get the loaded state of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current loaded state 

.. cpp:function:: string ShapeBase::getImageScriptAnimPrefix(int slot)

	Get the script animation prefix of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current script animation prefix 

.. cpp:function:: int ShapeBase::getImageSkinTag(int slot)

	Get the skin tag ID for the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the skinTag value passed to mountImage when the image was mounted 

.. cpp:function:: string ShapeBase::getImageState(int slot)

	Get the name of the current state of the Image in the specified slot.

	:param slot: Image slot to query

	:return: name of the current Image state, or "Error" if slot is invalid 

.. cpp:function:: bool ShapeBase::getImageTarget(int slot)

	Get the target state of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current target state 

.. cpp:function:: bool ShapeBase::getImageTrigger(int slot)

	Get the trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return: the Image's current trigger state 

.. cpp:function:: string ShapeBase::getLookAtPoint(float distance, int typeMask)

	Get the world position this object is looking at. Casts a ray from the eye and returns information about what the ray hits.

	:param distance: maximum distance of the raycast
	:param typeMask: typeMask of objects to include for raycast collision testing

	:return: look-at information as "Object HitX HitY HitZ [Material]" or empty string for no hit

	Example::

		%lookat = %obj.getLookAtPoint();
		echo( "Looking at: " @ getWords( %lookat, 1, 3 ) );

.. cpp:function:: float ShapeBase::getMaxDamage()

	Get the object's maxDamage level.

	:return: datablock.maxDamage 

.. cpp:function:: string ShapeBase::getModelFile()

	Get the model filename used by this shape.

	:return: the shape filename 

.. cpp:function:: int ShapeBase::getMountedImage(int slot)

	Get the Image mounted in the specified slot.

	:param slot: Image slot to query

	:return:  datablock mounted in the slot, or 0 if no Image is mounted there. 

.. cpp:function:: int ShapeBase::getMountSlot(ShapeBaseImageData image)

	Get the first slot the given datablock is mounted to on this object.

	:param image: ShapeBaseImageData datablock to query

	:return: index of the first slot the Image is mounted in, or -1 if the Image is not mounted in any slot on this object. 

.. cpp:function:: Point3F ShapeBase::getMuzzlePoint(int slot)

	Get the muzzle position of the Image mounted in the specified slot. If the Image shape contains a node called 'muzzlePoint', then the muzzle position is the position of that node in world space. If no such node is specified, the slot's mount node is used instead.

	:param slot: Image slot to query

	:return: the muzzle position, or "0 0 0" if the slot is invalid 

.. cpp:function:: VectorF ShapeBase::getMuzzleVector(int slot)

	Get the muzzle vector of the Image mounted in the specified slot. If the Image shape contains a node called 'muzzlePoint', then the muzzle vector is the forward direction vector of that node's transform in world space. If no such node is specified, the slot's mount node is used instead. If the correctMuzzleVector flag (correctMuzzleVectorTP in 3rd person) is set in the Image, the muzzle vector is computed to point at whatever object is right in front of the object's 'eye' node.

	:param slot: Image slot to query

	:return: the muzzle vector, or "0 1 0" if the slot is invalid 

.. cpp:function:: int ShapeBase::getPendingImage(int slot)

	Get the Image that will be mounted next in the specified slot. Calling mountImage when an Image is already mounted does one of two things: This command retrieves the ID of the pending Image (2nd case above).

	:param slot: Image slot to query

	:return:  datablock, or 0 if none. 

.. cpp:function:: float ShapeBase::getRechargeRate()

	Get the current recharge rate.

	:return: the recharge rate (per tick) 

.. cpp:function:: float ShapeBase::getRepairRate()

	Get the per-tick repair amount.

	:return: the current value to be subtracted from damage level each tick 

.. cpp:function:: string ShapeBase::getShapeName()

	Get the name of the shape.

	:return: the name of the shape

.. cpp:function:: string ShapeBase::getSkinName()

	Get the name of the skin applied to this shape.

	:return: the name of the skin

.. cpp:function:: TransformF ShapeBase::getSlotTransform(int slot)

	Get the world transform of the specified mount slot.

	:param slot: Image slot to query

	:return: the mount transform 

.. cpp:function:: int ShapeBase::getTargetCount()

	Get the number of materials in the shape.

	:return: the number of materials in the shape.

.. cpp:function:: string ShapeBase::getTargetName(int index)

	Get the name of the indexed shape material.

	:param index: index of the material to get (valid range is 0 - getTargetCount()-1).

	:return: the name of the indexed material.

.. cpp:function:: VectorF ShapeBase::getVelocity()

	Get the object's current velocity. Reimplemented in Camera .

	:return: the current velocity 

.. cpp:function:: float ShapeBase::getWhiteOut()

	Get the white-out level.

	:return: white-out level 

.. cpp:function:: bool ShapeBase::hasImageState(int slot, string state)

	Check if the given state exists on the mounted Image.

	:param slot: Image slot to query
	:param state: Image state to check for

	:return: true if the Image has the requested state defined. 

.. cpp:function:: bool ShapeBase::isCloaked()

	Check if this object is cloaked.

	:return: true if cloaked, false if not 

.. cpp:function:: bool ShapeBase::isDestroyed()

	Check if the object is in the Destroyed damage state.

	:return: true if damage state is "Destroyed", false if not 

.. cpp:function:: bool ShapeBase::isDisabled()

	Check if the object is in the Disabled or Destroyed damage state.

	:return: true if damage state is not "Enabled", false if it is 

.. cpp:function:: bool ShapeBase::isEnabled()

	Check if the object is in the Enabled damage state.

	:return: true if damage state is "Enabled", false if not 

.. cpp:function:: bool ShapeBase::isHidden()

	Check if the object is hidden.

	:return: true if the object is hidden, false if visible. 

.. cpp:function:: bool ShapeBase::isImageFiring(int slot)

	Check if the current Image state is firing.

	:param slot: Image slot to query

	:return: true if the current Image state in this slot has the 'stateFire' flag set. 

.. cpp:function:: bool ShapeBase::isImageMounted(ShapeBaseImageData image)

	Check if the given datablock is mounted to any slot on this object.

	:param image: ShapeBaseImageData datablock to query

	:return: true if the Image is mounted to any slot, false otherwise. 

.. cpp:function:: bool ShapeBase::mountImage(ShapeBaseImageData image, int slot, bool loaded, string skinTag)

	Mount a new Image.

	:param image: the Image to mount
	:param slot: Image slot to mount into (valid range is 0 - 3)
	:param loaded: initial loaded state for the Image
	:param skinTag: tagged string to reskin the mounted Image

	:return: true if successful, false if failed

	Example::

		%player.mountImage( PistolImage, 1 );
		%player.mountImage( CrossbowImage, 0, false );
		%player.mountImage( RocketLauncherImage, 0, true, blue );

.. cpp:function:: bool ShapeBase::pauseThread(int slot)

	Pause an animation thread. If restarted using playThread, the animation will resume from the paused position.

	:param slot: thread slot to stop

	:return: true if successful, false if failed

.. cpp:function:: bool ShapeBase::playAudio(int slot, SFXTrack track)

	Attach a sound to this shape and start playing it.

	:param slot: Audio slot index for the sound (valid range is 0 - 3)
	:param track: SFXTrack to play

	:return: true if the sound was attached successfully, false if failed

.. cpp:function:: bool ShapeBase::playThread(int slot, string name)

	Start a new animation thread, or restart one that has been paused or stopped.

	:param slot: thread slot to play. Valid range is 0 - 3)
	:param name: name of the animation sequence to play in this slot. If not specified, the paused or stopped thread in this slot will be resumed.

	:return: true if successful, false if failed

	Example::

		%obj.playThread( 0, "ambient" );      // Play the ambient sequence in slot 0
		%obj.setThreadTimeScale( 0, 0.5 );    // Play at half-speed
		%obj.pauseThread( 0 );                // Pause the sequence
		%obj.playThread( 0 );                 // Resume playback
		%obj.playThread( 0, "spin" );         // Replace the sequence in slot 0

.. cpp:function:: void ShapeBase::setAllMeshesHidden(bool hide)

	Set the hidden state on all the shape meshes. This allows you to hide all meshes in the shape, for example, and then only enable a few.

	:param hide: new hidden state for all meshes

.. cpp:function:: void ShapeBase::setCameraFov(float fov)

	Set the vertical field of view in degrees for this object if used as a camera.

	:param fov: new FOV value

.. cpp:function:: void ShapeBase::setCloaked(bool cloak)

	Set the cloaked state of this object. When an object is cloaked it is not rendered.

	:param cloak: true to cloak the object, false to uncloak

.. cpp:function:: void ShapeBase::setDamageFlash(float level)

	Set the damage flash level. Damage flash may be used as a postfx effect to flash the screen when the client is damaged.

	:param level: flash level (0-1)

.. cpp:function:: void ShapeBase::setDamageLevel(float level)

	Set the object's current damage level.

	:param level: new damage level

.. cpp:function:: bool ShapeBase::setDamageState(string state)

	Set the object's damage state.

	:param state: should be one of "Enabled", "Disabled", "Destroyed"

	:return: true if successful, false if failed 

.. cpp:function:: void ShapeBase::setDamageVector(Point3F vec)

	Set the damage direction vector. Currently this is only used to initialise the explosion if this object is blown up.

	:param vec: damage direction vector

	Example::

		%obj.setDamageVector( "0 0 1" );

.. cpp:function:: void ShapeBase::setEnergyLevel(float level)

	Set this object's current energy level.

	:param level: new energy level

.. cpp:function:: void ShapeBase::setHidden(bool show)

	Add or remove this object from the scene. When removed from the scene, the object will not be processed or rendered. Reimplemented from SimObject .

	:param show: False to hide the object, true to re-show it

.. cpp:function:: bool ShapeBase::setImageAltTrigger(int slot, bool state)

	Set the alt trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param state: new alt trigger state for the Image

	:return: the Image's new alt trigger state 

.. cpp:function:: bool ShapeBase::setImageAmmo(int slot, bool state)

	Set the ammo state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param state: new ammo state for the Image

	:return: the Image's new ammo state 

.. cpp:function:: int ShapeBase::setImageGenericTrigger(int slot, int trigger, bool state)

	Set the generic trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param trigger: Generic trigger number
	:param state: new generic trigger state for the Image

	:return: the Image's new generic trigger state or -1 if there was a problem. 

.. cpp:function:: bool ShapeBase::setImageLoaded(int slot, bool state)

	Set the loaded state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param state: new loaded state for the Image

	:return: the Image's new loaded state 

.. cpp:function:: void ShapeBase::setImageScriptAnimPrefix(int slot, string prefix)

	Set the script animation prefix for the Image mounted in the specified slot. This is used to further modify the prefix used when deciding which animation sequence to play while this image is mounted.

	:param slot: Image slot to modify
	:param prefix: The prefix applied to the image

.. cpp:function:: bool ShapeBase::setImageTarget(int slot, bool state)

	Set the target state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param state: new target state for the Image

	:return: the Image's new target state 

.. cpp:function:: bool ShapeBase::setImageTrigger(int slot, bool state)

	Set the trigger state of the Image mounted in the specified slot.

	:param slot: Image slot to modify
	:param state: new trigger state for the Image

	:return: the Image's new trigger state 

.. cpp:function:: void ShapeBase::setInvincibleMode(float time, float speed)

	Setup the invincible effect. This effect is used for HUD feedback to the user that they are invincible.

	:param time: duration in seconds for the invincible effect
	:param speed: speed at which the invincible effect progresses

.. cpp:function:: void ShapeBase::setMeshHidden(string name, bool hide)

	Set the hidden state on the named shape mesh.

	:param name: name of the mesh to hide/show
	:param hide: new hidden state for the mesh

.. cpp:function:: void ShapeBase::setRechargeRate(float rate)

	Set the recharge rate. The recharge rate is added to the object's current energy level each tick, up to the maxEnergy level set in the ShapeBaseData datablock.

	:param rate: the recharge rate (per tick)

.. cpp:function:: void ShapeBase::setRepairRate(float rate)

	Set amount to repair damage by each tick. Note that this value is separate to the repairRate field in ShapeBaseData . This value will be subtracted from the damage level each tick, whereas the ShapeBaseData field limits how much of the applyRepair value is subtracted each tick. Both repair types can be active at the same time.

	:param rate: value to subtract from damage level each tick (must be > 0)

.. cpp:function:: void ShapeBase::setShapeName(string name)

	Set the name of this shape.

	:param name: new name for the shape

.. cpp:function:: void ShapeBase::setSkinName(string name)

	Apply a new skin to this shape. 'Skinning' the shape effectively renames the material targets, allowing different materials to be used on different instances of the same model.

	:param name: name of the skin to apply

.. cpp:function:: bool ShapeBase::setThreadDir(int slot, bool fwd)

	Set the playback direction of an animation thread.

	:param slot: thread slot to modify
	:param fwd: true to play the animation forwards, false to play backwards

	:return: true if successful, false if failed

.. cpp:function:: bool ShapeBase::setThreadPosition(int slot, float pos)

	Set the position within an animation thread.

	:param slot: thread slot to modify
	:param pos: position within thread

	:return: true if successful, false if failed

.. cpp:function:: bool ShapeBase::setThreadTimeScale(int slot, float scale)

	Set the playback time scale of an animation thread.

	:param slot: thread slot to modify
	:param scale: new thread time scale (1=normal speed, 0.5=half speed etc)

	:return: true if successful, false if failed

.. cpp:function:: bool ShapeBase::setVelocity(Point3F vel)

	Set the object's velocity.

	:param vel: new velocity for the object

	:return: true 

.. cpp:function:: void ShapeBase::setWhiteOut(float level)

	Set the white-out level. White-out may be used as a postfx effect to brighten the screen in response to a game event.

	:param level: flash level (0-1)

.. cpp:function:: void ShapeBase::startFade(int time, int delay, bool fadeOut)

	Fade the object in or out without removing it from the scene. A faded out object is still in the scene and can still be collided with, so if you want to disable collisions for this shape after it fades out use setHidden to temporarily remove this shape from the scene.

	:param time: duration of the fade effect in ms
	:param delay: delay in ms before the fade effect begins
	:param fadeOut: true to fade-out to invisible, false to fade-in to full visibility

.. cpp:function:: bool ShapeBase::stopAudio(int slot)

	Stop a sound started with playAudio.

	:param slot: audio slot index (started with playAudio)

	:return: true if the sound was stopped successfully, false if failed

.. cpp:function:: bool ShapeBase::stopThread(int slot)

	Stop an animation thread. If restarted using playThread, the animation will start from the beginning again.

	:param slot: thread slot to stop

	:return: true if successful, false if failed

.. cpp:function:: bool ShapeBase::unmountImage(int slot)

	Unmount the mounted Image in the specified slot.

	:param slot: Image slot to unmount

	:return: true if successful, false if failed

.. cpp:function:: float ShapeBase::validateCameraFov(float fov)

	Called on the server when the client has requested a FOV change. When the client requests that its field of view should be changed (because they want to use a sniper scope, for example) this new FOV needs to be validated by the server. This method is called if it exists (it is optional) to validate the requested FOV, and modify it if necessary. This could be as simple as checking that the FOV falls within a correct range, to making sure that the FOV matches the capabilities of the current weapon. Following this method, ShapeBase ensures that the given FOV still falls within the datablock's cameraMinFov and cameraMaxFov. If that is good enough for your purposes, then you do not need to define the validateCameraFov() callback for your ShapeBase .

	:param fov: The FOV that has been requested by the client.

	:return: The FOV as validated by the server.

Fields
------


.. cpp:member:: bool  ShapeBase::isAIControlled

	Is this object AI controlled. If True then this object is considered AI controlled and not player controlled.

.. cpp:member:: string  ShapeBase::skin

	The skin applied to the shape. 'Skinning' the shape effectively renames the material targets, allowing different materials to be used on different instances of the same model. Using getSkinName() and setSkinName() is equivalent to reading and writing the skin field directly. Any material targets that start with the old skin name have that part of the name replaced with the new skin name. The initial old skin name is "base". For example, if a new skin of "blue" was applied to a model that had material targets base_body and face , the new targets would be blue_body and face . Note that face was not renamed since it did not start with the old skin name of "base". To support models that do not use the default "base" naming convention, you can also specify the part of the name to replace in the skin field itself. For example, if a model had a material target called shapemat , we could apply a new skin "shape=blue", and the material target would be renamed to bluemat (note "shape" has been replaced with "blue"). Multiple skin updates can also be applied at the same time by separating them with a semicolon. For example: "base=blue;face=happy_face". Material targets are only renamed if an existing Material maps to that name, or if there is a diffuse texture in the model folder with the same name as the new target.
