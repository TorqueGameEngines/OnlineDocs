Objects
=======

Objects which can be controlled or directly interact with a user, such as Player, Projectile, Item, etc. Does not include vehicles as they have their own section. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/AIPlayer
	class/AITurretShape
	class/AITurretShapeData
	class/GameBase
	class/GameBaseData
	class/Item
	class/ItemData
	class/Player
	class/PlayerData
	class/Projectile
	class/ProjectileData
	class/ProximityMine
	class/ProximityMineData
	class/SceneObject
	class/ShapeBase
	class/ShapeBaseData
	class/ShapeBaseImageData
	class/SpawnSphere
	class/StaticShape
	class/StaticShapeData
	class/Trigger
	class/TriggerData
	class/TSShapeConstructor
	class/TSStatic
	class/TurretShape
	class/TurretShapeData

Enumeration
-----------

.. cpp:member:: enum  ItemLightType

	The type of light the Item has.

	:param NoLight: The item has no light attached.
	:param ConstantLight: The item has a constantly emitting light attached.
	:param PulsingLight: The item has a pulsing light attached.

.. cpp:member:: enum  PlayerPose

	The pose of the Player .

	:param Stand: Standard movement pose.
	:param Sprint: Sprinting pose.
	:param Crouch: Crouch pose.
	:param Prone: Prone pose.
	:param Swim: Swimming pose.

.. cpp:member:: enum  ShapeBaseImageLightType

	The type of light to attach to this ShapeBaseImage.

	:param NoLight: No light is attached.
	:param ConstantLight: A constant emitting light is attached.
	:param SpotLight: A spotlight is attached.
	:param PulsingLight: A pusling light is attached.
	:param WeaponFireLight: Light emits when the weapon is fired, then dissipates.

.. cpp:member:: enum  ShapeBaseImageLoadedState

	The loaded state of this ShapeBaseImage.

	:param Ignore: Ignore the loaded state.
	:param Loaded: ShapeBaseImage is loaded.
	:param Empty: ShapeBaseImage is not loaded.

.. cpp:member:: enum  ShapeBaseImageRecoilState

	What kind of recoil this ShapeBaseImage should emit when fired.

	:param NoRecoil: No recoil occurs.
	:param LightRecoil: A light recoil occurs.
	:param MediumRecoil: A medium recoil occurs.
	:param HeavyRecoil: A heavy recoil occurs.

.. cpp:member:: enum  ShapeBaseImageSpinState

	How the spin animation should be played.

	:param Ignore: No changes to the spin sequence.
	:param Stop: Stops the spin sequence at its current position.
	:param SpinUp: Increase spin sequence timeScale from 0 (on state entry) to 1 (after stateTimeoutValue seconds).
	:param SpinDown: Decrease spin sequence timeScale from 1 (on state entry) to 0 (after stateTimeoutValue seconds).
	:param FullSpeed: Resume the spin sequence playback at its current position with timeScale = 1.

.. cpp:member:: enum  TSMeshType

	Type of mesh data available in a shape.

	:param None: No mesh data.
	:param Bounds: Bounding box of the shape.
	:param Mesh: Specifically desingated "collision" meshes.
	:param Mesh: Rendered mesh polygons.

.. cpp:member:: enum  TurretShapeFireLinkType

	How the weapons are linked to triggers for this TurretShape .

	:param FireTogether: All weapons fire under trigger 0.
	:param GroupedFire: Weapon mounts 0,2 fire under trigger 0, mounts 1,3 fire under trigger 1.
	:param IndividualFire: Each weapon mount fires under its own trigger 0-3.

Variables
---------

.. cpp:member:: float $SB::CloakSpeed

	Time to cloak, in seconds.

.. cpp:member:: float $SB::DFDec

	Speed to reduce the damage flash effect per tick.

.. cpp:member:: float $SB::FullCorrectionDistance

	Distance at which a weapon's muzzle vector is fully corrected to match where the player is looking. When a weapon image has correctMuzzleVector set and the Player is in 1st person, the muzzle vector from the weapon is modified to match where the player is looking. Beyond the FullCorrectionDistance the muzzle vector is always corrected. Between FullCorrectionDistance and the player, the weapon's muzzle vector is adjusted so that the closer the aim point is to the player, the closer the muzzle vector is to the true (non-corrected) one.

.. cpp:member:: bool  Trigger::renderTriggers  [static, inherited]

	Forces all Trigger's to render. Used by the Tools and debug render modes.

.. cpp:member:: float $SB::WODec

	Speed to reduce the whiteout effect per tick.
