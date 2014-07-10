TerrainBlock
============

Represent a terrain object in a Torque 3D level.

Inherit:
	:doc:`SceneObject`

Description
-----------

Represent a terrain object in a Torque 3D level.

Example::

	newTerrainBlock(theTerrain)
	{
	   terrainFile = "art/terrains/Deathball Desert_0.ter";
	   squareSize = "2";
	   tile = "0";
	   baseTexSize = "1024";
	   screenError = "16";
	   position = "-1024 -1024 179.978";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	   isRenderEnabled = "true";
	   canSaveDynamicFields = "1";
	};


Methods
-------


.. cpp:function:: bool TerrainBlock::exportHeightMap(string filename)

	export the terrain block's heightmap to a bitmap file (default: png)

.. cpp:function:: bool TerrainBlock::exportLayerMaps(string filePrefix)

	export the terrain block's layer maps to bitmap files (default: png)

.. cpp:function:: int TerrainBlock::import(String terrainName, String heightMap, F32 metersPerPixel, F32 heightScale, String materials, String opacityLayers)


.. cpp:function:: bool TerrainBlock::save(string fileName)

	Saves the terrain block's terrain file to the specified file name.

	:param fileName: Name and path of file to save terrain data to.

	:return: True if file save was successful, false otherwise 

Fields
------


.. cpp:member:: int  TerrainBlock::baseTexSize

	Size of base texture size per meter.

.. cpp:member:: bool  TerrainBlock::castShadows

	Allows the terrain to cast shadows onto itself and other objects.

.. cpp:member:: int  TerrainBlock::createNew

	TerrainBlock.create( String terrainName, U32 resolution, String materialName, bool genNoise ).

.. cpp:member:: int  TerrainBlock::lightMapSize

	Light map dimensions in pixels.

.. cpp:member:: int  TerrainBlock::screenError

	Not yet implemented.

.. cpp:member:: float  TerrainBlock::squareSize

	Indicates the spacing between points on the XY plane on the terrain.

.. cpp:member:: filename  TerrainBlock::terrainFile

	The source terrain data file.
