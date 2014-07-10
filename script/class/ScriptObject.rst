ScriptObject
============

A script-level OOP object which allows binding of a class, superClass and arguments along with declaration of methods.

Inherit:
	:doc:`SimObject`

Description
-----------

ScriptObjects are extrodinarily powerful objects that allow defining of any type of data required. They can optionally have a class and a superclass defined for added control of multiple ScriptObjects through a simple class definition.

Example::

	newScriptObject(Game)
	{
	   class = "DeathMatchGame";
	   superClass = GameCore;
	   genre = "Action FPS"; // Note the new, non-Torque variable
	};


Methods
-------


.. cpp:function:: void ScriptObject::onAdd(SimObjectId ID)

	Called when this ScriptObject is added to the system.

	:param ID: Unique object ID assigned when created (this in script).

.. cpp:function:: void ScriptObject::onRemove(SimObjectId ID)

	Called when this ScriptObject is removed from the system.

	:param ID: Unique object ID assigned when created (this in script).
