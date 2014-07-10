ForestWindEmitter
=================

Object responsible for simulating wind in a level.

Inherit:
	:doc:`SceneObject`

Description
-----------

When placed in the level, a ForestWindEmitter will cause tree branches to bend and sway, leaves to flutter, and create vertical bending on the tree's trunk.

Example::

	// The following is a full declaration of a wind emitternewForestWindEmitter()
	{
	   position = "497.739 765.821 102.395";
	   windEnabled = "1";
	   radialEmitter = "1";
	   strength = "1";
	   radius = "3";
	   gustStrength = "0.5";
	   gustFrequency = "1";
	   gustYawAngle = "10";
	   gustYawFrequency = "4";
	   gustWobbleStrength = "2";
	   turbulenceStrength = "1";
	   turbulenceFrequency = "2";
	   hasMount = "0";
	   scale = "3 3 3";
	   canSave = "1";
	   canSaveDynamicFields = "1";
	   rotation = "1 0 0 0";
	};

Methods
-------

.. cpp:function:: void ForestWindEmitter::attachToObject(int objectID)

	Mounts the wind emitter to another scene object.

	:param objectID: Unique ID of the object wind emitter should attach to

	Example::

		// Wind emitter previously created and named %windEmitter// Going to attach it to the player, making him a walking wind storm
		%windEmitter.attachToObject(%player);

Fields
------

.. cpp:member:: float  ForestWindEmitter::gustFrequency

	The frequency of gusting in seconds.

.. cpp:member:: float  ForestWindEmitter::gustStrength

	The maximum strength of a gust.

.. cpp:member:: float  ForestWindEmitter::gustWobbleStrength

	The amount of random wobble added to gust and turbulence vectors.

.. cpp:member:: float  ForestWindEmitter::gustYawAngle

	The amount of degrees the wind direction can drift (both positive and negative).

.. cpp:member:: float  ForestWindEmitter::gustYawFrequency

	The frequency of wind yaw drift, in seconds.

.. cpp:member:: bool  ForestWindEmitter::hasMount

	Determines if the emitter is mounted to another object.

.. cpp:member:: bool  ForestWindEmitter::radialEmitter

	Determines if the emitter is a global direction or local radial emitter.

.. cpp:member:: float  ForestWindEmitter::radius

	The radius of the emitter for local radial emitters.

.. cpp:member:: float  ForestWindEmitter::strength

	The strength of the wind force.

.. cpp:member:: float  ForestWindEmitter::turbulenceFrequency

	The frequency of gust turbulence, in seconds.

.. cpp:member:: float  ForestWindEmitter::turbulenceStrength

	The strength of gust turbulence.

.. cpp:member:: bool  ForestWindEmitter::windEnabled

	Determines if the emitter will be counted in wind calculations.
