RenderOcclusionMgr
==================

A render bin which renders occlusion query requests.

Inherit:
	:doc:`RenderBinManager`

Description
-----------

This render bin gathers occlusion query render instances and renders them. It is currently used by light flares and ShapeBase reflection cubemaps.

You can type '$RenderOcclusionMgr::debugRender = true' in the console to see debug rendering of the occlusion geometry.

