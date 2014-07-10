RenderMeshExample
=================

An example scene object which renders a mesh.

Inherit:
	:doc:`SceneObject`

Description
-----------

This class implements a basic SceneObject that can exist in the world at a 3D position and render itself. There are several valid ways to render an object in Torque. This class implements the preferred rendering method which is to submit a MeshRenderInst along with a Material, vertex buffer, primitive buffer, and transform and allow the RenderMeshMgr handle the actual setup and rendering for you.

See the C++ code for implementation details.

Methods
-------

.. cpp:function:: void RenderMeshExample::postApply()

	A utility method for forcing a network update.

Fields
------

.. cpp:member:: string  RenderMeshExample::Material

	The name of the material used to render the mesh.
