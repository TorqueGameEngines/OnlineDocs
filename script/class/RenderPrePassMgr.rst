RenderPrePassMgr
================

The render bin which performs a z+normals prepass used in Advanced Lighting.

Inherit:
	:doc:`RenderTexTargetBinManager`

Description
-----------

This render bin is used in Advanced Lighting to gather all opaque mesh render instances and render them to the g-buffer for use in lighting the scene and doing effects.

PostEffect and other shaders can access the output of this bin by using the prepass texture target name. See the edge anti-aliasing post effect for an example.

