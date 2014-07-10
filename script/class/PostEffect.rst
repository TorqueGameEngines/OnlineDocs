PostEffect
==========

A fullscreen shader effect.

Inherit:
	:doc:`SimGroup`

Description
-----------

A fullscreen shader effect.

PFXTextureIdentifiers
---------------------


Methods
-------


.. cpp:function:: void PostEffect::clearShaderMacros()

	Remove all shader macros.

.. cpp:function:: void PostEffect::disable()

	Disables the effect.

.. cpp:function:: String PostEffect::dumpShaderDisassembly()

	Dumps this PostEffect shader's disassembly to a temporary text file.

	:return: Full path to the dumped file or an empty string if failed. 

.. cpp:function:: void PostEffect::enable()

	Enables the effect.

.. cpp:function:: float PostEffect::getAspectRatio()


	:return: Width over height of the backbuffer. 

.. cpp:function:: bool  PostEffect::isEnabled()


	:return: True if the effect is enabled. 

.. cpp:function:: void PostEffect::onAdd()

	Called when this object is first created and registered.

.. cpp:function:: void PostEffect::onDisabled()

	Called when this effect becomes disabled.

.. cpp:function:: bool PostEffect::onEnabled()

	Called when this effect becomes enabled. If the user returns false from this callback the effect will not be enabled.

	:return: True to allow this effect to be enabled. 

.. cpp:function:: void PostEffect::preProcess()

	Called when an effect is processed but before textures are bound. This allows the user to change texture related paramaters or macros at runtime.

	Example::

		function SSAOPostFx::preProcess( %this )
		{
		   if ( $SSAOPostFx::quality !$= %this.quality )
		   {
		      %this.quality = mClamp( mRound( $SSAOPostFx::quality ), 0, 2 );
		      
		      %this.setShaderMacro( "QUALITY", %this.quality );
		   }
		   %this.targetScale = $SSAOPostFx::targetScale;
		}

.. cpp:function:: void PostEffect::reload()

	Reloads the effect shader and textures.

.. cpp:function:: void PostEffect::removeShaderMacro(string key)

	Remove a shader macro. This will usually be called within the preProcess callback.

	:param key: Macro to remove.

.. cpp:function:: void PostEffect::setShaderConst(string name, string value)

	Sets the value of a uniform defined in the shader. This will usually be called within the setShaderConsts callback. Array type constants are not supported.

	:param name: Name of the constanst, prefixed with '$'.
	:param value: Value to set, space seperate values with more than one element.

	Example::

		function MyPfx::setShaderConsts( %this )
		{
		   // example float4 uniform
		   %this.setShaderConst( "$colorMod", "1.0 0.9 1.0 1.0" );
		   // example float1 uniform
		   %this.setShaderConst( "$strength", "3.0" );
		   // example integer uniform
		   %this.setShaderConst( "$loops", "5" );}

.. cpp:function:: void PostEffect::setShaderConsts()

	Called immediate before processing this effect. This is the user's chance to set the value of shader uniforms (constants).

.. cpp:function:: void PostEffect::setShaderMacro(string key, string value)

	Adds a macro to the effect's shader or sets an existing one's value. This will usually be called within the onAdd or preProcess callback.

	:param key: lval of the macro.
	:param value: rval of the macro, or may be empty.

	Example::

		function MyPfx::onAdd( %this )
		{
		   %this.setShaderMacro( "NUM_SAMPLES", "10" );
		   %this.setShaderMacro( "HIGH_QUALITY_MODE" );
		   
		   // In the shader looks like... // #define NUM_SAMPLES 10// #define HIGH_QUALITY_MODE
		}

.. cpp:function:: void PostEffect::setTexture(int index, string filePath)

	This is used to set the texture file and load the texture on a running effect. If the texture file is not different from the current file nothing is changed. If the texture cannot be found a null texture is assigned.

	:param index: The texture stage index.
	:param filePath: The file name of the texture to set.

.. cpp:function:: bool PostEffect::toggle()

	Toggles the effect between enabled / disabled.

	:return: True if effect is enabled. 

Fields
------


.. cpp:member:: bool  PostEffect::allowReflectPass

	Is this effect processed during reflection render passes.

.. cpp:member:: bool  PostEffect::isEnabled

	Is the effect on.

.. cpp:member:: bool  PostEffect::oneFrameOnly

	Allows you to turn on a PostEffect for only a single frame.

.. cpp:member:: bool  PostEffect::onThisFrame

	Allows you to turn on a PostEffect for only a single frame.

.. cpp:member:: string  PostEffect::renderBin

	Name of a renderBin, used if renderTime is PFXBeforeBin or PFXAfterBin.

.. cpp:member:: float  PostEffect::renderPriority

	PostEffects are processed in DESCENDING order of renderPriority if more than one has the same renderBin/Time.

.. cpp:member:: PFXRenderTime PostEffect::renderTime

	When to process this effect during the frame.

.. cpp:member:: string  PostEffect::shader

	Name of a GFXShaderData for this effect.

.. cpp:member:: bool  PostEffect::skip

	Skip processing of this PostEffect and its children even if its parent is enabled. Parent and sibling PostEffects in the chain are still processed.

.. cpp:member:: GFXStateBlockData PostEffect::stateBlock

	Name of a GFXStateBlockData for this effect.

.. cpp:member:: string  PostEffect::target

	String identifier of this effect's target texture.

.. cpp:member:: PFXTargetClear PostEffect::targetClear

	Describes when the target texture should be cleared.

.. cpp:member:: ColorF  PostEffect::targetClearColor

	Color to which the target texture is cleared before rendering.

.. cpp:member:: string  PostEffect::targetDepthStencil

	Optional string identifier for this effect's target depth/stencil texture.

.. cpp:member:: GFXFormat PostEffect::targetFormat

	Format of the target texture, not applicable if writing to the backbuffer.

.. cpp:member:: Point2F  PostEffect::targetScale

	If targetSize is zero this is used to set a relative size from the current target.

.. cpp:member:: Point2I  PostEffect::targetSize

	If non-zero this is used as the absolute target size.

.. cpp:member:: PFXTargetViewport PostEffect::targetViewport

	Specifies how the viewport should be set up for a target texture.

.. cpp:member:: filename  PostEffect::texture [6]

	Input textures to this effect ( samplers ).
