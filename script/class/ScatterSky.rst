ScatterSky
==========

Represents both the sun and sky for scenes with a dynamic time of day.

Inherit:
	:doc:`SceneObject`

Description
-----------

Represents both the sun and sky for scenes with a dynamic time of day.

ScatterSky renders as a dome shaped mesh which is camera relative and always overhead. It is intended to be part of the background of your scene and renders before all other objects types.

ScatterSky is designed for outdoor scenes which need to transition fluidly between radically different times of day. It will respond to time changes originating from a TimeOfDay object or the elevation field can be directly adjusted.

During day, ScatterSky uses atmosphereic sunlight scattering aproximations to generate a sky gradient and sun corona. It also calculates the fog color, ambient color, and sun color, which are used for scene lighting. This is user controlled by fields within the ScatterSky group.

During night, ScatterSky supports can transition to a night sky cubemap and moon sprite. The user can control this and night time colors used for scene lighting with fields within the Night group.

A scene with a ScatterSky should not have any other sky or sun objects as it already fulfills both roles.

ScatterSky is intended to be used with CloudLayer and TimeOfDay as part of a scene with dynamic lighting. Having a ScatterSky without a changing time of day would unnecessarily give up artistic control compared and fillrate compared to a SkyBox + Sun setup.


Methods
-------


.. cpp:function:: void ScatterSky::applyChanges()

	Apply a full network update of all fields to all clients.

Fields
------


.. cpp:member:: ColorF  ScatterSky::ambientScale

	Modulates the ambient color of sunlight.

.. cpp:member:: Point3F  ScatterSky::attenuationRatio

	The proportions of constant, linear, and quadratic attenuation to use for the falloff for point and spot lights.

.. cpp:member:: float  ScatterSky::azimuth

	The horizontal angle of the sun measured clockwise from the positive Y world axis. This field is networked.

.. cpp:member:: float  ScatterSky::brightness

	The brightness of the ScatterSky's light object.

.. cpp:member:: bool  ScatterSky::castShadows

	Enables/disables shadows cast by objects due to ScatterSky light.

.. cpp:member:: ColorF  ScatterSky::colorize

	Tints the sky the color specified, the alpha controls the brigthness. The brightness is multipled by the value of colorizeAmt.

.. cpp:member:: float  ScatterSky::colorizeAmount

	Controls how much the the alpha component of colorize brigthens the sky. Setting to 0 returns default behavior.

.. cpp:member:: filename  ScatterSky::cookie

	A custom pattern texture which is projected from the light.

.. cpp:member:: float  ScatterSky::elevation

	The elevation angle of the sun above or below the horizon. This field is networked.

.. cpp:member:: float  ScatterSky::exposure

	Controls the contrast of the sky and sun during daytime.

.. cpp:member:: float  ScatterSky::fadeStartDistance

	Start fading shadows out at this distance. 0 = auto calculate this distance.

.. cpp:member:: float  ScatterSky::flareScale

	Changes the size and intensity of the flare.

.. cpp:member:: LightFlareData ScatterSky::flareType

	Datablock for the flare produced by the ScatterSky .

.. cpp:member:: ColorF  ScatterSky::fogScale

	Modulates the fog color. Note that this overrides the LevelInfo.fogColor property, so you should not use LevelInfo.fogColor if the level contains a ScatterSky object.

.. cpp:member:: bool  ScatterSky::includeLightmappedGeometryInShadow

	This light should render lightmapped geometry during its shadow-map update (ignored if 'representedInLightmap' is false).

.. cpp:member:: bool  ScatterSky::lastSplitTerrainOnly

	This toggles only terrain being rendered to the last split of a PSSM shadow map.

.. cpp:member:: float  ScatterSky::logWeight

	The logrithmic PSSM split distance factor.

.. cpp:member:: float  ScatterSky::moonAzimuth

	The horizontal angle of the moon measured clockwise from the positive Y world axis. This is not animated by time or networked.

.. cpp:member:: float  ScatterSky::moonElevation

	The elevation angle of the moon above or below the horizon. This is not animated by time or networked.

.. cpp:member:: bool  ScatterSky::moonEnabled

	Enable or disable rendering of the moon sprite during night.

.. cpp:member:: ColorF  ScatterSky::moonLightColor

	Color of light cast by the directional light during night.

.. cpp:member:: string  ScatterSky::moonMat

	Material for the moon sprite.

.. cpp:member:: float  ScatterSky::moonScale

	Controls size the moon sprite renders, specified as a fractional amount of the screen height.

.. cpp:member:: ColorF  ScatterSky::nightColor

	The ambient color during night. Also used for the sky color if useNightCubemap is false.

.. cpp:member:: string  ScatterSky::nightCubemap

	Cubemap visible during night.

.. cpp:member:: ColorF  ScatterSky::nightFogColor

	The fog color during night.

.. cpp:member:: int  ScatterSky::numSplits

	The logrithmic PSSM split distance factor.

.. cpp:member:: Point4F  ScatterSky::overDarkFactor

	The ESM shadow darkening factor.

.. cpp:member:: float  ScatterSky::rayleighScattering

	Controls how blue the atmosphere is during the day.

.. cpp:member:: bool  ScatterSky::representedInLightmap

	This light is represented in lightmaps (static light, default: false).

.. cpp:member:: ColorF  ScatterSky::shadowDarkenColor

	The color that should be used to multiply-blend dynamic shadows onto lightmapped geometry (ignored if 'representedInLightmap' is false).

.. cpp:member:: float  ScatterSky::shadowDistance

	The distance from the camera to extend the PSSM shadow.

.. cpp:member:: float  ScatterSky::shadowSoftness


.. cpp:member:: ShadowType ScatterSky::shadowType

	The type of shadow to use on this light.

.. cpp:member:: float  ScatterSky::skyBrightness

	Global brightness and intensity applied to the sky and objects in the level.

.. cpp:member:: ColorF  ScatterSky::sunScale

	Modulates the directional color of sunlight.

.. cpp:member:: float  ScatterSky::sunSize

	Affects the size of the sun's disk.

.. cpp:member:: int  ScatterSky::texSize

	The texture size of the shadow map.

.. cpp:member:: bool  ScatterSky::useNightCubemap

	Transition to the nightCubemap during night. If false we use nightColor.
