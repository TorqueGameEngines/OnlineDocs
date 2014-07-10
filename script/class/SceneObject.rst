SceneObject
===========

A networkable object that exists in the 3D world.

Inherit:
	:doc:`NetObject`

Description
-----------

A networkable object that exists in the 3D world.

The SceneObject class provides the foundation for 3D objects in the Engine. It exposes the functionality for:

You do not typically work with SceneObjects themselves. The SceneObject provides a reference within the game world (the scene), but does not render to the client on its own. The same is true of collision detection beyond that of the bounding box. Instead you use one of the many classes that derrive from SceneObject, such as TSStatic.

Difference Between setHidden() and isRenderEnabled
--------------------------------------------------

When it comes time to decide if a SceneObject should render or not, there are two methods that can stop the SceneObject from rendering at all. You need to be aware of the differences between these two methods as they impact how the SceneObject is networked from the server to the client.

The first method of manually controlling if a SceneObject is rendered is through its SceneObject::isRenderEnabled property. When set to false the SceneObject is considered invisible but still present within the scene. This means it still takes part in collisions and continues to be networked.

The second method is using the setHidden() method. This will actually remove a SceneObject from the scene and it will no longer be networked from the server to the cleint. Any client-side ghost of the object will be deleted as the server no longer considers the object to be in scope.


Methods
-------


.. cpp:function:: Point3F SceneObject::getEulerRotation()

	Get Euler rotation of this object.

	:return: the orientation of the object in the form of rotations around the X, Y and Z axes in degrees. 

.. cpp:function:: VectorF SceneObject::getForwardVector()

	Get the direction this object is facing.

	:return: a vector indicating the direction this object is facing. 

.. cpp:function:: TransformF SceneObject::getInverseTransform()

	Get the object's inverse transform.

	:return: the inverse transform of the object 

.. cpp:function:: int SceneObject::getMountedObject(int slot)

	Get the object mounted at a particular slot.

	:param slot: mount slot index to query

	:return: ID of the object mounted in the slot, or 0 if no object. 

.. cpp:function:: int SceneObject::getMountedObjectCount()

	Get the number of objects mounted to us.

	:return: the number of mounted objects. 

.. cpp:function:: int SceneObject::getMountedObjectNode(int slot)

	Get the mount node index of the object mounted at our given slot.

	:param slot: mount slot index to query

	:return: index of the mount node used by the object mounted in this slot. 

.. cpp:function:: int SceneObject::getMountNodeObject(int node)

	Get the object mounted at our given node index.

	:param node: mount node index to query

	:return: ID of the first object mounted at the node, or 0 if none found. 

.. cpp:function:: Box3F SceneObject::getObjectBox()

	Get the object's bounding box (relative to the object's origin).

	:return: six fields, two Point3Fs, containing the min and max points of the objectbox. 

.. cpp:function:: int SceneObject::getObjectMount()

	Get the object we are mounted to.

	:return: the SimObjectID of the object we're mounted to, or 0 if not mounted. 

.. cpp:function:: Point3F SceneObject::getPosition()

	Get the object's world position. Reimplemented in Camera .

	:return: the current world position of the object 

.. cpp:function:: VectorF SceneObject::getRightVector()

	Get the right vector of the object.

	:return: a vector indicating the right direction of this object.

.. cpp:function:: Point3F SceneObject::getScale()

	Get the object's scale.

	:return: object scale as a Point3F 

.. cpp:function:: TransformF SceneObject::getTransform()

	Get the object's transform.

	:return: the current transform of the object 

.. cpp:function:: int SceneObject::getType()

	Return the type mask for this object.

	:return: The numeric type mask for the object. 

.. cpp:function:: VectorF SceneObject::getUpVector()

	Get the up vector of the object.

	:return: a vector indicating the up direction of this object.

.. cpp:function:: Box3F SceneObject::getWorldBox()

	Get the object's world bounding box.

	:return: six fields, two Point3Fs, containing the min and max points of the worldbox. 

.. cpp:function:: Point3F SceneObject::getWorldBoxCenter()

	Get the center of the object's world bounding box.

	:return: the center of the world bounding box for this object. 

.. cpp:function:: bool SceneObject::isGlobalBounds()

	Check if this object has a global bounds set. If global bounds are set to be true, then the object is assumed to have an infinitely large bounding box for collision and rendering purposes.

	:return: true if the object has a global bounds. 

.. cpp:function:: bool SceneObject::isMounted()

	Check if we are mounted to another object.

	:return: true if mounted to another object, false if not mounted. 

.. cpp:function:: bool SceneObject::mountObject(SceneObject objB, int slot, TransformF txfm)

	Mount objB to this object at the desired slot with optional transform.

	:param objB: Object to mount onto us
	:param slot: Mount slot ID
	:param txfm: (optional) mount offset transform

	:return: true if successful, false if failed (objB is not valid) 

.. cpp:function:: void SceneObject::setScale(Point3F scale)

	Set the object's scale.

	:param scale: object scale to set

.. cpp:function:: void SceneObject::setTransform(TransformF txfm)

	Set the object's transform (orientation and position).

	:param txfm: object transform to set

.. cpp:function:: void SceneObject::unmount()

	Unmount us from the currently mounted object if any.

.. cpp:function:: bool SceneObject::unmountObject(SceneObject target)

	Unmount an object from ourselves.

	:param target: object to unmount

	:return: true if successful, false if failed 

Fields
------


.. cpp:member:: bool  SceneObject::isRenderEnabled

	Controls client-side rendering of the object.

.. cpp:member:: bool  SceneObject::isSelectionEnabled

	Determines if the object may be selected from wihin the Tools.

.. cpp:member:: int  SceneObject::mountNode

	Node we are mounted to.

.. cpp:member:: pid  SceneObject::mountPID

	PersistentID of object we are mounted to. Unlike the SimObjectID that is determined at run time, the PersistentID of an object is saved with the level/mission and may be used to form a link between objects.

.. cpp:member:: MatrixPosition  SceneObject::mountPos

	Position we are mounted at ( object space of our mount object ).

.. cpp:member:: MatrixRotation  SceneObject::mountRot

	Rotation we are mounted at ( object space of our mount object ).

.. cpp:member:: MatrixPosition  SceneObject::position

	Object world position.

.. cpp:member:: MatrixRotation  SceneObject::rotation

	Object world orientation.

.. cpp:member:: Point3F  SceneObject::scale

	Object world scale.
