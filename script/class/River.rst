River
=====

A water volume defined by a 3D spline.

Inherit:
	:doc:`WaterObject`

Description
-----------

A water volume defined by a 3D spline.

User may control width and depth per node and overall spline shape in three dimensions.

River supports dynamic planar reflections (fullReflect) like all WaterObject classes, but keep in mind it is not necessarily a planar surface. For best visual quality a River should be less reflective the more it twists and bends. This caution only applies to Rivers with fullReflect on.


Methods
-------


.. cpp:function:: void River::regenerate()

	Intended as a helper to developers and editor scripts. Force River to recreate its geometry.

.. cpp:function:: void River::setBatchSize(float meters)

	Intended as a helper to developers and editor scripts. BatchSize is not currently used.

.. cpp:function:: void River::setMaxDivisionSize(float meters)

	Intended as a helper to developers and editor scripts.

.. cpp:function:: void River::setMetersPerSegment(float meters)

	Intended as a helper to developers and editor scripts.

.. cpp:function:: void River::setNodeDepth(int idx, float meters)

	Intended as a helper to developers and editor scripts. Sets the depth in meters of a particular node.

Fields
------


.. cpp:member:: bool  River::EditorOpen  [static]

	For editor use.

.. cpp:member:: float  River::FlowMagnitude

	Magnitude of the force vector applied to dynamic objects within the River .

.. cpp:member:: float  River::LowLODDistance

	Segments of the river at this distance in meters or greater will render as a single unsubdivided without undulation effects.

.. cpp:member:: string  River::Node

	For internal use, do not modify.

.. cpp:member:: float  River::SegmentLength

	Divide the River lengthwise into segments of this length in meters. These geometric volumes are used for spacial queries like determining containment.

.. cpp:member:: bool  River::showNodes  [static]

	For editor use.

.. cpp:member:: bool  River::showRiver  [static]

	For editor use.

.. cpp:member:: bool  River::showSpline  [static]

	For editor use.

.. cpp:member:: bool  River::showWalls  [static]

	For editor use.

.. cpp:member:: bool  River::showWireframe  [static]

	For editor use.

.. cpp:member:: float  River::SubdivideLength

	For purposes of generating the renderable geometry River segments are further subdivided such that no quad is of greater width or length than this distance in meters.
