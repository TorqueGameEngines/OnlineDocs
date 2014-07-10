CustomMaterial
==============

Material object which provides more control over surface properties.

Inherit:
	:doc:`Material`

Description
-----------

CustomMaterials allow the user to specify their own shaders via the ShaderData datablock. Because CustomMaterials are derived from Materials, they can hold a lot of the same properties. It is up to the user to code how these properties are used.

Example::

	singleton CustomMaterial( WaterBasicMat )
	{
	   sampler["reflectMap"] = "$reflectbuff";
	   sampler["refractBuff"] = "$backbuff";
	
	   cubemap = NewLevelSkyCubemap;
	   shader = WaterBasicShader;
	   stateBlock = WaterBasicStateBlock;
	   version = 2.0;
	};

Fields
------

.. cpp:member:: Material CustomMaterial::fallback

	Alternate material for targeting lower end hardware. If the CustomMaterial requires a higher pixel shader version than the one it's using, it's fallback Material will be processed instead. If the fallback material wasn't defined, Torque 3D will assert and attempt to use a very basic material in it's place.

.. cpp:member:: bool  CustomMaterial::forwardLit

	Determines if the material should recieve lights in Basic Lighting. Has no effect in Advanced Lighting.

.. cpp:member:: string  CustomMaterial::shader

	Name of the ShaderData to use for this effect.

.. cpp:member:: GFXStateBlockData CustomMaterial::stateBlock

	Name of a GFXStateBlockData for this effect.

.. cpp:member:: string  CustomMaterial::target

	String identifier of this material's target texture.

.. cpp:member:: float  CustomMaterial::version

	Specifies pixel shader version for hardware. Valid pixel shader versions include 2.0, 3.0, etc.
