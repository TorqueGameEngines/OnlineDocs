Material
========

A material in Torque 3D is a data structure that describes a surface.

Inherit:
	:doc:`SimObject`

Description
-----------

It contains many different types of information for rendering properties. Torque 3D generates shaders from Material definitions. The shaders are compiled at runtime and output into the example/shaders directory. Any errors or warnings generated from compiling the procedurally generated shaders are output to the console as well as the output window in the Visual C IDE.

Example::

	singleton Material(DECAL_scorch)
	{
	   baseTex[0] = "./scorch_decal.png";
	   vertColor[ 0 ] = true;
	
	   translucent = true;
	   translucentBlendOp = None;
	   translucentZWrite = true;
	   alphaTest = true;
	   alphaRef = 84;
	};

Fields
------

.. cpp:member:: int  Material::alphaRef

	The alpha reference value for alpha testing. Must be between 0 to 255.

.. cpp:member:: bool  Material::alphaTest

	Enables alpha test when rendering the material.

.. cpp:member:: MaterialAnimType Material::animFlags [4]

	The types of animation to play on this material.

.. cpp:member:: filename  Material::baseTex [4]

	For backwards compatibility.

.. cpp:member:: bool  Material::bumpAtlas [4]


.. cpp:member:: filename  Material::bumpTex [4]

	For backwards compatibility.

.. cpp:member:: bool  Material::castShadows

	If set to false the lighting system will not cast shadows from this material.

.. cpp:member:: Point2I  Material::cellIndex [4]


.. cpp:member:: Point2I  Material::cellLayout [4]


.. cpp:member:: int  Material::cellSize [4]


.. cpp:member:: ColorF  Material::colorMultiply [4]

	For backwards compatibility.

.. cpp:member:: string  Material::cubemap

	The name of a CubemapData for environment mapping.

.. cpp:member:: SFXTrack Material::customFootstepSound

	The sound to play when the player walks over the material. If this is set, it overrides footstepSoundId . This field is useful for directly assigning custom footstep sounds to materials without having to rely on the PlayerData sound assignment. Be aware that materials are client-side objects. This means that the SFXTracks assigned to materials must be client-side, too.

.. cpp:member:: SFXTrack Material::customImpactSound

	The sound to play when the player impacts on the surface with a velocity equal or greater than PlayerData::groundImpactMinSpeed . If this is set, it overrides impactSoundId . This field is useful for directly assigning custom impact sounds to materials without having to rely on the PlayerData sound assignment. Be aware that materials are client-side objects. This means that the SFXTracks assigned to materials must be client-side, too.

.. cpp:member:: filename  Material::detailMap [4]

	A typically greyscale detail texture additively blended into the material.

.. cpp:member:: filename  Material::detailNormalMap [4]

	A second normal map texture applied at the detail scale. You can use the DXTnm format only when per-pixel specular highlights are disabled.

.. cpp:member:: float  Material::detailNormalMapStrength [4]

	Used to scale the strength of the detail normal map when blended with the base normal map.

.. cpp:member:: Point2F  Material::detailScale [4]

	The scale factor for the detail map.

.. cpp:member:: filename  Material::detailTex [4]

	For backwards compatibility.

.. cpp:member:: ColorF  Material::diffuseColor [4]

	This color is multiplied against the diffuse texture color. If no diffuse texture is present this is the material color.

.. cpp:member:: filename  Material::diffuseMap [4]

	The diffuse color texture map.

.. cpp:member:: bool  Material::doubleSided

	Disables backface culling casing surfaces to be double sided. Note that the lighting on the backside will be a mirror of the front side of the surface.

.. cpp:member:: void  Material::dumpInstances

	Dumps a formatted list of the currently allocated material instances for this material to the console.

.. cpp:member:: bool  Material::dynamicCubemap

	Enables the material to use the dynamic cubemap from the ShapeBase object its applied to.

.. cpp:member:: ColorF  Material::effectColor [2]

	If showDust is true, this is the set of colors to use for the ParticleData of the dust emitter.

.. cpp:member:: bool  Material::emissive [4]

	Enables emissive lighting for the material.

.. cpp:member:: filename  Material::envMap [4]

	The name of an environment map cube map to apply to this material.

.. cpp:member:: filename  Material::envTex [4]

	For backwards compatibility.

.. cpp:member:: void  Material::flush

	Flushes all material instances that use this material.

.. cpp:member:: int  Material::footstepSoundId

	What sound to play from the PlayerData sound list when the player walks over the material. -1 (default) to not play any sound. The IDs are: 
	
	 * 0: 
	 
	
	 * PlayerData::FootSoftSound
	 
	
	 * 1: 
	 
	
	 * PlayerData::FootHardSound
	 
	
	 * 2: 
	 
	
	 * PlayerData::FootMetalSound
	 
	
	 * 3: 
	 
	
	 * PlayerData::FootSnowSound
	 
	
	 * 4: 
	 
	
	 * PlayerData::FootShallowSound
	 
	
	 * 5: 
	 
	
	 * PlayerData::FootWadingSound
	 
	
	 * 6: 
	 
	
	 * PlayerData::FootUnderwaterSound
	 
	
	 * 7: 
	 
	
	 * PlayerData::FootBubblesSound
	 
	
	 * 8: 
	 
	
	 * PlayerData::movingBubblesSound
	 
	
	 * 9: 
	 
	
	 * PlayerData::waterBreathSound
	 
	
	 * 10: 
	 
	
	 * PlayerData::impactSoftSound
	 
	
	 * 11: 
	 
	
	 * PlayerData::impactHardSound
	 
	
	 * 12: 
	 
	
	 * PlayerData::impactMetalSound
	 
	
	 * 13: 
	 
	
	 * PlayerData::impactSnowSound
	 
	
	 * 14: 
	 
	
	 * PlayerData::impactWaterEasy
	 
	
	 * 15: 
	 
	
	 * PlayerData::impactWaterMedium
	 
	
	 * 16: 
	 
	
	 * PlayerData::impactWaterHard
	 
	
	 * 17: 
	 
	
	 * PlayerData::exitingWater

.. cpp:member:: string  Material::getAnimFlags


.. cpp:member:: string  Material::getFilename

	Get filename of material.

.. cpp:member:: bool  Material::glow [4]

	Enables rendering this material to the glow buffer.

.. cpp:member:: int  Material::impactSoundId

	What sound to play from the PlayerData sound list when the player impacts on the surface with a velocity equal or greater than PlayerData::groundImpactMinSpeed . For a list of IDs, see footstepSoundId

.. cpp:member:: bool  Material::isAutoGenerated

	Returns true if this Material was automatically generated by MaterialList::mapMaterials().

.. cpp:member:: filename  Material::lightMap [4]

	The lightmap texture used with pureLight.

.. cpp:member:: string  Material::mapTo

	Used to map this material to the material name used by TSShape.

.. cpp:member:: float  Material::minnaertConstant [4]

	The Minnaert shading constant value. Must be greater than 0 to enable the effect.

.. cpp:member:: filename  Material::normalMap [4]

	The normal map texture. You can use the DXTnm format only when per-pixel specular highlights are disabled, or a specular map is in use.

.. cpp:member:: filename  Material::overlayMap [4]

	A secondary diffuse color texture map which will use the second texcoord of a mesh.

.. cpp:member:: filename  Material::overlayTex [4]

	For backwards compatibility.

.. cpp:member:: float  Material::parallaxScale [4]

	Enables parallax mapping and defines the scale factor for the parallax effect. Typically this value is less than 0.4 else the effect breaks down.

.. cpp:member:: bool  Material::pixelSpecular [4]

	This enables per-pixel specular highlights controlled by the alpha channel of the normal map texture. Note that if pixel specular is enabled the DXTnm format will not work with your normal map, unless you are also using a specular map.

.. cpp:member:: bool  Material::planarReflection


.. cpp:member:: void  Material::reload

	Reloads all material instances that use this material.

.. cpp:member:: Point2F  Material::rotPivotOffset [4]

	The piviot position in UV coordinates to center the rotation animation.

.. cpp:member:: float  Material::rotSpeed [4]

	The speed to rotate the texture in degrees per second when rotation animation is enabled.

.. cpp:member:: Point2F  Material::scrollDir [4]

	The scroll direction in UV space when scroll animation is enabled.

.. cpp:member:: float  Material::scrollSpeed [4]

	The speed to scroll the texture in UVs per second when scroll animation is enabled.

.. cpp:member:: float  Material::sequenceFramePerSec [4]

	The number of frames per second for frame based sequence animations if greater than zero.

.. cpp:member:: float  Material::sequenceSegmentSize [4]

	The size of each frame in UV units for sequence animations.

.. cpp:member:: void  Material::setAutoGenerated

	setAutoGenerated(bool isAutoGenerated): Set whether or not the Material is autogenerated.

.. cpp:member:: bool  Material::showDust

	Whether to emit dust particles from a shape moving over the material. This is, for example, used by vehicles or players to decide whether to show dust trails.

.. cpp:member:: bool  Material::showFootprints

	Whether to show player footprint decals on this material.

.. cpp:member:: ColorF  Material::specular [4]

	The color of the specular highlight when not using a specularMap.

.. cpp:member:: filename  Material::specularMap [4]

	The specular map texture. The RGB channels of this texture provide a per-pixel replacement for the 'specular' parameter on the material. If this texture contains alpha information, the alpha channel of the texture will be used as the gloss map. This provides a per-pixel replacement for the 'specularPower' on the material.

.. cpp:member:: float  Material::specularPower [4]

	The hardness of the specular highlight when not using a specularMap.

.. cpp:member:: float  Material::specularStrength [4]

	The strength of the specular highlight when not using a specularMap.

.. cpp:member:: bool  Material::subSurface [4]

	Enables the subsurface scattering approximation.

.. cpp:member:: ColorF  Material::subSurfaceColor [4]

	The color used for the subsurface scattering approximation.

.. cpp:member:: float  Material::subSurfaceRolloff [4]

	The 0 to 1 rolloff factor used in the subsurface scattering approximation.

.. cpp:member:: filename  Material::toneMap [4]

	The tonemap texture used with pureLight.

.. cpp:member:: bool  Material::translucent

	If true this material is translucent blended.

.. cpp:member:: MaterialBlendOp Material::translucentBlendOp

	The type of blend operation to use when the material is translucent.

.. cpp:member:: bool  Material::translucentZWrite

	If enabled and the material is translucent it will write into the depth buffer.

.. cpp:member:: bool  Material::useAnisotropic [4]

	Use anisotropic filtering for the textures of this stage.

.. cpp:member:: bool  Material::vertColor [4]

	If enabled, vertex colors are premultiplied with diffuse colors.

.. cpp:member:: bool  Material::vertLit [4]

	If true the vertex color is used for lighting.

.. cpp:member:: float  Material::waveAmp [4]

	The wave amplitude when wave animation is enabled.

.. cpp:member:: float  Material::waveFreq [4]

	The wave frequency when wave animation is enabled.

.. cpp:member:: MaterialWaveType Material::waveType [4]

	The type of wave animation to perform when wave animation is enabled.
