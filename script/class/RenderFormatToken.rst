RenderFormatToken
=================

Used to change the render target format when rendering in AL.

Inherit:
	:doc:`RenderPassStateToken`

Description
-----------

RenderFormatToken is an implementation which changes the format of the back buffer and/or the depth buffer.

The RenderPassStateBin manager changes the rendering state associated with this token. In stock Torque 3D, a single example exists in the way of AL_FormatToken (found in renderManager.cs). In that script file, all the render managers are intialized, and a single RenderFormatToken is used. This implementation basically exists to ensure Advanced Lighting works with MSAA.

The actions for this token toggle the format of the back/depth buffers and it lets you specify a custom shader to "copy" the data so it can be reformatted or altered. This is done through the variables copyEffect and resolveEffect (which are post processes just like fog or glow)

Example::

	// This token, and the associated render managers, ensure that driver MSAA does not get used for Advanced Lighting renders.// The AL_FormatResolve PostEffect copies the result to the backbuffer.newRenderFormatToken(AL_FormatToken)
	{
	   enabled = "false";
	
	   format = "GFXFormatR8G8B8A8";
	   depthFormat = "GFXFormatD24S8";
	   aaLevel = 0; // -1 = match backbuffer
	   // The contents of the back buffer before this format token is executed
	   // is provided in 
	   $inTexcopyEffect = "AL_FormatCopy";
	
	   // The contents of the render target created by this format token is
	   // provided in 
	   $inTexresolveEffect = "AL_FormatCopy";
	};

Fields
------

.. cpp:member:: int  RenderFormatToken::aaLevel

	Anti-ailiasing level for the this token. 0 disables, -1 uses adapter default.

.. cpp:member:: PostEffect RenderFormatToken::copyEffect

	This PostEffect will be run when the render target is changed to the format specified by this token. It is used to copy/format data into the token rendertarget.

.. cpp:member:: GFXFormat RenderFormatToken::depthFormat

	Sets the depth/stencil buffer format for this token.

.. cpp:member:: GFXFormat RenderFormatToken::format

	Sets the color buffer format for this token.

.. cpp:member:: PostEffect RenderFormatToken::resolveEffect

	This PostEffect will be run when the render target is changed back to the format active prior to this token. It is used to copy/format data from the token rendertarget to the backbuffer.
