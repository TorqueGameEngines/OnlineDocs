Sun
===

A global light affecting your entire scene and optionally renders a corona effect.

Inherit:
	:doc:`SceneObject`

Description
-----------

A global light affecting your entire scene and optionally renders a corona effect.

Sun is both the directional and ambient light for your entire scene.


Fields
------


.. cpp:member:: ColorF  Sun::ambient

	Color shading applied to surfaces not in direct contact with light source, such as in the shadows or interiors.

.. cpp:member:: void  Sun::animate

	animate( F32 duration, F32 startAzimuth, F32 endAzimuth, F32 startElevation, F32 endElevation )

.. cpp:member:: void  Sun::apply


.. cpp:member:: Point3F  Sun::attenuationRatio

	The proportions of constant, linear, and quadratic attenuation to use for the falloff for point and spot lights.

.. cpp:member:: float  Sun::azimuth

	The horizontal angle of the sun measured clockwise from the positive Y world axis.

.. cpp:member:: float  Sun::brightness

	Adjust the Sun's global contrast/intensity.

.. cpp:member:: bool  Sun::castShadows

	Enables/disables shadows cast by objects due to Sun light.

.. cpp:member:: ColorF  Sun::color

	Color shading applied to surfaces in direct contact with light source.

.. cpp:member:: filename  Sun::cookie

	A custom pattern texture which is projected from the light.

.. cpp:member:: bool  Sun::coronaEnabled

	Enable or disable rendering of the corona sprite.

.. cpp:member:: string  Sun::coronaMaterial

	Texture for the corona sprite.

.. cpp:member:: float  Sun::coronaScale

	Controls size the corona sprite renders, specified as a fractional amount of the screen height.

.. cpp:member:: ColorF  Sun::coronaTint

	Modulates the corona sprite color ( if coronaUseLightColor is false ).

.. cpp:member:: bool  Sun::coronaUseLightColor

	Modulate the corona sprite color by the color of the light ( overrides coronaTint ).

.. cpp:member:: float  Sun::elevation

	The elevation angle of the sun above or below the horizon.

.. cpp:member:: float  Sun::fadeStartDistance

	Start fading shadows out at this distance. 0 = auto calculate this distance.

.. cpp:member:: float  Sun::flareScale

	Changes the size and intensity of the flare.

.. cpp:member:: LightFlareData Sun::flareType

	Datablock for the flare produced by the Sun .

.. cpp:member:: bool  Sun::includeLightmappedGeometryInShadow

	This light should render lightmapped geometry during its shadow-map update (ignored if 'representedInLightmap' is false).

.. cpp:member:: bool  Sun::lastSplitTerrainOnly

	This toggles only terrain being rendered to the last split of a PSSM shadow map.

.. cpp:member:: float  Sun::logWeight

	The logrithmic PSSM split distance factor.

.. cpp:member:: int  Sun::numSplits

	The logrithmic PSSM split distance factor.

.. cpp:member:: Point4F  Sun::overDarkFactor

	The ESM shadow darkening factor.

.. cpp:member:: bool  Sun::representedInLightmap

	This light is represented in lightmaps (static light, default: false).

.. cpp:member:: ColorF  Sun::shadowDarkenColor

	The color that should be used to multiply-blend dynamic shadows onto lightmapped geometry (ignored if 'representedInLightmap' is false).

.. cpp:member:: float  Sun::shadowDistance

	The distance from the camera to extend the PSSM shadow.

.. cpp:member:: float  Sun::shadowSoftness


.. cpp:member:: ShadowType Sun::shadowType

	The type of shadow to use on this light.

.. cpp:member:: int  Sun::texSize

	The texture size of the shadow map.
