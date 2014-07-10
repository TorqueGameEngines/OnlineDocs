AITurretShapeData
=================

object.

Inherit:
	:doc:`TurretShapeData`

Description
-----------

Defines properties for an AITurretShape object.


Fields
------


.. cpp:member:: float  AITurretShapeData::maxScanDistance

	Maximum distance to scan. When combined with maxScanHeading and maxScanPitch this forms a 3D scanning wedge used to initially locate a target.

.. cpp:member:: float  AITurretShapeData::maxScanHeading

	Maximum number of degrees to scan left and right.

.. cpp:member:: float  AITurretShapeData::maxScanPitch

	Maximum number of degrees to scan up and down.

.. cpp:member:: float  AITurretShapeData::maxWeaponRange

	Maximum distance that the weapon will fire upon a target.

.. cpp:member:: int  AITurretShapeData::scanTickFrequency

	How often should we perform a full scan when looking for a target. Expressed as the number of ticks between full scans, but no less than 1.

.. cpp:member:: int  AITurretShapeData::scanTickFrequencyVariance

	Random amount that should be added to the scan tick frequency each scan period. Expressed as the number of ticks to randomly add, but no less than zero.

.. cpp:member:: bool  AITurretShapeData::stateDirection [31]

	Direction of the animation to play in this state. True is forward, false is backward.

.. cpp:member:: bool  AITurretShapeData::stateFire [31]

	The first state with this set to true is the state entered by the client when it receives the 'fire' event.

.. cpp:member:: caseString  AITurretShapeData::stateName [31]

	Name of this state.

.. cpp:member:: bool  AITurretShapeData::stateScaleAnimation [31]

	If true, the timeScale of the stateSequence animation will be adjusted such that the sequence plays for stateTimeoutValue seconds.

.. cpp:member:: bool  AITurretShapeData::stateScan [31]

	Indicates the turret should perform a continuous scan looking for targets.

.. cpp:member:: caseString  AITurretShapeData::stateScript [31]

	Method to execute on entering this state. Scoped to AITurretShapeData .

.. cpp:member:: string  AITurretShapeData::stateSequence [31]

	Name of the sequence to play on entry to this state.

.. cpp:member:: float  AITurretShapeData::stateTimeoutValue [31]

	Time in seconds to wait before transitioning to stateTransitionOnTimeout.

.. cpp:member:: string  AITurretShapeData::stateTransitionOnActivated [31]

	Name of the state to transition to when the turret goes from deactivated to activated.

.. cpp:member:: string  AITurretShapeData::stateTransitionOnAtRest [31]

	Name of the state to transition to when the turret is at rest (static).

.. cpp:member:: string  AITurretShapeData::stateTransitionOnDeactivated [31]

	Name of the state to transition to when the turret goes from activated to deactivated.

.. cpp:member:: string  AITurretShapeData::stateTransitionOnNoTarget [31]

	Name of the state to transition to when the turret loses a target.

.. cpp:member:: string  AITurretShapeData::stateTransitionOnNotAtRest [31]

	Name of the state to transition to when the turret is not at rest (not static).

.. cpp:member:: string  AITurretShapeData::stateTransitionOnTarget [31]

	Name of the state to transition to when the turret gains a target.

.. cpp:member:: string  AITurretShapeData::stateTransitionOnTimeout [31]

	Name of the state to transition to when we have been in this state for stateTimeoutValue seconds.

.. cpp:member:: bool  AITurretShapeData::stateWaitForTimeout [31]

	If false, this state ignores stateTimeoutValue and transitions immediately if other transition conditions are met.

.. cpp:member:: float  AITurretShapeData::trackLostTargetTime

	How long after the turret has lost the target should it still track it. Expressed in seconds.

.. cpp:member:: float  AITurretShapeData::weaponLeadVelocity

	Velocity used to lead target. If value lt = 0, don't lead target.
