RenderPassStateBin
==================

A non-rendering render bin used to enable/disable a RenderPassStateToken.

Inherit:
	:doc:`RenderBinManager`

Description
-----------

This is a utility RenderBinManager which does not render any render instances. Its only used to define a point in the render bin order at which a RenderPassStateToken is triggered.

Fields
------

.. cpp:member:: RenderPassStateToken RenderPassStateBin::stateToken

