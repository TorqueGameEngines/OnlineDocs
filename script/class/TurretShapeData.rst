TurretShapeData
===============

object.

Inherit:
	:doc:`ItemData`

Description
-----------

Defines properties for a TurretShape object.


Methods
-------


.. cpp:function:: void TurretShapeData::onMountObject(TurretShape turret, SceneObject obj, int node)

	Informs the TurretShapeData object that a player is mounting it.

	:param turret: The TurretShape object.
	:param obj: The player that is mounting.
	:param node: The node the player is mounting to.

.. cpp:function:: void TurretShapeData::onStickyCollision(TurretShape obj)

	Informs the TurretData object that it is now sticking to another object. This callback is only called if the TurretData::sticky property for this Turret is true.

	:param obj: The Turret object that is colliding.

.. cpp:function:: void TurretShapeData::onUnmountObject(TurretShape turret, SceneObject obj)

	Informs the TurretShapeData object that a player is unmounting it.

	:param turret: The TurretShape object.
	:param obj: The player that is unmounting.

Fields
------


.. cpp:member:: float  TurretShapeData::cameraOffset

	Vertical (Z axis) height of the camera above the turret.

.. cpp:member:: float  TurretShapeData::headingRate

	Degrees per second rotation. A value of 0 means no rotation is allowed. A value less than 0 means the rotation is instantaneous.

.. cpp:member:: float  TurretShapeData::maxHeading

	Maximum number of degrees to rotate from center. A value of 180 or more degrees indicates the turret may rotate completely around.

.. cpp:member:: float  TurretShapeData::maxPitch

	Maximum number of degrees to rotate up from straight ahead.

.. cpp:member:: float  TurretShapeData::minPitch

	Minimum number of degrees to rotate down from straight ahead.

.. cpp:member:: float  TurretShapeData::pitchRate

	Degrees per second rotation. A value of 0 means no rotation is allowed. A value less than 0 means the rotation is instantaneous.

.. cpp:member:: bool  TurretShapeData::startLoaded

	Does the turret's mounted weapon(s) start in a loaded state. True indicates that all mounted weapons start in a loaded state.

.. cpp:member:: TurretShapeFireLinkType TurretShapeData::weaponLinkType

	Set how the mounted weapons are linked and triggered. 
	
	* FireTogether: All weapons fire under trigger 0.
	* GroupedFire: Weapon mounts 0,2 fire under trigger 0, mounts 1,3 fire under trigger 1.
	* IndividualFire: Each weapon mount fires under its own trigger 0-3.

.. cpp:member:: bool  TurretShapeData::zRotOnly

	Should the turret allow only z rotations. True indicates that the turret may only be rotated on its z axis, just like the Item class. This keeps the turret always upright regardless of the surface it lands on.
