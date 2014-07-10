WaterObject
===========

Abstract base class for representing a body of water.

Inherit:
	:doc:`SceneObject`

Description
-----------

Abstract base class for representing a body of water.

WaterObject is abstract and may not be created. It defines functionality shared by its derived classes.

WaterObject exposes many fields for controlling it visual quality.

WaterObject surface rendering has the following general features:

It will, however, look significantly different depending on the LightingManager that is active. With Basic Lighting, we do not have a prepass texture to lookup per-pixel depth and therefore cannot use our rendering techniques that depend on it.

In particular, the following field groups are not used under Basic Lighting:

WaterObject also defines several fields for gameplay use and objects that support buoyancy.


Fields
------


.. cpp:member:: ColorI  WaterObject::baseColor

	Changes color of water fog.

.. cpp:member:: float  WaterObject::clarity

	Relative opacity or transparency of the water surface.

.. cpp:member:: string  WaterObject::cubemap

	Cubemap used instead of reflection texture if fullReflect is off.

.. cpp:member:: float  WaterObject::density

	Affects buoyancy of an object, thus affecting the Z velocity of a player (jumping, falling, etc.

.. cpp:member:: float  WaterObject::depthGradientMax

	Depth in world units, the max range of the color gradient texture.

.. cpp:member:: filename  WaterObject::depthGradientTex

	1D texture defining the base water color by depth

.. cpp:member:: float  WaterObject::distortEndDist

	Max distance that distortion algorithm is performed. The lower, the more distorted the effect.

.. cpp:member:: float  WaterObject::distortFullDepth

	Determines the scaling down of distortion in shallow water.

.. cpp:member:: float  WaterObject::distortStartDist

	Determines start of distortion effect where water surface intersects the camera near plane.

.. cpp:member:: bool  WaterObject::emissive

	When true the water colors don't react to changes to environment lighting.

.. cpp:member:: float  WaterObject::foamAmbientLerp


.. cpp:member:: Point2F  WaterObject::foamDir [2]


.. cpp:member:: float  WaterObject::foamMaxDepth


.. cpp:member:: float  WaterObject::foamOpacity [2]


.. cpp:member:: float  WaterObject::foamRippleInfluence


.. cpp:member:: float  WaterObject::foamSpeed [2]


.. cpp:member:: filename  WaterObject::foamTex

	Diffuse texture for foam in shallow water (advanced lighting only).

.. cpp:member:: Point2F  WaterObject::foamTexScale [2]

	applied to the surface.

.. cpp:member:: float  WaterObject::fresnelBias

	Extent of fresnel affecting reflection fogging.

.. cpp:member:: float  WaterObject::fresnelPower

	Measures intensity of affect on reflection based on fogging.

.. cpp:member:: bool  WaterObject::fullReflect

	Enables dynamic reflection rendering.

.. cpp:member:: string  WaterObject::liquidType

	Liquid type of WaterBlock , such as water, ocean, lava Currently only Water is defined and used.

.. cpp:member:: float  WaterObject::overallFoamOpacity


.. cpp:member:: float  WaterObject::overallRippleMagnitude

	Master variable affecting entire surface.

.. cpp:member:: float  WaterObject::overallWaveMagnitude

	Master variable affecting entire body of water's undulation.

.. cpp:member:: float  WaterObject::reflectDetailAdjust

	scale up or down the detail level for objects rendered in a reflection

.. cpp:member:: float  WaterObject::reflectivity

	Overall scalar to the reflectivity of the water surface.

.. cpp:member:: int  WaterObject::reflectMaxRateMs

	Affects the sort time of reflected objects.

.. cpp:member:: bool  WaterObject::reflectNormalUp

	always use z up as the reflection normal

.. cpp:member:: float  WaterObject::reflectPriority

	Affects the sort order of reflected objects.

.. cpp:member:: int  WaterObject::reflectTexSize

	The texture size used for reflections (square).

.. cpp:member:: Point2F  WaterObject::rippleDir [3]

	Modifies the direction of ripples on the surface.

.. cpp:member:: float  WaterObject::rippleMagnitude [3]

	Intensifies the vertext modification of the surface.

.. cpp:member:: float  WaterObject::rippleSpeed [3]

	Modifies speed of surface ripples.

.. cpp:member:: filename  WaterObject::rippleTex

	Normal map used to simulate small surface ripples.

.. cpp:member:: Point2F  WaterObject::rippleTexScale [3]

	Intensifies the affect of the normal map applied to the surface.

.. cpp:member:: SFXAmbience WaterObject::soundAmbience

	Ambient sound environment when listener is submerged.

.. cpp:member:: ColorF  WaterObject::specularColor

	Color used for specularity on the water surface ( sun only ).

.. cpp:member:: float  WaterObject::specularPower

	Power used for specularity on the water surface ( sun only ).

.. cpp:member:: ColorI  WaterObject::underwaterColor

	Changes the color shading of objects beneath the water surface.

.. cpp:member:: bool  WaterObject::useOcclusionQuery

	turn off reflection rendering when occluded (delayed).

.. cpp:member:: float  WaterObject::viscosity

	Affects drag force applied to an object submerged in this container.

.. cpp:member:: float  WaterObject::waterFogDensity

	Intensity of underwater fogging.

.. cpp:member:: float  WaterObject::waterFogDensityOffset

	Delta, or limit, applied to waterFogDensity.

.. cpp:member:: Point2F  WaterObject::waveDir [3]

	Direction waves flow toward shores.

.. cpp:member:: float  WaterObject::waveMagnitude [3]

	Height of water undulation.

.. cpp:member:: float  WaterObject::waveSpeed [3]

	Speed of water undulation.

.. cpp:member:: float  WaterObject::wetDarkening

	The refract color intensity scaled at wetDepth.

.. cpp:member:: float  WaterObject::wetDepth

	The depth in world units at which full darkening will be received, giving a wet look to objects underwater.
