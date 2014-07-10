NavPath
=======



Inherit:
	:doc:`SceneObject`

Description
-----------

UNDOCUMENTED!


Methods
-------


.. cpp:function:: int NavPath::getCount()

	Return the number of nodes in this path.

.. cpp:function:: float NavPath::getLength()

	Get the length of this path in Torque units (i.e. the total distance it covers).

.. cpp:function:: Point3F NavPath::getNode(int idx)

	Get a specified node along the path.

.. cpp:function:: bool NavPath::replan()

	Find a path using the already-specified path properties.

Fields
------


.. cpp:member:: bool  NavPath::alwaysRender

	Render this NavPath even when not selected.

.. cpp:member:: Point3F  NavPath::from

	World location this path starts at.

.. cpp:member:: bool  NavPath::isLooping

	Does this path loop?

.. cpp:member:: NavMesh NavPath::mesh

	NavMesh object this path travels within.

.. cpp:member:: Point3F  NavPath::to

	World location this path should end at.

.. cpp:member:: Path NavPath::waypoints

	Path containing waypoints for this NavPath to visit.

.. cpp:member:: bool  NavPath::xray

	Render this NavPath through other objects.
