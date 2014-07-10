LightFlareData
==============

Defines a light flare effect usable by scene lights.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

LightFlareData is a datablock which defines a type of flare effect. This may then be referenced by other classes which support the rendering of a flare: Sun, ScatterSky, LightBase.

A flare contains one or more elements defined in the element* named fields of LightFlareData, with a maximum of ten elements. Each element is rendered as a 2D sprite in screenspace.

Example::

	// example from Full Template, core/art/datablocks/lights.cs
	datablock LightFlareData( LightFlareExample0 )
	{
	   overallScale = 2.0;
	   flareEnabled = true;
	   renderReflectPass = true;
	   flareTexture = "./../special/lensFlareSheet1";
	   occlusionRadius = 0.25;
	   
	   elementRect[0] = "0 512 512 512";
	   elementDist[0] = 0.0;
	   elementScale[0] = 0.5;
	   elementTint[0] = "1.0 1.0 1.0";
	   elementRotate[0] = false;
	   elementUseLightColor[0] = false;
	   
	   elementRect[1] = "512 0 512 512";
	   elementDist[1] = 0.0;
	   elementScale[1] = 2.0;
	   elementTint[1] = "0.5 0.5 0.5";
	   elementRotate[1] = false;
	   elementUseLightColor[1] = false;
	};

The elementDist field defines where along the flare's beam the element appears. A distance of 0.0 is directly over the light source, a distance of 1.0 is at the screen center, and a distance of 2.0 is at the position of the light source mirrored across the screen center.

Methods
-------

.. cpp:function:: void LightFlareData::apply()

	Intended as a helper to developers and editor scripts. Force trigger an inspectPostApply

Fields
------

.. cpp:member:: float  LightFlareData::elementDist [20]

	Where this element appears along the flare beam.

.. cpp:member:: RectF  LightFlareData::elementRect [20]

	A rectangle specified in pixels of the flareTexture image.

.. cpp:member:: bool  LightFlareData::elementRotate [20]

	Defines if this element orients to point along the flare beam or if it is always upright.

.. cpp:member:: float  LightFlareData::elementScale [20]

	Size scale applied to this element.

.. cpp:member:: ColorF  LightFlareData::elementTint [20]

	Used to modulate this element's color if elementUseLightColor is false.

.. cpp:member:: bool  LightFlareData::elementUseLightColor [20]

	If true this element's color is modulated by the light color. If false, elementTint will be used.

.. cpp:member:: bool  LightFlareData::flareEnabled

	Allows the user to disable this flare globally for any lights referencing it.

.. cpp:member:: filename  LightFlareData::flareTexture

	The texture / sprite sheet for this flare.

.. cpp:member:: float  LightFlareData::occlusionRadius

	If positive an occlusion query is used to test flare visibility, else it uses simple raycasts.

.. cpp:member:: float  LightFlareData::overallScale

	Size scale applied to all elements of the flare.

.. cpp:member:: bool  LightFlareData::renderReflectPass

	If false the flare does not render in reflections, else only non-zero distance elements are rendered.
