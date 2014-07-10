PhysicsShape
============

Represents a destructible physical object simulated through the plugin system.

Inherit:
	:doc:`GameBase`

Description
-----------

Represents a destructible physical object simulated through the plugin system.


Methods
-------


.. cpp:function:: void PhysicsShape::destroy()

	Disables rendering and physical simulation. Calling destroy() will also spawn any explosions, debris, and/or destroyedShape defined for it, as well as remove it from the scene graph. Destroyed objects are only created on the server. Ghosting will later update the client.

.. cpp:function:: bool PhysicsShape::isDestroyed()

	Returns if a PhysicsShape has been destroyed or not.

.. cpp:function:: void PhysicsShape::restore()

	Restores the shape to its state before being destroyed. Re-enables rendering and physical simulation on the object and adds it to the client's scene graph. Has no effect if the shape is not destroyed.

Fields
------


.. cpp:member:: bool  PhysicsShape::playAmbient

	Enables or disables playing of an ambient animation upon loading the shape.
