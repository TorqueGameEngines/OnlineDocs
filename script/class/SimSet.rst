SimSet
======

A collection of SimObjects.

Inherit:
	:doc:`SimObject`

Description
-----------

It is often necessary to keep track of an arbitrary set of SimObjects. For instance, Torque's networking code needs to not only keep track of the set of objects which need to be ghosted, but also the set of objects which must always be ghosted. It does this by working with two sets. The first of these is the RootGroup (which is actually a SimGroup) and the second is the GhostAlwaysSet, which contains objects which must always be ghosted to the client.

Some general notes on SimSets:

* Membership is not exclusive. A SimObject may be a member of multiple SimSets.
* A SimSet does not destroy subobjects when it is destroyed.
* A SimSet may hold an arbitrary number of objects.

Methods
-------

.. cpp:function:: bool SimSet::acceptsAsChild(SimObject obj)

	Test whether the given object may be added to the set.

	:param obj: The object to test for potential membership.

	:return: True if the object may be added to the set, false otherwise. 

.. cpp:function:: void SimSet::add(SimObject objects, ...)

	Add the given objects to the set.

	:param objects: The objects to add to the set.

.. cpp:function:: void SimSet::bringToFront(SimObject obj)

	Make the given object the first object in the set.

	:param obj: The object to bring to the frontmost position. Must be contained in the set.

.. cpp:function:: void SimSet::callOnChildren(string method, string args, ...)

	Call a method on all objects contained in the set.

	:param method: The name of the method to call.
	:param args: The arguments to the method.

.. cpp:function:: void SimSet::callOnChildrenNoRecurse(string method, string args, ...)

	Call a method on all objects contained in the set.

	:param method: The name of the method to call.
	:param args: The arguments to the method.

.. cpp:function:: void SimSet::clear()

	Remove all objects from the set. Reimplemented in GuiPopUpMenuCtrlEx .

.. cpp:function:: void SimSet::deleteAllObjects()

	Delete all objects in the set.

.. cpp:function:: SimObject  SimSet::findObjectByInternalName(string internalName, bool searchChildren)

	Find an object in the set by its internal name.

	:param internalName: The internal name of the object to look for.
	:param searchChildren: If true, SimSets contained in the set will be recursively searched for the object.

	:return: The object with the given internal name or 0 if no match was found. 

.. cpp:function:: int SimSet::getCount()

	Get the number of objects contained in the set.

	:return: The number of objects contained in the set. 

.. cpp:function:: int SimSet::getFullCount()

	Get the number of direct and indirect child objects contained in the set.

	:return: The number of objects contained in the set as well as in other sets contained directly or indirectly in the set. 

.. cpp:function:: SimObject  SimSet::getObject(int index)

	Get the object at the given index.

	:param index: The object index.

	:return: The object at the given index or -1 if index is out of range. 

.. cpp:function:: int SimSet::getObjectIndex(SimObject obj)

	Return the index of the given object in this set.

	:param obj: The object for which to return the index. Must be contained in the set.

	:return: The index of the object or -1 if the object is not contained in the set. 

.. cpp:function:: SimObject  SimSet::getRandom()

	Return a random object from the set.

	:return: A randomly selected object from the set or -1 if the set is empty. 

.. cpp:function:: bool SimSet::isMember(SimObject obj)

	Test whether the given object belongs to the set.

	:param obj: The object.

	:return: True if the object is contained in the set; false otherwise. 

.. cpp:function:: void SimSet::listObjects()

	Dump a list of all objects contained in the set to the console.

.. cpp:function:: void SimSet::onObjectAdded(SimObject object)

	Called when an object is added to the set.

	:param object: The object that was added.

.. cpp:function:: void SimSet::onObjectRemoved(SimObject object)

	Called when an object is removed from the set.

	:param object: The object that was removed.

.. cpp:function:: void SimSet::pushToBack(SimObject obj)

	Make the given object the last object in the set.

	:param obj: The object to bring to the last position. Must be contained in the set.

.. cpp:function:: void SimSet::remove(SimObject objects, ...)

	Remove the given objects from the set.

	:param objects: The objects to remove from the set.

.. cpp:function:: void SimSet::reorderChild(SimObject child1, SimObject child2)

	Make sure child1 is ordered right before child2 in the set.

	:param child1: The first child. The object must already be contained in the set.
	:param child2: The second child. The object must already be contained in the set.

.. cpp:function:: void SimSet::sort(string callbackFunction)

	Sort the objects in the set using the given comparison function.

	:param callbackFunction: Name of a function that takes two object arguments A and B and returns -1 if A is less, 1 if B is less, and 0 if both are equal.
