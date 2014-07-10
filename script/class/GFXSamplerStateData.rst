GFXSamplerStateData
===================

A sampler state used by GFXStateBlockData.

Inherit:
	:doc:`SimObject`

Description
-----------

The samplers define how a texture will be sampled when used from the shader or fixed function device.

Example::

	singleton GFXSamplerStateData(SamplerClampLinear)
	{
	   textureColorOp = GFXTOPModulate;
	   addressModeU = GFXAddressClamp;
	   addressModeV = GFXAddressClamp;
	   addressModeW = GFXAddressClamp;
	   magFilter = GFXTextureFilterLinear;
	   minFilter = GFXTextureFilterLinear;
	   mipFilter = GFXTextureFilterLinear;
	};

There are a few predefined samplers in the core scripts which you can use with GFXStateBlockData for the most common rendering cases:

* SamplerClampLinear
* SamplerClampPoint
* SamplerWrapLinear
* SamplerWrapPoint

Fields
------

.. cpp:member:: GFXTextureAddressMode GFXSamplerStateData::addressModeU

	The texture address mode for the u coordinate. The default is GFXAddressWrap.

.. cpp:member:: GFXTextureAddressMode GFXSamplerStateData::addressModeV

	The texture address mode for the v coordinate. The default is GFXAddressWrap.

.. cpp:member:: GFXTextureAddressMode GFXSamplerStateData::addressModeW

	The texture address mode for the w coordinate. The default is GFXAddressWrap.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::alphaArg1

	The first alpha argument for the texture stage. The default value is GFXTATexture.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::alphaArg2

	The second alpha argument for the texture stage. The default value is GFXTADiffuse.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::alphaArg3

	The third alpha channel selector operand for triadic operations (multiply, add, and linearly interpolate). The default value is GFXTACurrent.

.. cpp:member:: GFXTextureOp GFXSamplerStateData::alphaOp

	The texture alpha blending operation. The default value is GFXTOPModulate.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::colorArg1

	The first color argument for the texture stage. The default value is GFXTACurrent.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::colorArg2

	The second color argument for the texture stage. The default value is GFXTATexture.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::colorArg3

	The third color argument for triadic operations (multiply, add, and linearly interpolate). The default value is GFXTACurrent.

.. cpp:member:: GFXTextureFilterType GFXSamplerStateData::magFilter

	The texture magnification filter. The default is GFXTextureFilterLinear.

.. cpp:member:: int  GFXSamplerStateData::maxAnisotropy

	The maximum texture anisotropy. The default value is 1.

.. cpp:member:: GFXTextureFilterType GFXSamplerStateData::minFilter

	The texture minification filter. The default is GFXTextureFilterLinear.

.. cpp:member:: GFXTextureFilterType GFXSamplerStateData::mipFilter

	The texture mipmap filter used during minification. The default is GFXTextureFilterLinear.

.. cpp:member:: float  GFXSamplerStateData::mipLODBias

	The mipmap level of detail bias. The default value is zero.

.. cpp:member:: GFXTextureArgument GFXSamplerStateData::resultArg

	The selection of the destination register for the result of this stage. The default is GFXTACurrent.

.. cpp:member:: GFXTextureOp GFXSamplerStateData::textureColorOp

	The texture color blending operation. The default value is GFXTOPDisable which disables the sampler.

.. cpp:member:: GFXTextureTransformFlags GFXSamplerStateData::textureTransform

	Sets the texture transform state. The default is GFXTTFFDisable.
