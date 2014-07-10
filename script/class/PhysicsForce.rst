PhysicsForce
============

Helper object for gameplay physical forces.

Inherit:
	:doc:`SceneObject`

Description
-----------

PhysicsForces can be created and "attached" to other PhysicsBodies to attract them to the position of the PhysicsForce.

Methods
-------

.. cpp:function:: void PhysicsForce::attach(Point3F start, Point3F direction, float maxDist)

	Attempts to associate the PhysicsForce with a PhysicsBody. Performs a physics ray cast of the provided length and direction. The PhysicsForce will attach itself to the first dynamic PhysicsBody the ray collides with. On every tick, the attached body will be attracted towards the position of the PhysicsForce. A PhysicsForce can only be attached to one body at a time.

.. cpp:function:: void PhysicsForce::detach(Point3F force)

	Disassociates the PhysicsForce from any attached PhysicsBody.

	:param force: Optional force to apply to the attached PhysicsBody before detaching.

.. cpp:function:: bool PhysicsForce::isAttached()

	Returns true if the PhysicsForce is currently attached to an object.
