PxMaterial
==========

Defines a PhysX material assignable to a PxMaterial.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

When two actors collide, the collision behavior that results depends on the material properties of the actors' surfaces. For example, the surface properties determine if the actors will or will not bounce, or if they will slide or stick. Currently, the only special feature supported by materials is anisotropic friction, but according to Nvidia, other effects such as moving surfaces and more types of friction are slotted for future release.

For more information, refer to Nvidia's PhysX docs.

Fields
------

.. cpp:member:: float  PxMaterial::dynamicFriction

	Coefficient of dynamic friction to be applied. Dynamic friction reduces the velocity of a moving object while it is in contact with a surface. A higher coefficient will result in a larger reduction in velocity. A shape's dynamicFriction should be equal to or larger than 0.

.. cpp:member:: float  PxMaterial::restitution

	Coeffecient of a bounce applied to the shape in response to a collision. A value of 0 makes the object bounce as little as possible, while higher values up to 1.0 result in more bounce.

.. cpp:member:: float  PxMaterial::staticFriction

	Coefficient of static friction to be applied. Static friction determines the force needed to start moving an at-rest object in contact with a surface. If the force applied onto shape cannot overcome the force of static friction, the shape will remain at rest. A higher coefficient will require a larger force to start motion.
