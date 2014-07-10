GFXStateBlockData
=================

A state block description for rendering.

Inherit:
	:doc:`SimObject`

Description
-----------

This object is used with ShaderData in CustomMaterial and PostEffect to define the render state.

Example::

	singleton GFXStateBlockData( PFX_DOFDownSampleStateBlock )
	{
	   zDefined = true;
	   zEnable = false;
	   zWriteEnable = false;
	
	   samplersDefined = true;
	   samplerStates[0] = SamplerClampLinear;
	   samplerStates[1] = SamplerClampPoint;
	
	   // Copy the clamped linear sampler, but change
	   // the u coord to wrap for this special case.
	   samplerStates[2] = newGFXSamplerStateData( : SamplerClampLinear )
	   {
	      addressModeU = GFXAddressWrap;
	   };
	};

Fields
------

.. cpp:member:: bool  GFXStateBlockData::alphaDefined

	Set to true if the alpha test state is not all defaults.

.. cpp:member:: bool  GFXStateBlockData::alphaTestEnable

	Enables per-pixel alpha testing. The default is false.

.. cpp:member:: GFXCmpFunc GFXStateBlockData::alphaTestFunc

	The test function used to accept or reject a pixel based on its alpha value. The default is GFXCmpGreaterEqual.

.. cpp:member:: int  GFXStateBlockData::alphaTestRef

	The reference alpha value against which pixels are tested. The default is zero.

.. cpp:member:: bool  GFXStateBlockData::blendDefined

	Set to true if the alpha blend state is not all defaults.

.. cpp:member:: GFXBlend GFXStateBlockData::blendDest

	The destination blend state. The default is GFXBlendZero.

.. cpp:member:: bool  GFXStateBlockData::blendEnable

	Enables alpha blending. The default is false.

.. cpp:member:: GFXBlendOp GFXStateBlockData::blendOp

	The arithmetic operation applied to alpha blending. The default is GFXBlendOpAdd.

.. cpp:member:: GFXBlend GFXStateBlockData::blendSrc

	The source blend state. The default is GFXBlendOne.

.. cpp:member:: bool  GFXStateBlockData::colorWriteAlpha

	Enables alpha channel writes. The default is true.

.. cpp:member:: bool  GFXStateBlockData::colorWriteBlue

	Enables blue channel writes. The default is true.

.. cpp:member:: bool  GFXStateBlockData::colorWriteDefined

	Set to true if the color write state is not all defaults.

.. cpp:member:: bool  GFXStateBlockData::colorWriteGreen

	Enables green channel writes. The default is true.

.. cpp:member:: bool  GFXStateBlockData::colorWriteRed

	Enables red channel writes. The default is true.

.. cpp:member:: bool  GFXStateBlockData::cullDefined

	Set to true if the culling state is not all defaults.

.. cpp:member:: GFXCullMode GFXStateBlockData::cullMode

	Defines how back facing triangles are culled if at all. The default is GFXCullCCW.

.. cpp:member:: bool  GFXStateBlockData::ffLighting

	Enables fixed function lighting when rendering without a shader on geometry with vertex normals. The default is false.

.. cpp:member:: bool  GFXStateBlockData::samplersDefined

	Set to true if the sampler states are not all defaults.

.. cpp:member:: GFXSamplerStateData GFXStateBlockData::samplerStates [16]

	The array of texture sampler states.

.. cpp:member:: bool  GFXStateBlockData::separateAlphaBlendDefined

	Set to true if the seperate alpha blend state is not all defaults.

.. cpp:member:: GFXBlend GFXStateBlockData::separateAlphaBlendDest

	The destination blend state. The default is GFXBlendZero.

.. cpp:member:: bool  GFXStateBlockData::separateAlphaBlendEnable

	Enables the separate blend mode for the alpha channel. The default is false.

.. cpp:member:: GFXBlendOp GFXStateBlockData::separateAlphaBlendOp

	The arithmetic operation applied to separate alpha blending. The default is GFXBlendOpAdd.

.. cpp:member:: GFXBlend GFXStateBlockData::separateAlphaBlendSrc

	The source blend state. The default is GFXBlendOne.

.. cpp:member:: bool  GFXStateBlockData::stencilDefined

	Set to true if the stencil state is not all defaults.

.. cpp:member:: bool  GFXStateBlockData::stencilEnable

	Enables stenciling. The default is false.

.. cpp:member:: GFXStencilOp GFXStateBlockData::stencilFailOp

	The stencil operation to perform if the stencil test fails. The default is GFXStencilOpKeep.

.. cpp:member:: GFXCmpFunc GFXStateBlockData::stencilFunc

	The comparison function to test the reference value to a stencil buffer entry. The default is GFXCmpNever.

.. cpp:member:: int  GFXStateBlockData::stencilMask

	The mask applied to the reference value and each stencil buffer entry to determine the significant bits for the stencil test. The default is 0xFFFFFFFF.

.. cpp:member:: GFXStencilOp GFXStateBlockData::stencilPassOp

	The stencil operation to perform if both the stencil and the depth tests pass. The default is GFXStencilOpKeep.

.. cpp:member:: int  GFXStateBlockData::stencilRef

	The reference value for the stencil test. The default is zero.

.. cpp:member:: int  GFXStateBlockData::stencilWriteMask

	The write mask applied to values written into the stencil buffer. The default is 0xFFFFFFFF.

.. cpp:member:: GFXStencilOp GFXStateBlockData::stencilZFailOp

	The stencil operation to perform if the stencil test passes and the depth test fails. The default is GFXStencilOpKeep.

.. cpp:member:: ColorI  GFXStateBlockData::textureFactor

	The color used for multiple-texture blending with the GFXTATFactor texture-blending argument or the GFXTOPBlendFactorAlpha texture-blending operation. The default is opaque white (255, 255, 255, 255).

.. cpp:member:: bool  GFXStateBlockData::vertexColorEnable

	Enables fixed function vertex coloring when rendering without a shader. The default is false.

.. cpp:member:: float  GFXStateBlockData::zBias

	A floating-point bias used when comparing depth values. The default is zero.

.. cpp:member:: bool  GFXStateBlockData::zDefined

	Set to true if the depth state is not all defaults.

.. cpp:member:: bool  GFXStateBlockData::zEnable

	Enables z-buffer reads. The default is true.

.. cpp:member:: GFXCmpFunc GFXStateBlockData::zFunc

	The depth comparision function which a pixel must pass to be written to the z-buffer. The default is GFXCmpLessEqual.

.. cpp:member:: float  GFXStateBlockData::zSlopeBias

	An additional floating-point bias based on the maximum depth slop of the triangle being rendered. The default is zero.

.. cpp:member:: bool  GFXStateBlockData::zWriteEnable

	Enables z-buffer writes. The default is true.
