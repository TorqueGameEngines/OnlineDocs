RenderObjectExample
===================

An example scene object which renders using a callback.

Inherit:
	:doc:`SceneObject`

Description
-----------

This class implements a basic SceneObject that can exist in the world at a 3D position and render itself. Note that RenderObjectExample handles its own rendering by submitting itself as an ObjectRenderInst (see renderInstance enderPassmanager.h) along with a delegate for its render() function. However, the preffered rendering method in the engine is to submit a MeshRenderInst along with a Material, vertex buffer, primitive buffer, and transform and allow the RenderMeshMgr handle the actual rendering. You can see this implemented in RenderMeshExample.

See the C++ code for implementation details.

