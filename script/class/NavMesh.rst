NavMesh
=======



Inherit:
	:doc:`SceneObject`

Description
-----------

UNDOCUMENTED!


Methods
-------


.. cpp:function:: bool NavMesh::build(bool background, bool save)

	Create a Recast nav mesh.

.. cpp:function:: void NavMesh::buildTiles(Box3F box)

	Rebuild the tiles overlapped by the input box.

.. cpp:function:: void NavMesh::cancelBuild()

	Cancel the current NavMesh build.

.. cpp:function:: bool NavMesh::load()

	Load this NavMesh from its file.

.. cpp:function:: void NavMesh::save()

	Save this NavMesh to its file.

Fields
------


.. cpp:member:: float  NavMesh::actorClimb

	Maximum climbing height of an actor.

.. cpp:member:: float  NavMesh::actorHeight

	Height of an actor.

.. cpp:member:: float  NavMesh::actorRadius

	Radius of an actor.

.. cpp:member:: bool  NavMesh::alwaysRender

	Display this NavMesh even outside the editor.

.. cpp:member:: int  NavMesh::borderSize

	Size of the non-walkable border around the navigation mesh (in voxels).

.. cpp:member:: float  NavMesh::cellHeight

	Height of a voxel.

.. cpp:member:: float  NavMesh::cellSize

	Length/width of a voxel.

.. cpp:member:: float  NavMesh::detailSampleDist

	Sets the sampling distance to use when generating the detail mesh.

.. cpp:member:: float  NavMesh::detailSampleError

	The maximum distance the detail mesh surface should deviate from heightfield data.

.. cpp:member:: string  NavMesh::fileName

	Name of the data file to store this navmesh in (relative to engine executable).

.. cpp:member:: int  NavMesh::maxEdgeLen

	The maximum allowed length for contour edges along the border of the mesh.

.. cpp:member:: int  NavMesh::maxPolysPerTile

	The maximum number of polygons allowed in a tile.

.. cpp:member:: int  NavMesh::mergeRegionArea

	Any regions with a span count smaller than this value will, if possible, be merged with larger regions.

.. cpp:member:: int  NavMesh::minRegionArea

	The minimum number of cells allowed to form isolated island areas.

.. cpp:member:: float  NavMesh::simplificationError

	The maximum distance a simplfied contour's border edges should deviate from the original raw contour.

.. cpp:member:: float  NavMesh::tileSize

	The horizontal size of tiles.

.. cpp:member:: float  NavMesh::walkableSlope

	Maximum walkable slope in degrees.
