Physics
=======

Objects and functions related to Torque 3D's physics layer. 

Classes
-------

 .. toctree::
	:maxdepth: 1
	
	class/PhysicsDebris
	class/PhysicsDebrisData
	class/PhysicsForce
	class/PhysicsShape
	class/PhysicsShapeData
	class/PxCloth
	class/PxMaterial
	class/PxMultiActor
	class/PxMultiActorData
	class/RadialImpulseEvent
	class/RigidShape
	class/RigidShapeData

Enumeration
-----------

.. cpp:member:: enum  PhysicsSimType

	How to handle the physics simulation with the client's and server.

	:param ClientOnly: Only handle physics on the client.
	:param ServerOnly: Only handle physics on the server.
	:param ClientServer: Handle physics on both the client and server.

Variables
---------

.. cpp:member:: bool $PhysXLogWarnings

	Output PhysX warnings to the console.

.. cpp:member:: bool $Physics::isSinglePlayer

	Informs the physics simulation if only a single player exists. If true, optimizations will be implemented to better cater to a single player environmnent.

.. cpp:member:: bool  physicsPluginPresent

	Returns true if a physics plugin exists and is initialized. physicsPluginPresent()

.. cpp:member:: int $pref::Physics::threadCount

	Number of threads to use in a single pass of the physics engine. Defaults to 2 if not set.
