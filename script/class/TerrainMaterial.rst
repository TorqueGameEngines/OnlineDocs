TerrainMaterial
===============

The TerrainMaterial class orginizes the material settings for a single terrain material layer.

Inherit:
	:doc:`SimObject`

Description
-----------

The TerrainMaterial class orginizes the material settings for a single terrain material layer.

Example::

	// Created by the Terrain Painter tool in the World EditornewTerrainMaterial()
	{
	   internalName = "grass1";
	   diffuseMap = "art/terrains/Test/grass1";
	   detailMap = "art/terrains/Test/grass1_d";
	   detailSize = "10";
	   isManaged = "1";
	   detailBrightness = "1";
	   Enabled = "1";
	   diffuseSize = "200";
	};

Fields
------

.. cpp:member:: float  TerrainMaterial::detailDistance

	Changes how far camera can see the detail map rendering on the material.

.. cpp:member:: filename  TerrainMaterial::detailMap

	Detail map for the material.

.. cpp:member:: float  TerrainMaterial::detailSize

	Used to scale the detail map to the material square.

.. cpp:member:: float  TerrainMaterial::detailStrength

	Exponentially sharpens or lightens the detail map rendering on the material.

.. cpp:member:: filename  TerrainMaterial::diffuseMap

	Base texture for the material.

.. cpp:member:: float  TerrainMaterial::diffuseSize

	Used to scale the diffuse map to the material square.

.. cpp:member:: float  TerrainMaterial::macroDistance

	Changes how far camera can see the Macro map rendering on the material.

.. cpp:member:: filename  TerrainMaterial::macroMap

	Macro map for the material.

.. cpp:member:: float  TerrainMaterial::macroSize

	Used to scale the Macro map to the material square.

.. cpp:member:: float  TerrainMaterial::macroStrength

	Exponentially sharpens or lightens the Macro map rendering on the material.

.. cpp:member:: filename  TerrainMaterial::normalMap

	Bump map for the material.

.. cpp:member:: float  TerrainMaterial::parallaxScale

	Used to scale the height from the normal map to give some self occlusion effect (aka parallax) to the terrain material.

.. cpp:member:: bool  TerrainMaterial::useSideProjection

	Makes that terrain material project along the sides of steep slopes instead of projected downwards.
