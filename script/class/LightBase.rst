LightBase
=========

This is the base class for light objects.

Inherit:
	:doc:`SceneObject`

Description
-----------

It is *NOT* intended to be used directly in script, but exists to provide the base member variables and generic functionality. You should be using the derived classes PointLight and SpotLight, which can be declared in TorqueScript or added from the World Editor.

For this class, we only add basic lighting options that all lighting systems would use. The specific lighting system options are injected at runtime by the lighting system itself.

Methods
-------

.. cpp:function:: void LightBase::playAnimation()

	Plays the light animation assigned to this light with the existing LightAnimData datablock.

	Example::

		// Play the animation assigned to this light
		CrystalLight.playAnimation();

.. cpp:function:: void LightBase::playAnimation(LightAnimData anim)

	Plays the light animation on this light using a new LightAnimData . If no LightAnimData is passed the existing one is played.

	:param anim: Name of the LightAnimData datablock to be played

	Example::

		// Play the animation using a new LightAnimData datablock
		CrystalLight.playAnimation(SubtlePulseLightAnim);

.. cpp:function:: void LightBase::setLightEnabled(bool state)

	Toggles the light on and off.

	:param state: Turns the light on (true) or off (false)

	Example::

		// Disable the light
		CrystalLight.setLightEnabled(false);
		
		// Renable the light
		CrystalLight.setLightEnabled(true);

Fields
------

.. cpp:member:: bool  LightBase::animate

	Toggles animation for the light on and off.

.. cpp:member:: float  LightBase::animationPeriod

	The length of time in seconds for a single playback of the light animation (must be gt 0).

.. cpp:member:: float  LightBase::animationPhase

	The phase used to offset the animation start time to vary the animation of nearby lights.

.. cpp:member:: LightAnimData LightBase::animationType

	Datablock containing light animation information ( LightAnimData ).

.. cpp:member:: Point3F  LightBase::attenuationRatio

	The proportions of constant, linear, and quadratic attenuation to use for the falloff for point and spot lights.

.. cpp:member:: float  LightBase::brightness

	Adjusts the lights power, 0 being off completely.

.. cpp:member:: bool  LightBase::castShadows

	Enables/disabled shadow casts by this light.

.. cpp:member:: ColorF  LightBase::color

	Changes the base color hue of the light.

.. cpp:member:: filename  LightBase::cookie

	A custom pattern texture which is projected from the light.

.. cpp:member:: float  LightBase::fadeStartDistance

	Start fading shadows out at this distance. 0 = auto calculate this distance.

.. cpp:member:: float  LightBase::flareScale

	Globally scales all features of the light flare.

.. cpp:member:: LightFlareData LightBase::flareType

	Datablock containing light flare information ( LightFlareData ).

.. cpp:member:: bool  LightBase::includeLightmappedGeometryInShadow

	This light should render lightmapped geometry during its shadow-map update (ignored if 'representedInLightmap' is false).

.. cpp:member:: bool  LightBase::isEnabled

	Enables/Disables the object rendering and functionality in the scene.

.. cpp:member:: bool  LightBase::lastSplitTerrainOnly

	This toggles only terrain being rendered to the last split of a PSSM shadow map.

.. cpp:member:: float  LightBase::logWeight

	The logrithmic PSSM split distance factor.

.. cpp:member:: int  LightBase::numSplits

	The logrithmic PSSM split distance factor.

.. cpp:member:: Point4F  LightBase::overDarkFactor

	The ESM shadow darkening factor.

.. cpp:member:: void  LightBase::pauseAnimation

	Stops the light animation.

.. cpp:member:: float  LightBase::priority

	Used for sorting of lights by the light manager. Priority determines if a light has a stronger effect than, those with a lower value.

.. cpp:member:: bool  LightBase::representedInLightmap

	This light is represented in lightmaps (static light, default: false).

.. cpp:member:: ColorF  LightBase::shadowDarkenColor

	The color that should be used to multiply-blend dynamic shadows onto lightmapped geometry (ignored if 'representedInLightmap' is false).

.. cpp:member:: float  LightBase::shadowDistance

	The distance from the camera to extend the PSSM shadow.

.. cpp:member:: float  LightBase::shadowSoftness


.. cpp:member:: ShadowType LightBase::shadowType

	The type of shadow to use on this light.

.. cpp:member:: int  LightBase::texSize

	The texture size of the shadow map.
