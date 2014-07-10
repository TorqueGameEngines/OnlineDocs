PointLight
==========

Lighting object that radiates light in all directions.

Inherit:
	:doc:`LightBase`

Description
-----------

PointLight is one of the two types of lighting objects that can be added to a Torque 3D level, the other being SpotLight. Unlike directional or conical light, the PointLight emits lighting in all directions. The attenuation is controlled by a single variable: LightObject::radius.

Example::

	// Declaration of a point light in script, or created by World EditornewPointLight(CrystalLight)
	{
	   radius = "10";
	   isEnabled = "1";
	   color = "1 0.905882 0 1";
	   brightness = "0.5";
	   castShadows = "1";
	   priority = "1";
	   animate = "1";
	   animationType = "SubtlePulseLightAnim";
	   animationPeriod = "3";
	   animationPhase = "3";
	   flareScale = "1";
	   attenuationRatio = "0 1 1";
	   shadowType = "DualParaboloidSinglePass";
	   texSize = "512";
	   overDarkFactor = "2000 1000 500 100";
	   shadowDistance = "400";
	   shadowSoftness = "0.15";
	   numSplits = "1";
	   logWeight = "0.91";
	   fadeStartDistance = "0";
	   lastSplitTerrainOnly = "0";
	   splitFadeDistances = "10 20 30 40";
	   representedInLightmap = "0";
	   shadowDarkenColor = "0 0 0 -1";
	   includeLightmappedGeometryInShadow = "1";
	   position = "-61.3866 1.69186 5.1464";
	   rotation = "1 0 0 0";
	};

Fields
------

.. cpp:member:: float  PointLight::radius

	Controls the falloff of the light emission.
