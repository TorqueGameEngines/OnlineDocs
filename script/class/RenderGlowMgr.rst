RenderGlowMgr
=============

A render bin for the glow pass.

Inherit:
	:doc:`RenderTexTargetBinManager`

Description
-----------

When the glow buffer PostEffect is enabled this bin gathers mesh render instances with glow materials and renders them to the glowbuffer offscreen render target.

This render target is then used by the 'GlowPostFx' PostEffect to blur and render the glowing portions of the screen.

