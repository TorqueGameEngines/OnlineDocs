Terrain
=======

Objects that specialize in representing terrain and other collidable/walkable surfaces.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/DecalRoad
	class/GroundPlane
	class/MeshRoad
	class/TerrainBlock

Functions
---------

.. cpp:function:: bool getTerrainHeight(Point2I position)

	Gets the terrain height at the specified position.

	:param position: The world space point, minus the z (height) value. Formatted as ("x y")

	:return: Returns the terrain height at the given point as an F32 value. 

.. cpp:function:: bool getTerrainHeight(F32 x, F32 y)

	Gets the terrain height at the specified position.

	:param x: The X coordinate in world space
	:param y: The Y coordinate in world space

	:return: Returns the terrain height at the given point as an F32 value. 

.. cpp:function:: bool getTerrainHeightBelowPosition(Point2I position)

	Takes a world point and find the "highest" terrain underneath it.

	:param position: The world space point, minus the z (height) value. Formatted as ("x y")

	:return: Returns the closest terrain height below the given point as an F32 value. 

.. cpp:function:: bool getTerrainHeightBelowPosition(F32 x, F32 y)

	Takes a world point and find the "highest" terrain underneath it.

	:param x: The X coordinate in world space
	:param y: The Y coordinate in world space

	:return: Returns the closest terrain height below the given point as an F32 value. 

.. cpp:function:: bool getTerrainUnderWorldPoint(Point3F position)

	Gets the terrain block that is located under the given world point.

	:param position: The world space coordinate you wish to query at. Formatted as ("x y z")

	:return: Returns the ID of the requested terrain block (0 if not found). 

.. cpp:function:: bool getTerrainUnderWorldPoint(F32 x, F32 y, F32 z)

	Takes a world point and find the "highest" terrain underneath it.

	:param x: The X coordinate in world space
	:param y: The Y coordinate in world space
	:param z: The Z coordinate in world space

	:return: Returns the ID of the requested terrain block (0 if not found). 

Variables
---------

.. cpp:member:: bool  TerrainBlock::debugRender  [static, inherited]

	Triggers debug rendering of terrain cells.

.. cpp:member:: float $pref::Terrain::detailScale

	A global detail scale used to tweak the material detail distances.

.. cpp:member:: float $pref::Terrain::lodScale

	A global LOD scale used to tweak the default terrain screen error value.
