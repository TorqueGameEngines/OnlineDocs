Trigger
=======

.

Inherit:
	:doc:`GameBase`

Description
-----------

A Trigger is a volume of space that initiates script callbacks when objects pass through the Trigger.

TriggerData provides the callbacks for the Trigger when an object enters, stays inside or leaves the Trigger's volume.


Methods
-------


.. cpp:function:: int Trigger::getNumObjects()

	Get the number of objects that are within the Trigger's bounds.

.. cpp:function:: int Trigger::getObject(int index)

	Retrieve the requested object that is within the Trigger's bounds.

	:param index: Index of the object to get (range is 0 to getNumObjects()-1)

	:return: The SimObjectID of the object, or -1 if the requested index is invalid. 

.. cpp:function:: void Trigger::onAdd(int objectId)

	Called when the Trigger is being created.

	:param objectId: the object id of the Trigger being created

.. cpp:function:: void Trigger::onRemove(int objectId)

	Called just before the Trigger is deleted.

	:param objectId: the object id of the Trigger being deleted

Fields
------


.. cpp:member:: string  Trigger::enterCommand

	The command to execute when an object enters this trigger. Object id stored in %obj. Maximum 1023 characters.

.. cpp:member:: string  Trigger::leaveCommand

	The command to execute when an object leaves this trigger. Object id stored in %obj. Maximum 1023 characters.

.. cpp:member:: floatList  Trigger::polyhedron

	Defines a non-rectangular area for the trigger. Rather than the standard rectangular bounds, this optional parameter defines a quadrilateral trigger area. The quadrilateral is defined as a corner point followed by three vectors representing the edges extending from the corner.

.. cpp:member:: string  Trigger::tickCommand

	The command to execute while an object is inside this trigger. Maximum 1023 characters.
