TSStatic
========

A static object derived from a 3D model file and placed within the game world.

Inherit:
	:doc:`SceneObject`

Description
-----------

A static object derived from a 3D model file and placed within the game world.

TSStatic is the most basic 3D shape in Torque. Unlike StaticShape it doesn't make use of a datablock. It derrives directly from SceneObject. This makes TSStatic extremely light weight, which is why the Tools use this class when you want to drop in a DTS or DAE object.

While a TSStatic doesn't provide any motion -- it stays were you initally put it -- it does allow for a single ambient animation sequence to play when the object is first added to the scene.

Example::

	newTSStatic(Team1Base) {
	   shapeName = "art/shapes/desertStructures/station01.dts";
	   playAmbient = "1";
	   receiveSunLight = "1";
	   receiveLMLighting = "1";
	   useCustomAmbientLighting = "0";
	   customAmbientLighting = "0 0 0 1";
	   collisionType = "Visible Mesh";
	   decalType = "Collision Mesh";
	   allowPlayerStep = "1";
	   renderNormals = "0";
	   forceDetail = "-1";
	   position = "315.18 -180.418 244.313";
	   rotation = "0 0 1 195.952";
	   scale = "1 1 1";
	   isRenderEnabled = "true";
	   canSaveDynamicFields = "1";
	};


Methods
-------


.. cpp:function:: void TSStatic::changeMaterial(string mapTo, Material oldMat, Material newMat)

	Change one of the materials on the shape. This method changes materials per mapTo with others. The material that is being replaced is mapped to unmapped_mat as a part of this transition.

	:param mapTo: the name of the material target to remap (from getTargetName)
	:param oldMat: the old Material that was mapped
	:param newMat: the new Material to map

	Example::

		// remap the first material in the shape
		%mapTo = %obj.getTargetName( 0 );
		%obj.changeMaterial( %mapTo, 0, MyMaterial );

.. cpp:function:: string TSStatic::getModelFile()

	Get the model filename used by this shape.

	:return: the shape filename

	Example::

		// Acquire the model filename used on this shape.
		%modelFilename = %obj.getModelFile();

.. cpp:function:: int TSStatic::getTargetCount()

	Get the number of materials in the shape.

	:return: the number of materials in the shape. 

.. cpp:function:: string TSStatic::getTargetName(int index)

	Get the name of the indexed shape material.

	:param index: index of the material to get (valid range is 0 - getTargetCount()-1).

	:return: the name of the indexed material. 

Fields
------


.. cpp:member:: bool  TSStatic::allowPlayerStep

	Allow a Player to walk up sloping polygons in the TSStatic (based on the collisionType). When set to false, the slightest bump will stop the player from walking on top of the object.

.. cpp:member:: TSMeshType TSStatic::collisionType

	The type of mesh data to use for collision queries.

.. cpp:member:: TSMeshType TSStatic::decalType

	The type of mesh data used to clip decal polygons against.

.. cpp:member:: int  TSStatic::forceDetail

	Forces rendering to a particular detail level.

.. cpp:member:: bool  TSStatic::meshCulling

	Enables detailed culling of meshes within the TSStatic . Should only be used with large complex shapes like buildings which contain many submeshes.

.. cpp:member:: bool  TSStatic::originSort

	Enables translucent sorting of the TSStatic by its origin instead of the bounds.

.. cpp:member:: bool  TSStatic::playAmbient

	Enables automatic playing of the animation sequence named "ambient" (if it exists) when the TSStatic is loaded.

.. cpp:member:: float  TSStatic::renderNormals

	Debug rendering mode shows the normals for each point in the TSStatic's mesh.

.. cpp:member:: filename  TSStatic::shapeName

	Path and filename of the model file (.DTS, .DAE) to use for this TSStatic .

.. cpp:member:: string  TSStatic::skin

	The skin applied to the shape. 'Skinning' the shape effectively renames the material targets, allowing different materials to be used on different instances of the same model. Any material targets that start with the old skin name have that part of the name replaced with the new skin name. The initial old skin name is "base". For example, if a new skin of "blue" was applied to a model that had material targets base_body and face , the new targets would be blue_body and face . Note that face was not renamed since it did not start with the old skin name of "base". To support models that do not use the default "base" naming convention, you can also specify the part of the name to replace in the skin field itself. For example, if a model had a material target called shapemat , we could apply a new skin "shape=blue", and the material target would be renamed to bluemat (note "shape" has been replaced with "blue"). Multiple skin updates can also be applied at the same time by separating them with a semicolon. For example: "base=blue;face=happy_face". Material targets are only renamed if an existing Material maps to that name, or if there is a diffuse texture in the model folder with the same name as the new target.
