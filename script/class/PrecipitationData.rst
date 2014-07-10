PrecipitationData
=================

Defines the droplets used in a storm (raindrops, snowflakes, etc).

Inherit:
	:doc:`GameBaseData`

Description
-----------

Defines the droplets used in a storm (raindrops, snowflakes, etc).

Example::

	datablock PrecipitationData( HeavyRain )
	{
	   soundProfile = "HeavyRainSound";
	   dropTexture = "art/environment/precipitation/rain";
	   splashTexture = "art/environment/precipitation/water_splash";
	   dropsPerSide = 4;
	   splashesPerSide = 2;
	};


Fields
------


.. cpp:member:: string  PrecipitationData::dropShader

	The name of the shader used for raindrops.

.. cpp:member:: int  PrecipitationData::dropsPerSide

	How many rows and columns are in the raindrop texture. For example, if the texture has 16 raindrops arranged in a grid, this field should be set to 4.

.. cpp:member:: filename  PrecipitationData::dropTexture

	Texture filename for drop particles. The drop texture can contain several different drop sub-textures arranged in a grid. There must be the same number of rows as columns. A random frame will be chosen for each drop.

.. cpp:member:: SFXTrack PrecipitationData::soundProfile

	Looping SFXProfile effect to play while Precipitation is active.

.. cpp:member:: int  PrecipitationData::splashesPerSide

	How many rows and columns are in the splash texture. For example, if the texture has 9 splashes arranged in a grid, this field should be set to 3.

.. cpp:member:: string  PrecipitationData::splashShader

	The name of the shader used for splashes.

.. cpp:member:: filename  PrecipitationData::splashTexture

	Texture filename for splash particles. The splash texture can contain several different splash sub-textures arranged in a grid. There must be the same number of rows as columns. A random frame will be chosen for each splash.
