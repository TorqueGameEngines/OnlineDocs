PxCloth
=======

Rectangular patch of cloth simulated by PhysX.

Inherit:
	:doc:`GameBase`

Description
-----------

PxCloth is affected by other objects in the simulation but does not itself affect others, it is essentially a visual effect. Eg, shooting at cloth will disturb it but will not explode the projectile.

Be careful with the cloth size and resolution because it can easily become performance intensive to simulate. A single piece of cloth that is very large or high resolution is also much more expensive than multiple pieces that add up to the same number of verts.

Note that most field docs have been copied from their PhysX counterpart.

Fields
------

.. cpp:member:: PxClothAttachment  PxCloth::attachments

	Optional way to specify cloth verts that will be attached to the world position it is created at.

.. cpp:member:: bool  PxCloth::bending

	Enables or disables bending resistance. Set the bending resistance through PxCloth::bendingStiffness .

.. cpp:member:: float  PxCloth::bendingStiffness

	Bending stiffness of the cloth in the range 0 to 1.

.. cpp:member:: bool  PxCloth::damping

	Enable/disable damping of internal velocities.

.. cpp:member:: float  PxCloth::dampingCoefficient

	Spring damping of the cloth in the range 0 to 1.

.. cpp:member:: float  PxCloth::density

	Density of the cloth (Mass per Area).

.. cpp:member:: float  PxCloth::friction

	Friction coefficient in the range 0 to 1. Defines the damping of the velocities of cloth particles that are in contact.

.. cpp:member:: string  PxCloth::Material

	Name of the material to render.

.. cpp:member:: Point2I  PxCloth::samples

	The number of cloth vertices in width and length. At least two verts should be defined.

.. cpp:member:: bool  PxCloth::selfCollision

	Enables or disables self-collision handling within a single piece of cloth.

.. cpp:member:: Point2F  PxCloth::size

	The width and height of the cloth.

.. cpp:member:: float  PxCloth::thickness

	Value representing how thick the cloth is. The thickness is usually a fraction of the overall extent of the cloth and should not be set to a value greater than that. A good value is the maximal distance between two adjacent cloth particles in their rest pose. Visual artifacts or collision problems may appear if the thickness is too small.

.. cpp:member:: bool  PxCloth::triangleCollision

	Not supported in current release (according to PhysX docs). Enables or disables collision detection of cloth triangles against the scene. If not set, only collisions of cloth particles are detected. If set, collisions of cloth triangles are detected as well.
