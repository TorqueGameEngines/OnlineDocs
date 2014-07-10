RenderPassStateToken
====================

Abstract base class for RenderFormatToken, used to manipulate what goes on in the render manager.

Inherit:
	:doc:`SimObject`

Description
-----------

You cannot actually instantiate RenderPassToken, only its child: RenderFormatToken. RenderFormatToken is an implementation which changes the format of the back buffer and/or the depth buffer.

The RenderPassStateBin manager changes the rendering state associated with a token it is declared with. In stock Torque 3D, a single example exists in the way of AL_FormatToken (found in renderManager.cs). In that script file, all the render managers are intialized, and a single RenderFormatToken is used. This implementation basically exists to ensure Advanced Lighting works with MSAA.

Methods
-------

.. cpp:function:: void RenderPassStateToken::disable()

	Disables the token.

.. cpp:function:: void RenderPassStateToken::enable()

	Enables the token.

.. cpp:function:: void RenderPassStateToken::toggle()

	Toggles the token from enabled to disabled or vice versa.

Fields
------

.. cpp:member:: bool  RenderPassStateToken::enabled

	Enables or disables this token.
