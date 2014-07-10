SpotLight
=========

Lighting object which emits conical light in a direction.

Inherit:
	:doc:`LightBase`

Description
-----------

SpotLight is one of the two types of lighting objects that can be added to a Torque 3D level, the other being PointLight. Unlike directional or point lights, the SpotLights emits lighting in a specific direction within a cone. The distance of the cone is controlled by the SpotLight::range variable.

Example::

	// Declaration of a point light in script, or created by World EditornewSpotLight(SampleSpotLight)
	{
	   range = "10";
	   innerAngle = "40";
	   outerAngle = "45";
	   isEnabled = "1";
	   color = "1 1 1 1";
	   brightness = "1";
	   castShadows = "0";
	   priority = "1";
	   animate = "1";
	   animationPeriod = "1";
	   animationPhase = "1";
	   flareType = "LightFlareExample0";
	   flareScale = "1";
	   attenuationRatio = "0 1 1";
	   shadowType = "Spot";
	   texSize = "512";
	   overDarkFactor = "2000 1000 500 100";
	   shadowDistance = "400";
	   shadowSoftness = "0.15";
	   numSplits = "1";
	   logWeight = "0.91";
	   fadeStartDistance = "0";
	   lastSplitTerrainOnly = "0";
	   representedInLightmap = "0";
	   shadowDarkenColor = "0 0 0 -1";
	   includeLightmappedGeometryInShadow = "0";
	   position = "-29.4362 -5.86289 5.58602";
	   rotation = "1 0 0 0";
	};

Fields
------

.. cpp:member:: float  SpotLight::innerAngle


.. cpp:member:: float  SpotLight::outerAngle


.. cpp:member:: float  SpotLight::range

