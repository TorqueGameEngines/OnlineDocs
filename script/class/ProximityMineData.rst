ProximityMineData
=================

.

Inherit:
	:doc:`ItemData`

Description
-----------

Stores common properties for a ProximityMine.


Methods
-------


.. cpp:function:: void ProximityMineData::onExplode(ProximityMine obj, Point3F pos)

	Callback invoked when a ProximityMine is about to explode.

	:param obj: The ProximityMine object
	:param pos: The position of the mine explosion

.. cpp:function:: void ProximityMineData::onTriggered(ProximityMine obj, SceneObject target)

	Callback invoked when an object triggers the ProximityMine .

	:param obj: The ProximityMine object
	:param target: The object that triggered the mine

Fields
------


.. cpp:member:: float  ProximityMineData::armingDelay

	Delay (in seconds) from when the mine is placed to when it becomes active.

.. cpp:member:: SFXTrack ProximityMineData::armingSound

	Sound to play when the mine is armed (starts at the same time as the armed sequence if defined).

.. cpp:member:: float  ProximityMineData::autoTriggerDelay

	Delay (in seconds) from arming until the mine automatically triggers and explodes, even if no object has entered the trigger area. Set to 0 to disable.

.. cpp:member:: float  ProximityMineData::explosionOffset

	Offset from the mine's origin where the explosion emanates from.Sometimes a thrown mine may be slightly sunk into the ground. This can be just enough to cause the explosion to occur under the ground, especially on flat ground, which can end up blocking the explosion. This offset along the mine's 'up' normal allows you to raise the explosion origin to a better height.

.. cpp:member:: float  ProximityMineData::triggerDelay

	Delay (in seconds) from when the mine is triggered until it explodes.

.. cpp:member:: bool  ProximityMineData::triggerOnOwner

	Controls whether the mine can be triggered by the object that owns it. For example, a player could deploy mines that are only dangerous to other players and not himself.

.. cpp:member:: float  ProximityMineData::triggerRadius

	Distance at which an activated mine will detect other objects and explode.

.. cpp:member:: SFXTrack ProximityMineData::triggerSound

	Sound to play when the mine is triggered (starts at the same time as the triggered sequence if defined).

.. cpp:member:: float  ProximityMineData::triggerSpeed

	Speed above which moving objects within the trigger radius will trigger the mine.
