Prefab
======

A collection of arbitrary objects which can be allocated and manipulated as a group.

Inherit:
	:doc:`SceneObject`

Description
-----------

Prefab always points to a (.prefab) file which defines its objects. In fact more than one Prefab can reference this file and both will update if the file is modified.

Prefab is a very simple object and only exists on the server. When it is created it allocates children objects by reading the (.prefab) file like a list of instructions. It then sets their transform relative to the Prefab and Torque networking handles the rest by ghosting the new objects to clients. Prefab itself is not ghosted.

Methods
-------


.. cpp:function:: void Prefab::onLoad(SimGroup children)

	Called when the prefab file is loaded and children objects are created.

	:param children: SimGroup containing all children objects.

Fields
------

.. cpp:member:: filename  Prefab::fileName

	(.prefab) File describing objects within this prefab.
