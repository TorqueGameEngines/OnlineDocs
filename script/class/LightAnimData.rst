LightAnimData
=============

A datablock which defines and performs light animation, such as rotation, brightness fade, and colorization.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

A datablock which defines and performs light animation, such as rotation, brightness fade, and colorization.

Example::

	datablock LightAnimData( SubtlePulseLightAnim )
	{
	   brightnessA = 0.5;
	   brightnessZ = 1;
	   brightnessPeriod = 1;
	   brightnessKeys = "aza";
	   brightnessSmooth = true;
	};


Fields
------


.. cpp:member:: float  LightAnimData::brightnessA

	The value of the A key in the keyframe sequence.

.. cpp:member:: string  LightAnimData::brightnessKeys

	The keyframe sequence encoded into a string where characters from A to Z define a position between the two animation values.

.. cpp:member:: float  LightAnimData::brightnessPeriod

	The animation time for keyframe sequence.

.. cpp:member:: bool  LightAnimData::brightnessSmooth

	If true the transition between keyframes will be smooth.

.. cpp:member:: float  LightAnimData::brightnessZ

	The value of the Z key in the keyframe sequence.

.. cpp:member:: float  LightAnimData::colorA [3]

	The value of the A key in the keyframe sequence.

.. cpp:member:: string  LightAnimData::colorKeys [3]

	The keyframe sequence encoded into a string where characters from A to Z define a position between the two animation values.

.. cpp:member:: float  LightAnimData::colorPeriod [3]

	The animation time for keyframe sequence.

.. cpp:member:: bool  LightAnimData::colorSmooth [3]

	If true the transition between keyframes will be smooth.

.. cpp:member:: float  LightAnimData::colorZ [3]

	The value of the Z key in the keyframe sequence.

.. cpp:member:: float  LightAnimData::offsetA [3]

	The value of the A key in the keyframe sequence.

.. cpp:member:: string  LightAnimData::offsetKeys [3]

	The keyframe sequence encoded into a string where characters from A to Z define a position between the two animation values.

.. cpp:member:: float  LightAnimData::offsetPeriod [3]

	The animation time for keyframe sequence.

.. cpp:member:: bool  LightAnimData::offsetSmooth [3]

	If true the transition between keyframes will be smooth.

.. cpp:member:: float  LightAnimData::OffsetZ [3]

	The value of the Z key in the keyframe sequence.

.. cpp:member:: float  LightAnimData::rotA [3]

	The value of the A key in the keyframe sequence.

.. cpp:member:: string  LightAnimData::rotKeys [3]

	The keyframe sequence encoded into a string where characters from A to Z define a position between the two animation values.

.. cpp:member:: float  LightAnimData::rotPeriod [3]

	The animation time for keyframe sequence.

.. cpp:member:: bool  LightAnimData::rotSmooth [3]

	If true the transition between keyframes will be smooth.

.. cpp:member:: float  LightAnimData::rotZ [3]

	The value of the Z key in the keyframe sequence.
