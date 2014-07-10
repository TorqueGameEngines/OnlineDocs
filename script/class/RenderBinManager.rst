RenderBinManager
================

The abstract base for all render bins.

Inherit:
	:doc:`SimObject`

Description
-----------

The render bins are used by the engine as a high level method to order and batch rendering operations.

Methods
-------

.. cpp:function:: string RenderBinManager::getBinType()

	Returns the bin type string.

Fields
------

.. cpp:member:: string  RenderBinManager::binType

	Sets the render bin type which limits what render instances are added to this bin.

.. cpp:member:: float  RenderBinManager::processAddOrder

	Defines the order for adding instances in relation to other bins.

.. cpp:member:: float  RenderBinManager::renderOrder

	Defines the order for rendering in relation to other bins.
