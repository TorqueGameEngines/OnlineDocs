RenderPassManager
=================

A grouping of render bin managers which forms a render pass.

Inherit:
	:doc:`SimObject`

Description
-----------

The render pass is used to order a set of RenderBinManager objects which are used when rendering a scene. This class does little work itself other than managing its list of render bins.

In 'core/scripts/client/renderManager.cs' you will find the DiffuseRenderPassManager which is used by the C++ engine to render the scene.

Methods
-------

.. cpp:function:: void RenderPassManager::addManager(RenderBinManager renderBin)

	Add as a render bin manager to the pass.

.. cpp:function:: RenderBinManager  RenderPassManager::getManager(int index)

	Returns the render bin manager at the index or null if the index is out of range.

.. cpp:function:: int RenderPassManager::getManagerCount()

	Returns the total number of bin managers.

.. cpp:function:: void RenderPassManager::removeManager(RenderBinManager renderBin)

	Removes a render bin manager.
