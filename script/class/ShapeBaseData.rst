ShapeBaseData
=============

object.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines properties for a ShapeBase object.


Methods
-------


.. cpp:function:: bool ShapeBaseData::checkDeployPos(TransformF txfm)

	Check if there is the space at the given transform is free to spawn into. The shape's bounding box volume is used to check for collisions at the given world transform. Only interior and static objects are checked for collision.

	:param txfm: Deploy transform to check

	:return: True if the space is free, false if there is already something in the way. 

.. cpp:function:: TransformF ShapeBaseData::getDeployTransform(Point3F pos, Point3F normal)

	Helper method to get a transform from a position and vector (suitable for use with setTransform).

	:param pos: Desired transform position
	:param normal: Vector of desired direction

	:return: The deploy transform 

.. cpp:function:: void ShapeBaseData::onCollision(ShapeBase obj, SceneObject collObj, VectorF vec, float len)

	Called when we collide with another object.

	:param obj: The ShapeBase object
	:param collObj: The object we collided with
	:param vec: Collision impact vector
	:param len: Length of the impact vector

.. cpp:function:: void ShapeBaseData::onDamage(ShapeBase obj, float delta)

	Called when the object is damaged.

	:param obj: The ShapeBase object
	:param obj: The ShapeBase object
	:param delta: The amount of damage received.

.. cpp:function:: void ShapeBaseData::onDestroyed(ShapeBase obj, string lastState)

	Called when the object damage state changes to Destroyed.

	:param obj: The ShapeBase object
	:param lastState: The previous damage state

.. cpp:function:: void ShapeBaseData::onDisabled(ShapeBase obj, string lastState)

	Called when the object damage state changes to Disabled.

	:param obj: The ShapeBase object
	:param lastState: The previous damage state

.. cpp:function:: void ShapeBaseData::onEnabled(ShapeBase obj, string lastState)

	Called when the object damage state changes to Enabled.

	:param obj: The ShapeBase object
	:param lastState: The previous damage state

.. cpp:function:: void ShapeBaseData::onEndSequence(ShapeBase obj, int slot)

	Called when a thread playing a non-cyclic sequence reaches the end of the sequence.

	:param obj: The ShapeBase object
	:param slot: Thread slot that finished playing

.. cpp:function:: void ShapeBaseData::onForceUncloak(ShapeBase obj, string reason)

	Called when the object is forced to uncloak.

	:param obj: The ShapeBase object
	:param reason: String describing why the object was uncloaked

.. cpp:function:: void ShapeBaseData::onImpact(ShapeBase obj, SceneObject collObj, VectorF vec, float len)

	Called when we collide with another object beyond some impact speed. The Player class makes use of this callback when a collision speed is more than PlayerData::minImpactSpeed .

	:param obj: The ShapeBase object
	:param collObj: The object we collided with
	:param vec: Collision impact vector
	:param len: Length of the impact vector

.. cpp:function:: void ShapeBaseData::onTrigger(ShapeBase obj, int index, bool state)

	Called when a move trigger input changes state.

	:param obj: The ShapeBase object
	:param index: Index of the trigger that changed
	:param state: New state of the trigger

Fields
------


.. cpp:member:: bool  ShapeBaseData::cameraCanBank

	If the derrived class supports it, allow the camera to bank.

.. cpp:member:: float  ShapeBaseData::cameraDefaultFov

	The default camera vertical FOV in degrees.

.. cpp:member:: float  ShapeBaseData::cameraMaxDist

	The maximum distance from the camera to the object. Used when computing a custom camera transform for this object.

.. cpp:member:: float  ShapeBaseData::cameraMaxFov

	The maximum camera vertical FOV allowed in degrees.

.. cpp:member:: float  ShapeBaseData::cameraMinDist

	The minimum distance from the camera to the object. Used when computing a custom camera transform for this object.

.. cpp:member:: float  ShapeBaseData::cameraMinFov

	The minimum camera vertical FOV allowed in degrees.

.. cpp:member:: bool  ShapeBaseData::computeCRC

	If true, verify that the CRC of the client's shape model matches the server's CRC for the shape model when loaded by the client.

.. cpp:member:: string  ShapeBaseData::cubeReflectorDesc

	References a ReflectorDesc datablock that defines performance and quality properties for dynamic reflections.

.. cpp:member:: DebrisData ShapeBaseData::Debris

	Debris to generate when this shape is blown up.

.. cpp:member:: filename  ShapeBaseData::debrisShapeName

	The DTS or DAE model to use for auto-generated breakups.

.. cpp:member:: float  ShapeBaseData::density

	Shape density. Used when computing buoyancy when in water.

.. cpp:member:: float  ShapeBaseData::destroyedLevel

	Damage level above which the object is destroyed. When the damage level increases above this value, the object damage state is set to "Destroyed".

.. cpp:member:: float  ShapeBaseData::disabledLevel

	Damage level above which the object is disabled. Currently unused.

.. cpp:member:: float  ShapeBaseData::drag

	Drag factor. Reduces velocity of moving objects.

.. cpp:member:: ExplosionData ShapeBaseData::Explosion

	Explosion to generate when this shape is blown up.

.. cpp:member:: bool  ShapeBaseData::firstPersonOnly

	Flag controlling whether the view from this object is first person only.

.. cpp:member:: bool  ShapeBaseData::inheritEnergyFromMount

	Flag controlling whether to manage our own energy level, or to use the energy level of the object we are mounted to.

.. cpp:member:: bool  ShapeBaseData::isInvincible

	Invincible flag; when invincible, the object cannot be damaged or repaired.

.. cpp:member:: float  ShapeBaseData::mass

	Shape mass. Used in simulation of moving objects.

.. cpp:member:: float  ShapeBaseData::maxDamage

	Maximum damage level for this object.

.. cpp:member:: float  ShapeBaseData::maxEnergy

	Maximum energy level for this object.

.. cpp:member:: bool  ShapeBaseData::mountedImagesBank

	Do mounted images bank along with the camera?

.. cpp:member:: bool  ShapeBaseData::observeThroughObject

	Observe this object through its camera transform and default fov. If true, when this object is the camera it can provide a custom camera transform and FOV (instead of the default eye transform).

.. cpp:member:: bool  ShapeBaseData::renderWhenDestroyed

	Whether to render the shape when it is in the "Destroyed" damage state.

.. cpp:member:: float  ShapeBaseData::repairRate

	Rate at which damage is repaired in damage units/tick. This value is subtracted from the damage level until it reaches 0.

.. cpp:member:: bool  ShapeBaseData::shadowEnable

	Enable shadows for this shape (currently unused, shadows are always enabled).

.. cpp:member:: float  ShapeBaseData::shadowMaxVisibleDistance

	Maximum distance at which shadow is visible (currently unused).

.. cpp:member:: float  ShapeBaseData::shadowProjectionDistance

	Maximum height above ground to project shadow. If the object is higher than this no shadow will be rendered.

.. cpp:member:: int  ShapeBaseData::shadowSize

	Size of the projected shadow texture (must be power of 2).

.. cpp:member:: float  ShapeBaseData::shadowSphereAdjust

	Scalar applied to the radius of spot shadows (initial radius is based on the shape bounds but can be adjusted with this field).

.. cpp:member:: filename  ShapeBaseData::shapeFile

	The DTS or DAE model to use for this object.

.. cpp:member:: ExplosionData ShapeBaseData::underwaterExplosion

	Explosion to generate when this shape is blown up underwater.

.. cpp:member:: bool  ShapeBaseData::useEyePoint

	Flag controlling whether the client uses this object's eye point to view from.
