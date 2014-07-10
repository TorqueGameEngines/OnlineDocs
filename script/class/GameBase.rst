GameBase
========

Base class for game objects which use datablocks, networking, are editable, and need to process ticks.

Inherit:
	:doc:`SceneObject`

Description
-----------

Base class for game objects which use datablocks, networking, are editable, and need to process ticks.


Methods
-------


.. cpp:function:: bool GameBase::applyImpulse(Point3F pos, VectorF vel)

	Apply an impulse to this object as defined by a world position and velocity vector.

	:param pos: impulse world position
	:param vel: impulse velocity (impulse force F = m * v)

	:return: Always true 

.. cpp:function:: void GameBase::applyRadialImpulse(Point3F origin, float radius, float magnitude)

	Applies a radial impulse to the object using the given origin and force.

	:param origin: World point of origin of the radial impulse.
	:param radius: The radius of the impulse area.
	:param magnitude: The strength of the impulse.

.. cpp:function:: int GameBase::getDataBlock()

	Get the datablock used by this object.

	:return:  is using.

.. cpp:function:: void GameBase::setControl(bool controlled)

	Called when the client controlling the object changes.

	:param controlled: true if a client now controls this object, false if no client controls this object.

.. cpp:function:: bool GameBase::setDataBlock(GameBaseData data)

	Assign this GameBase to use the specified datablock.

	:param data: new datablock to use

	:return: true if successful, false if failed.

Fields
------


.. cpp:member:: bool  GameBase::boundingBox  [static]

	Toggles on the rendering of the bounding boxes for certain types of objects in scene.

.. cpp:member:: GameBaseData GameBase::dataBlock

	Script datablock used for game objects.
