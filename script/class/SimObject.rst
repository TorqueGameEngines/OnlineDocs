SimObject
=========

Base class for almost all objects involved in the simulation.

Description
-----------

SimObject is a base class for most of the classes you'll encounter working in Torque. It provides fundamental services allowing "smart" object referencing, creation, destruction, organization, and location. Along with SimEvent, it gives you a flexible event-scheduling system, as well as laying the foundation for the in-game editors, GUI system, and other vital subsystems.

Subclassing
~~~~~~~~~~~~

You will spend a lot of your time in Torque subclassing, or working with subclasses of, SimObject. SimObject is designed to be easy to subclass.

You should not need to override anything in a subclass except:

* the constructor/destructor
* processArguments()
* onAdd()/onRemove()
* onGroupAdd()/onGroupRemove()
* onNameChange()
* onStaticModified()
* onDeleteNotify()
* onEditorEnable()/onEditorDisable()
* inspectPreApply()/inspectPostApply()
* things from ConsoleObject (see ConsoleObject docs for specifics)

Of course, if you know what you're doing, go nuts! But in most cases, you shouldn't need to touch things not on that list.

When you subclass, you should define a typedef in the class, called Parent, that references the class you're inheriting from::

   class mySubClass : public SimObject {
       typedef SimObject Parent;
       ...

Then, when you override a method, put in::

   bool mySubClass::onAdd()
   {
       if(!Parent::onAdd())
           return false;

       // ... do other things ...
   }

Of course, you want to replace onAdd with the appropriate method call.

A SimObject's Life Cycle
~~~~~~~~~~~~~~~~~~~~~~~~

SimObjects do not live apart. One of the primary benefits of using a SimObject is that you can uniquely identify it and easily find it (using its ID). Torque does this by keeping a global hierarchy of SimGroups - a tree - containing every registered SimObject. You can then query for a given object using Sim::findObject() (or SimSet::findObject() if you want to search only a specific set)::

	// Three examples of registering an object.

	// Method 1:
	AIClient *aiPlayer = new AIClient();
	aiPlayer->registerObject();

	// Method 2:
	ActionMap* globalMap = new ActionMap;
	globalMap->registerObject("GlobalActionMap");

	// Method 3:
	bool reg = mObj->registerObject(id);

Registering a SimObject performs these tasks:

* Marks the object as not cleared and not removed.
* Assigns the object a unique SimObjectID if it does not have one already.
* Adds the object to the global name and ID dictionaries so it can be found again.
* Calls the object's onAdd() method. Note: SimObject::onAdd() performs some important initialization steps. See here for details" on how to properly subclass SimObject.
* If onAdd() fails (returns false), it calls unregisterObject().
* Checks to make sure that the SimObject was properly initialized (and asserts if not).

Calling registerObject() and passing an ID or a name will cause the object to be assigned that name and/or ID before it is registered.

Congratulations, you have now registered your object! What now?

Well, hopefully, the SimObject will have a long, useful life. But eventually, it must die.

There are a two ways a SimObject can die.

* First, the game can be shut down. This causes the root SimGroup to be unregistered and deleted. When a SimGroup is unregistered, it unregisters all of its member SimObjects; this results in everything that has been registered with Sim being unregistered, as everything registered with Sim is in the root group.
* Second, you can manually kill it off, either by calling unregisterObject() or by calling deleteObject().

When you unregister a SimObject, the following tasks are performed:

* The object is flagged as removed.
* Notifications are cleaned up.
* If the object is in a group, then it removes itself from the group.
* Delete notifications are sent out.
* Finally, the object removes itself from the Sim globals, and tells Sim to get rid of any pending events for it.

If you call deleteObject(), all of the above tasks are performed, in addition to some sanity checking to make sure the object was previously added properly, and isn't in the process of being deleted. After the object is unregistered, it deallocates itself.

Torque Editors
~~~~~~~~~~~~~~

SimObjects are one of the building blocks for the in-game editors. They provide a basic interface for the editor to be able to list the fields of the object, update them safely and reliably, and inform the object things have changed.

This interface is implemented in the following areas:

* onNameChange() is called when the object is renamed.
* onStaticModified() is called whenever a static field is modified.
* inspectPreApply() is called before the object's fields are updated, when changes are being applied.
* inspectPostApply() is called after the object's fields are updated.
* onEditorEnable() is called whenever an editor is enabled (for instance, when you hit F11 to bring up the world editor).
* onEditorDisable() is called whenever the editor is disabled (for instance, when you hit F11 again to close the world editor).

(Note: you can check the variable gEditingMission to see if the mission editor is running; if so, you may want to render special indicators. For instance, the fxFoliageReplicator renders inner and outer radii when the mission editor is runnning.)

The Console
~~~~~~~~~~~

SimObject extends ConsoleObject by allowing you to to set arbitrary dynamic fields on the object, as well as statically defined fields. This is done through two methods, setDataField and getDataField, which deal with the complexities of allowing access to two different types of object fields.

Static fields take priority over dynamic fields. This is to be expected, as the role of dynamic fields is to allow data to be stored in addition to the predefined fields.

The fields in a SimObject are like properties (or fields) in a class.

Some fields may be arrays, which is what the array parameter is for; if it's non-null, then it is parsed with dAtoI and used as an index into the array. If you access something as an array which isn't, then you get an empty string.

You don't need to read any further than this. Right now, set/getDataField are called a total of 6 times through the entire Torque codebase. Therefore, you probably don't need to be familiar with the details of accessing them. You may want to look at Con::setData instead. Most of the time you will probably be accessing fields directly, or using the scripting language, which in either case means you don't need to do anything special.

The functions to get/set these fields are very straightforward::

	setDataField(StringTable->insert("locked", false), NULL, b ? "true" : "false" );
	curObject->setDataField(curField, curFieldArray, STR.getStringValue());
	setDataField(slotName, array, value);

For advanced users: There are two flags which control the behavior of these functions. The first is ModStaticFields, which controls whether or not the DataField functions look through the static fields (defined with addField; see ConsoleObject for details) of the class. The second is ModDynamicFields, which controls dynamically defined fields. They are set automatically by the console constructor code.

Methods
-------

.. cpp:function:: void SimObject::assignFieldsFrom(SimObject fromObject)

	Copy fields from another object onto this one. The objects must be of same type. Everything from the object will overwrite what's in this object; extra fields in this object will remain. This includes dynamic fields.

	:param fromObject: The object from which to copy fields.

.. cpp:function:: void SimObject::assignPersistentId()

	Assign a persistent ID to the object if it does not already have one.

.. cpp:function:: string SimObject::call(string method, string args, ...)

	Dynamically call a method on an object.

	:param method: Name of method to call.
	:param args: Zero or more arguments for the method.

	:return: The result of the method call. 

.. cpp:function:: SimObject  SimObject::clone()

	Create a copy of this object.

	:return: An exact duplicate of this object. 

.. cpp:function:: SimObject  SimObject::deepClone()

	Create a copy of this object and all its subobjects.

	:return: An exact duplicate of this object and all objects it references. 

.. cpp:function:: void SimObject::delete()

	Delete and remove the object.

.. cpp:function:: void SimObject::dump(bool detailed)

	Dump a description of all fields and methods defined on this object to the console.

	:param detailed: Whether to print detailed information about members.

.. cpp:function:: void SimObject::dumpClassHierarchy()

	Dump the native C++ class hierarchy of this object's C++ class to the console.

.. cpp:function:: void SimObject::dumpGroupHierarchy()

	Dump the hierarchy of this object up to RootGroup to the console.

.. cpp:function:: ArrayObject  SimObject::dumpMethods()

	List the methods defined on this object. Each description is a newline-separated vector with the following elements: 
	
	* Minimum number of arguments.
	* Maximum number of arguments.
	* Prototype string.
	* Full script file path (if script method).
	* Line number of method definition in script (if script method).
	* Documentation string (not including prototype). This takes up the remainder of the vector. 

	:return:  populated with (name,description) pairs of all methods defined on the object. 

.. cpp:function:: bool SimObject::getCanSave()

	Get whether the object will be included in saves.

	:return: True if the object will be saved; false otherwise. 

.. cpp:function:: string SimObject::getClassName()

	Get the name of the C++ class which the object is an instance of.

	:return: The name of the C++ class of the object. 

.. cpp:function:: string SimObject::getClassNamespace()

	Get the name of the class namespace assigned to this object.

	:return: The name of the 'class' namespace. 

.. cpp:function:: ArrayObject  SimObject::getDebugInfo()

	Return some behind-the-scenes information on the object.

	:return:  filled with internal information about the object. 

.. cpp:function:: int SimObject::getDeclarationLine()

	Get the line number at which the object is defined in its file.

	:return: The line number of the object's definition in script. 

.. cpp:function:: string SimObject::getDynamicField(int index)

	Get a value of a dynamic field by index.

	:param index: The index of the dynamic field.

	:return: The value of the dynamic field at the given index or "". 

.. cpp:function:: int SimObject::getDynamicFieldCount()

	Get the number of dynamic fields defined on the object.

	:return: The number of dynamic fields defined on the object. 

.. cpp:function:: string SimObject::getField(int index)

	Retrieve the value of a static field by index.

	:param index: The index of the static field.

	:return: The value of the static field with the given index or "". 

.. cpp:function:: int SimObject::getFieldCount()

	Get the number of static fields on the object.

	:return: The number of static fields defined on the object. 

.. cpp:function:: string SimObject::getFieldType(string fieldName)

	Get the console type code of the given field.

	:return: The numeric type code for the underlying console type of the given field. 

.. cpp:function:: string SimObject::getFieldValue(string fieldName, int index)

	Return the value of the given field on this object.

	:param fieldName: The name of the field. If it includes a field index, the index is parsed out.
	:param index: Optional parameter to specify the index of an array field separately.

	:return: The value of the given field or "" if undefined. 

.. cpp:function:: string SimObject::getFilename()

	Returns the filename the object is attached to. Reimplemented in CubemapData .

	:return: The name of the file the object is associated with; usually the file the object was loaded from. 

.. cpp:function:: SimGroup  SimObject::getGroup()

	Get the group that this object is contained in.

	:return:  object to which the object belongs. 

.. cpp:function:: int SimObject::getId()

	Get the underlying unique numeric ID of the object.

	:return: The unique numeric ID of the object. 

.. cpp:function:: string SimObject::getInternalName()

	Get the internal name of the object.

	:return: The internal name of the object. 

.. cpp:function:: string SimObject::getName()

	Get the global name of the object.

	:return: The global name assigned to the object. 

.. cpp:function:: string SimObject::getSuperClassNamespace()

	Get the name of the superclass namespace assigned to this object.

	:return: The name of the 'superClass' namespace. 

.. cpp:function:: bool SimObject::isChildOfGroup(SimGroup group)

	Test whether the object belongs directly or indirectly to the given group.

	:param group: The SimGroup object.

	:return: True if the object is a child of the given group or a child of a group that the given group is directly or indirectly a child to. 

.. cpp:function:: bool SimObject::isEditorOnly()

	Return true if the object is only used by the editor.

	:return: True if this object exists only for the sake of editing. 

.. cpp:function:: bool SimObject::isExpanded()

	Get whether the object has been marked as expanded. (in editor). Reimplemented in GuiRolloutCtrl .

	:return: True if the object is marked expanded. 

.. cpp:function:: bool SimObject::isField(string fieldName)

	Test whether the given field is defined on this object.

	:param fieldName: The name of the field.

	:return: True if the object implements the given field. 

.. cpp:function:: bool SimObject::isInNamespaceHierarchy(string name)

	Test whether the namespace of this object is a direct or indirect child to the given namespace.

	:param name: The name of a namespace.

	:return: True if the given namespace name is within the namespace hierarchy of this object. 

.. cpp:function:: bool SimObject::isMemberOfClass(string className)

	Test whether this object is a member of the specified class.

	:param className: Name of a native C++ class.

	:return: True if this object is an instance of the given C++ class or any of its super classes. 

.. cpp:function:: bool SimObject::isMethod(string methodName)

	Test whether the given method is defined on this object.

	:param The: name of the method.

	:return: True if the object implements the given method. 

.. cpp:function:: bool SimObject::isNameChangeAllowed()

	Get whether this object may be renamed.

	:return: True if this object can be renamed; false otherwise. 

.. cpp:function:: bool SimObject::isSelected()

	Get whether the object has been marked as selected. (in editor).

	:return: True if the object is currently selected. 

.. cpp:function:: bool SimObject::save(string fileName, bool selectedOnly, string preAppendString)

	Save out the object to the given file.

	:param fileName: The name of the file to save to.
	:param selectedOnly: If true, only objects marked as selected will be saved out.
	:param preAppendString: Text which will be preprended directly to the object serialization.
	:param True: on success, false on failure.

.. cpp:function:: int SimObject::schedule(float time, string method, string args, ...)

	Delay an invocation of a method.

	:param time: The number of milliseconds after which to invoke the method. This is a soft limit.
	:param method: The method to call.
	:param args: The arguments with which to call the method.

	:return: The numeric ID of the created schedule. Can be used to cancel the call. 

.. cpp:function:: void SimObject::setCanSave(bool value)

	Set whether the object will be included in saves.

	:param value: If true, the object will be included in saves; if false, it will be excluded.

.. cpp:function:: void SimObject::setClassNamespace(string name)

	Assign a class namespace to this object.

	:param name: The name of the 'class' namespace for this object.

.. cpp:function:: void SimObject::setEditorOnly(bool value)

	Set/clear the editor-only flag on this object.

	:param value: If true, the object is marked as existing only for the editor.

.. cpp:function:: void SimObject::setFieldType(string fieldName, string type)

	Set the console type code for the given field.

	:param fieldName: The name of the dynamic field to change to type for.
	:param type: The name of the console type.

.. cpp:function:: bool SimObject::setFieldValue(string fieldName, string value, int index)

	Set the value of the given field on this object.

	:param fieldName: The name of the field to assign to. If it includes an array index, the index will be parsed out.
	:param value: The new value to assign to the field.
	:param index: Optional argument to specify an index for an array field.

	:return: True. 

.. cpp:function:: void SimObject::setFilename(string fileName)

	Sets the object's file name and path.

	:param fileName: The name of the file to associate this object with.

.. cpp:function:: void SimObject::setHidden(bool value)

	Hide/unhide the object. Reimplemented in ShapeBase .

	:param value: If true, the object will be hidden; if false, the object will be unhidden.

.. cpp:function:: void SimObject::setInternalName(string newInternalName)

	Set the internal name of the object.

	:param newInternalName: The new internal name for the object.

.. cpp:function:: void SimObject::setIsExpanded(bool state)

	Set whether the object has been marked as expanded. (in editor).

	:param state: True if the object is to be marked expanded; false if not.

.. cpp:function:: void SimObject::setIsSelected(bool state)

	Set whether the object has been marked as selected. (in editor).

	:param state: True if object is to be marked selected; false if not.

.. cpp:function:: void SimObject::setLocked(bool value)

	Lock/unlock the object in the editor.

	:param value: If true, the object will be locked; if false, the object will be unlocked.

.. cpp:function:: void SimObject::setName(string newName)

	Set the global name of the object.

	:param newName: The new global name to assign to the object.

.. cpp:function:: void SimObject::setNameChangeAllowed(bool value)

	Set whether this object can be renamed from its first name.

	:param value: If true, renaming is allowed for this object; if false, trying to change the name of the object will generate a console error.

.. cpp:function:: void SimObject::setSuperClassNamespace(string name)

	Assign a superclass namespace to this object.

	:param name: The name of the 'superClass' namespace for this object.

Fields
------

.. cpp:member:: bool  SimObject::canSave

	Whether the object can be saved out. If false, the object is purely transient in nature.

.. cpp:member:: bool  SimObject::canSaveDynamicFields

	True if dynamic fields (added at runtime) should be saved. Defaults to true.

.. cpp:member:: string  SimObject::class

	Script class of object.

.. cpp:member:: string  SimObject::className

	Script class of object.

.. cpp:member:: bool  SimObject::hidden

	Whether the object is visible.

.. cpp:member:: string  SimObject::internalName

	Optional name that may be used to lookup this object within a SimSet .

.. cpp:member:: bool  SimObject::locked

	Whether the object can be edited.

.. cpp:member:: string  SimObject::name

	Optional global name of this object.

.. cpp:member:: SimObject SimObject::parentGroup

	Group hierarchy parent of the object.

.. cpp:member:: pid  SimObject::persistentId

	The universally unique identifier for the object.

.. cpp:member:: string  SimObject::superClass

	Script super-class of object.
