PhysicsDebris
=============

Represents one or more rigid bodies defined in a single mesh file with a limited lifetime.

Inherit:
	:doc:`GameBase`

Description
-----------

A PhysicsDebris object can be viewed as a single system capable of generating multiple PhysicsBodies as debris when triggered. Vaguely similar to how a ParticleEmitter is capable of creating Particles, but isn't a particle in itself. After it's lifetime has elapsed, the object will be deleted.

PhysicsDebris loads a standard .DAE or .DTS file and creates a rigid body for each defined collision node.

For collision nodes to work correctly, they must be setup as follows:

* Visible mesh nodes are siblings of the collision node under a common parent dummy node.
* Collision node is a child of its visible mesh node.

Colmesh type nodes are NOT supported; physx and most standard rigid body simulations do not support arbitrary triangle meshs for dynamics do to the computational expense.

Therefore, collision nodes must be one of the following:

* Colbox
* Colsphere
* Colcapsule
* Col (convex)

PhysicsDebris should NOT be created on the server.

