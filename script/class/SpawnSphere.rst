SpawnSphere
===========

This class is used for creating any type of game object, assigning it a class, datablock, and other properties when it is spawned.

Inherit:
	:doc:`MissionMarker`

Description
-----------

Torque 3D uses a simple spawn system, which can be easily modified to spawn any kind of object (of any class). Each new level already contains at least one SpawnSphere, which is represented by a green octahedron in stock Torque 3D. The spawnClass field determines the object type, such as Player, AIPlayer, etc. The spawnDataBlock field applies the pre-defined datablock to each spawned object instance. The really powerful feature of this class is provided by the spawnScript field which allows you to define a simple script (multiple lines) that will be executed once the object has been spawned.

Example::

	// Define an SpawnSphere that essentially performs the following each time an object is spawned
	//$SpawnObject = new Player()
	//{
	//   dataBlock = "DefaultPlayerData";
	//   name = "Bob";
	//   lifeTotal = 3;
	//};
	//echo("Spawned a Player: " @ $SpawnObject);
	newSpawnSphere(DefaultSpawnSphere)
	{
	   spawnClass = "Player";
	   spawnDatablock = "DefaultPlayerData";
	   spawnScript = "echo(\"Spawned a Player: \" @ $SpawnObject);"; // embedded quotes must be escaped with \ spawnProperties = "name = \"Bob\";lifeTotal = 3;"; // embedded quotes must be escaped with \ autoSpawn = "1";
	   dataBlock = "SpawnSphereMarker";
	   position = "-0.77266 -19.882 17.8153";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	   canSave = "1";
	   canSaveDynamicFields = "1";
	};
	
	// Because autoSpawn is set to true in the above example, the following lines
	// of code will execute AFTER the Player object has been spawned.
	echo("Object Spawned");
	echo("Hello World");

Methods
-------

.. cpp:function:: void SpawnSphere::onAdd(int objectId)

	Called when the SpawnSphere is being created.

	:param objectId: The unique SimObjectId generated when SpawnSphere is created (%this in script)

.. cpp:function:: bool SpawnSphere::spawnObject(string additionalProps)

	Dynamically create a new game object with a specified class, datablock, and optional properties. This is called on the actual SpawnSphere , not to be confused with the Sim::spawnObject() global function

	:param additionalProps: Optional set of semiconlon delimited parameters applied to the spawn object during creation.

	Example::

		// Use the SpawnSphere::spawnObject function to create a game object// No additional properties assigned
		%player = DefaultSpawnSphere.spawnObject();

Fields
------


.. cpp:member:: bool  SpawnSphere::autoSpawn

	Flag to spawn object as soon as SpawnSphere is created, true to enable or false to disable.

.. cpp:member:: float  SpawnSphere::indoorWeight

	Deprecated.

.. cpp:member:: float  SpawnSphere::outdoorWeight

	Deprecated.

.. cpp:member:: float  SpawnSphere::radius

	Deprecated.

.. cpp:member:: string  SpawnSphere::spawnClass

	Object class to create (eg. Player , AIPlayer , Debris etc).

.. cpp:member:: string  SpawnSphere::spawnDatablock

	Predefined datablock assigned to the object when created.

.. cpp:member:: string  SpawnSphere::spawnProperties

	String containing semicolon (;) delimited properties to set when the object is created.

.. cpp:member:: string  SpawnSphere::spawnScript

	Command to execute immediately after spawning an object. New object id is stored in $SpawnObject. Max 255 characters.

.. cpp:member:: bool  SpawnSphere::spawnTransform

	Flag to set the spawned object's transform to the SpawnSphere's transform.

.. cpp:member:: float  SpawnSphere::sphereWeight

	Deprecated.
