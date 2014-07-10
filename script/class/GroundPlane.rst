GroundPlane
===========

An infinite plane extending in all direction.

Inherit:
	:doc:`SceneObject`

Description
-----------

An infinite plane extending in all direction.

GroundPlane is useful for setting up simple testing scenes, or it can be placed under an existing scene to keep objects from falling into 'nothing'.

GroundPlane may not be moved or rotated, it is always at the world origin.


Methods
-------


.. cpp:function:: void GroundPlane::postApply()

	Intended as a helper to developers and editor scripts. Force trigger an inspectPostApply. This will transmit material and other fields to client objects.

Fields
------


.. cpp:member:: string  GroundPlane::Material

	Name of Material used to render GroundPlane's surface.

.. cpp:member:: float  GroundPlane::scaleU

	Scale of texture repeat in the U direction.

.. cpp:member:: float  GroundPlane::scaleV

	Scale of texture repeat in the V direction.

.. cpp:member:: float  GroundPlane::squareSize

	Square size in meters to which GroundPlane subdivides its geometry.
