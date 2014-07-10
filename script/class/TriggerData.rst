TriggerData
===========

objects.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines shared properties for Trigger objects.

The primary focus of the TriggerData datablock is the callbacks it provides when an object is within or leaves the Trigger bounds.


Methods
-------


.. cpp:function:: void TriggerData::onEnterTrigger(Trigger trigger, GameBase obj)

	Called when an object enters the volume of the Trigger instance using this TriggerData .

	:param trigger: the Trigger instance whose volume the object entered
	:param obj: the object that entered the volume of the Trigger instance

.. cpp:function:: void TriggerData::onLeaveTrigger(Trigger trigger, GameBase obj)

	Called when an object leaves the volume of the Trigger instance using this TriggerData .

	:param trigger: the Trigger instance whose volume the object left
	:param obj: the object that left the volume of the Trigger instance

.. cpp:function:: void TriggerData::onTickTrigger(Trigger trigger)

	Called every tickPeriodMS number of milliseconds (as specified in the TriggerData ) whenever one or more objects are inside the volume of the trigger. The Trigger has methods to retrieve the objects that are within the Trigger's bounds if you want to do something with them in this callback.

	:param trigger: the Trigger instance whose volume the object is inside

Fields
------


.. cpp:member:: bool  TriggerData::clientSide

	Forces Trigger callbacks to only be called on clients.

.. cpp:member:: int  TriggerData::tickPeriodMS

	Time in milliseconds between calls to onTickTrigger() while at least one object is within a Trigger's bounds.
