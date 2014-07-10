LevelInfo
=========

Stores and controls the rendering and status information for a game level.

Inherit:
	:doc:`NetObject`

Description
-----------

Stores and controls the rendering and status information for a game level.

Example::

	newLevelInfo(theLevelInfo)
	{
	  visibleDistance = "1000";
	  fogColor = "0.6 0.6 0.7 1";
	  fogDensity = "0";
	  fogDensityOffset = "700";
	  fogAtmosphereHeight = "0";
	  canvasClearColor = "0 0 0 255";
	  canSaveDynamicFields = "1";
	  levelName = "Blank Room";
	  desc0 = "A blank room ready to be populated with Torque objects.";
	  Enabled = "1";
	};


Fields
------


.. cpp:member:: bool  LevelInfo::advancedLightmapSupport

	Enable expanded support for mixing static and dynamic lighting (more costly).

.. cpp:member:: EaseF  LevelInfo::ambientLightBlendCurve

	Interpolation curve to use for blending from one ambient light color to a different one.

.. cpp:member:: float  LevelInfo::ambientLightBlendPhase

	Number of seconds it takes to blend from one ambient light color to a different one.

.. cpp:member:: ColorI  LevelInfo::canvasClearColor

	The color used to clear the background before the scene or any GUIs are rendered.

.. cpp:member:: float  LevelInfo::decalBias

	NearPlane bias used when rendering Decal and DecalRoad . This should be tuned to the visibleDistance in your level.

.. cpp:member:: float  LevelInfo::fogAtmosphereHeight

	A height in meters for altitude fog falloff.

.. cpp:member:: ColorF  LevelInfo::fogColor

	The default color for the scene fog.

.. cpp:member:: float  LevelInfo::fogDensity

	The 0 to 1 density value for the exponential fog falloff.

.. cpp:member:: float  LevelInfo::fogDensityOffset

	An offset from the camera in meters for moving the start of the fog effect.

.. cpp:member:: float  LevelInfo::nearClip

	Closest distance from the camera's position to render the world.

.. cpp:member:: SFXAmbience LevelInfo::soundAmbience

	The global ambient sound environment.

.. cpp:member:: SFXDistanceModel LevelInfo::soundDistanceModel

	The distance attenuation model to use.

.. cpp:member:: float  LevelInfo::visibleDistance

	Furthest distance fromt he camera's position to render the world.
