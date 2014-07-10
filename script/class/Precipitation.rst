Precipitation
=============

Defines a precipitation based storm (rain, snow, etc).

Inherit:
	:doc:`GameBase`

Description
-----------

Defines a precipitation based storm (rain, snow, etc).

The Precipitation effect works by creating many 'drops' within a fixed size box. This box can be configured to move around with the camera (to simulate level-wide precipitation), or to remain in a fixed position (to simulate localized precipitation). When followCam is true, the box containing the droplets can be thought of as centered on the camera then pushed slightly forward in the direction the camera is facing so most of the box is in front of the camera (allowing more drops to be visible on screen at once).

The effect can also be configured to create a small 'splash' whenever a drop hits another world object.

Example::

	// The following is added to a level file (.mis) by the World EditornewPrecipitation( TheRain )
	{
	   dropSize = "0.5";
	   splashSize = "0.5";
	   splashMS = "250";
	   animateSplashes = "1";
	   dropAnimateMS = "0";
	   fadeDist = "0";
	   fadeDistEnd = "0";
	   useTrueBillboards = "0";
	   useLighting = "0";
	   glowIntensity = "0 0 0 0";
	   reflect = "0";
	   rotateWithCamVel = "1";
	   doCollision = "1";
	   hitPlayers = "0";
	   hitVehicles = "0";
	   followCam = "1";
	   useWind = "0";
	   minSpeed = "1.5";
	   maxSpeed = "2";
	   minMass = "0.75";
	   maxMass = "0.85";
	   useTurbulence = "0";
	   maxTurbulence = "0.1";
	   turbulenceSpeed = "0.2";
	   numDrops = "1024";
	   boxWidth = "200";
	   boxHeight = "100";
	   dataBlock = "HeavyRain";
	};


Methods
-------


.. cpp:function:: void Precipitation::modifyStorm(float percentage, float seconds)

	Smoothly change the maximum number of drops in the effect (from current value to numDrops * percentage ). This method can be used to simulate a storm building or fading in intensity as the number of drops in the Precipitation box changes.

	:param percentage: New maximum number of drops value (as a percentage of numDrops). Valid range is 0-1.
	:param seconds: Length of time (in seconds) over which to increase the drops percentage value. Set to 0 to change instantly.

	Example::

		%percentage = 0.5;  // The percentage, from 0 to 1, of the maximum drops to display
		%seconds = 5.0;     // The length of time over which to make the change.
		%precipitation.modifyStorm( %percentage, %seconds );

.. cpp:function:: void Precipitation::setPercentage(float percentage)

	Sets the maximum number of drops in the effect, as a percentage of numDrops . The change occurs instantly (use modifyStorm() to change the number of drops over a period of time.

	:param percentage: New maximum number of drops value (as a percentage of numDrops). Valid range is 0-1.

	Example::

		%percentage = 0.5;  // The percentage, from 0 to 1, of the maximum drops to display
		%precipitation.setPercentage( %percentage );

.. cpp:function:: void Precipitation::setTurbulence(float max, float speed, float seconds)

	Smoothly change the turbulence parameters over a period of time.

	:param max: New maxTurbulence value. Set to 0 to disable turbulence.
	:param speed: New turbulenceSpeed value.
	:param seconds: Length of time (in seconds) over which to interpolate the turbulence settings. Set to 0 to change instantly.

	Example::

		%turbulence = 0.5;     // Set the new turbulence value. Set to 0 to disable turbulence.
		%speed = 5.0;          // The new speed of the turbulance effect.
		%seconds = 5.0;        // The length of time over which to make the change.
		%precipitation.setTurbulence( %turbulence, %speed, %seconds );

Fields
------


.. cpp:member:: bool  Precipitation::animateSplashes

	Set to true to enable splash animations when drops collide with other surfaces.

.. cpp:member:: float  Precipitation::boxHeight

	Height (vertical dimension) of the precipitation box.

.. cpp:member:: float  Precipitation::boxWidth

	Width and depth (horizontal dimensions) of the precipitation box.

.. cpp:member:: bool  Precipitation::doCollision

	Allow drops to collide with world objects. If animateSplashes is true, drops that collide with another object will produce a simple splash animation.

.. cpp:member:: int  Precipitation::dropAnimateMS

	Length (in milliseconds) to display each drop frame. If dropAnimateMS lt = 0, drops select a single random frame at creation that does not change throughout the drop's lifetime. If dropAnimateMS gt 0, each drop cycles through the the available frames in the drop texture at the given rate.

.. cpp:member:: float  Precipitation::dropSize

	Size of each drop of precipitation. This will scale the texture.

.. cpp:member:: float  Precipitation::fadeDist

	The distance at which drops begin to fade out.

.. cpp:member:: float  Precipitation::fadeDistEnd

	The distance at which drops are completely faded out.

.. cpp:member:: bool  Precipitation::followCam

	Controls whether the Precipitation system follows the camera or remains where it is first placed in the scene. Set to true to make it seem like it is raining everywhere in the level (ie. the Player will always be in the rain). Set to false to have a single area affected by rain (ie. the Player can move in and out of the rainy area).

.. cpp:member:: ColorF  Precipitation::glowIntensity

	Set to 0 to disable the glow or or use it to control the intensity of each channel.

.. cpp:member:: bool  Precipitation::hitPlayers

	Allow drops to collide with Player objects; only valid if doCollision is true.

.. cpp:member:: bool  Precipitation::hitVehicles

	Allow drops to collide with Vehicle objects; only valid if doCollision is true.

.. cpp:member:: float  Precipitation::maxMass

	Maximum mass of a drop. Drop mass determines how strongly the drop is affected by wind and turbulence. On creation, the drop will be assigned a random speed between minMass and minMass .

.. cpp:member:: float  Precipitation::maxSpeed

	Maximum speed at which a drop will fall. On creation, the drop will be assigned a random speed between minSpeed and maxSpeed .

.. cpp:member:: float  Precipitation::maxTurbulence

	Radius at which precipitation drops spiral when turbulence is enabled.

.. cpp:member:: float  Precipitation::minMass

	Minimum mass of a drop. Drop mass determines how strongly the drop is affected by wind and turbulence. On creation, the drop will be assigned a random speed between minMass and minMass .

.. cpp:member:: float  Precipitation::minSpeed

	Minimum speed at which a drop will fall. On creation, the drop will be assigned a random speed between minSpeed and maxSpeed .

.. cpp:member:: int  Precipitation::numDrops

	Maximum number of drops allowed to exist in the precipitation box at any one time. The actual number of drops in the effect depends on the current percentage, which can change over time using modifyStorm() .

.. cpp:member:: bool  Precipitation::reflect

	This enables precipitation rendering during reflection passes.

.. cpp:member:: bool  Precipitation::rotateWithCamVel

	Set to true to include the camera velocity when calculating drop rotation speed.

.. cpp:member:: int  Precipitation::splashMS

	Lifetime of splashes in milliseconds.

.. cpp:member:: float  Precipitation::splashSize

	Size of each splash animation when a drop collides with another surface.

.. cpp:member:: float  Precipitation::turbulenceSpeed

	Speed at which precipitation drops spiral when turbulence is enabled.

.. cpp:member:: bool  Precipitation::useLighting

	Set to true to enable shading of the drops and splashes by the sun color.

.. cpp:member:: bool  Precipitation::useTrueBillboards

	Set to true to make drops true (non axis-aligned) billboards.

.. cpp:member:: bool  Precipitation::useTurbulence

	Check to enable turbulence. This causes precipitation drops to spiral while falling.

.. cpp:member:: bool  Precipitation::useWind

	Controls whether drops are affected by wind.
