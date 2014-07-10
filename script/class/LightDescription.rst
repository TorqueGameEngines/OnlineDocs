LightDescription
================

A helper datablock used by classes (such as shapebase) that submit lights to the scene but do not use actual "LightBase" objects.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

A helper datablock used by classes (such as shapebase) that submit lights to the scene but do not use actual "LightBase" objects.

This datablock stores the properties of that light as fields that can be initialized from script.

Example::

	// Declare a light description to be used on a rocket launcher projectile
	datablock LightDescription(RocketLauncherLightDesc)
	{
	   range = 4.0;
	   color = "1 1 0";
	   brightness = 5.0;
	   animationType = PulseLightAnim;
	   animationPeriod = 0.25;
	};
	
	// Declare a ProjectileDatablock which uses the light description
	datablock ProjectileData(RocketLauncherProjectile)
	{
	   lightDesc = RocketLauncherLightDesc;
	
	   projectileShapeName = "art/shapes/weapons/SwarmGun/rocket.dts";
	
	   directDamage = 30;
	   radiusDamage = 30;
	   damageRadius = 5;
	   areaImpulse = 2500;
	
	   // ... remaining ProjectileData fields not listed for this example
	};


Methods
-------


.. cpp:function:: void LightDescription::apply()

	Force an inspectPostApply call for the benefit of tweaking via the console. Normally this functionality is only exposed to objects via the World Editor, once changes have been made. Exposing apply to script allows you to make changes to it on the fly without the World Editor.

	Example::

		// Change a property of the light description
		RocketLauncherLightDesc.brightness = 10;
		
		// Make it so
		RocketLauncherLightDesc.apply();

Fields
------


.. cpp:member:: float  LightDescription::animationPeriod

	The length of time in seconds for a single playback of the light animation.

.. cpp:member:: float  LightDescription::animationPhase

	The phase used to offset the animation start time to vary the animation of nearby lights.

.. cpp:member:: LightAnimData LightDescription::animationType

	Datablock containing light animation information ( LightAnimData ).

.. cpp:member:: Point3F  LightDescription::attenuationRatio

	The proportions of constant, linear, and quadratic attenuation to use for the falloff for point and spot lights.

.. cpp:member:: float  LightDescription::brightness

	Adjusts the lights power, 0 being off completely.

.. cpp:member:: bool  LightDescription::castShadows

	Enables/disabled shadow casts by this light.

.. cpp:member:: ColorF  LightDescription::color

	Changes the base color hue of the light.

.. cpp:member:: filename  LightDescription::cookie

	A custom pattern texture which is projected from the light.

.. cpp:member:: float  LightDescription::fadeStartDistance

	Start fading shadows out at this distance. 0 = auto calculate this distance.

.. cpp:member:: float  LightDescription::flareScale

	Globally scales all features of the light flare.

.. cpp:member:: LightFlareData LightDescription::flareType

	Datablock containing light flare information ( LightFlareData ).

.. cpp:member:: bool  LightDescription::includeLightmappedGeometryInShadow

	This light should render lightmapped geometry during its shadow-map update (ignored if 'representedInLightmap' is false).

.. cpp:member:: bool  LightDescription::lastSplitTerrainOnly

	This toggles only terrain being rendered to the last split of a PSSM shadow map.

.. cpp:member:: float  LightDescription::logWeight

	The logrithmic PSSM split distance factor.

.. cpp:member:: int  LightDescription::numSplits

	The logrithmic PSSM split distance factor.

.. cpp:member:: Point4F  LightDescription::overDarkFactor

	The ESM shadow darkening factor.

.. cpp:member:: float  LightDescription::range

	Controls the size (radius) of the light.

.. cpp:member:: bool  LightDescription::representedInLightmap

	This light is represented in lightmaps (static light, default: false).

.. cpp:member:: ColorF  LightDescription::shadowDarkenColor

	The color that should be used to multiply-blend dynamic shadows onto lightmapped geometry (ignored if 'representedInLightmap' is false).

.. cpp:member:: float  LightDescription::shadowDistance

	The distance from the camera to extend the PSSM shadow.

.. cpp:member:: float  LightDescription::shadowSoftness


.. cpp:member:: ShadowType LightDescription::shadowType

	The type of shadow to use on this light.

.. cpp:member:: int  LightDescription::texSize

	The texture size of the shadow map.
