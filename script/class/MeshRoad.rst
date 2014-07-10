MeshRoad
========

A strip of rectangular mesh segments defined by a 3D spline for prototyping road-shaped objects in your scene.

Inherit:
	:doc:`SceneObject`

Description
-----------

A strip of rectangular mesh segments defined by a 3D spline for prototyping road-shaped objects in your scene.

User may control width and depth per node, overall spline shape in three dimensions, and seperate Materials for rendering the top, bottom, and side surfaces.

MeshRoad is not capable of handling intersections, branches, curbs, or other desirable features in a final 'road' asset and is therefore intended for prototyping and experimentation.

Materials assigned to MeshRoad should tile vertically.


Methods
-------


.. cpp:function:: void MeshRoad::postApply()

	Intended as a helper to developers and editor scripts. Force trigger an inspectPostApply. This will transmit material and other fields ( not including nodes ) to client objects.

.. cpp:function:: void MeshRoad::regenerate()

	Intended as a helper to developers and editor scripts. Force MeshRoad to recreate its geometry.

.. cpp:function:: void MeshRoad::setNodeDepth(int idx, float meters)

	Intended as a helper to developers and editor scripts. Sets the depth in meters of a particular node.

Fields
------


.. cpp:member:: string  MeshRoad::bottomMaterial

	Material for the bottom surface of the road.

.. cpp:member:: float  MeshRoad::breakAngle

	Angle in degrees - MeshRoad will subdivide the spline if its curve is greater than this threshold.

.. cpp:member:: bool  MeshRoad::EditorOpen  [static]

	True if the MeshRoad editor is open, otherwise false.

.. cpp:member:: string  MeshRoad::Node

	Do not modify, for internal use.

.. cpp:member:: bool  MeshRoad::showBatches  [static]

	Determines if the debug rendering of the batches cubes is displayed or not.

.. cpp:member:: bool  MeshRoad::showRoad  [static]

	If true, the road will be rendered. When in the editor, roads are always rendered regardless of this flag.

.. cpp:member:: bool  MeshRoad::showSpline  [static]

	If true, the spline on which the curvature of this road is based will be rendered.

.. cpp:member:: string  MeshRoad::sideMaterial

	Material for the left, right, front, and back surfaces of the road.

.. cpp:member:: float  MeshRoad::textureLength

	The length in meters of textures mapped to the MeshRoad .

.. cpp:member:: string  MeshRoad::topMaterial

	Material for the upper surface of the road.

.. cpp:member:: int  MeshRoad::widthSubdivisions

	Subdivide segments widthwise this many times when generating vertices.

.. cpp:member:: bool  MeshRoad::wireframe  [static]

	If true, will render the wireframe of the road.
