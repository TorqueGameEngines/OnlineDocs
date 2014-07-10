fxShapeReplicatedStatic
=======================

The object definition for shapes that will be replicated across an area using an fxShapeReplicator.

Inherit:
	:doc:`SceneObject`

Description
-----------

The object definition for shapes that will be replicated across an area using an fxShapeReplicator.

Fields
------

.. cpp:member:: bool  fxShapeReplicatedStatic::allowPlayerStep

	Allow a Player to walk up sloping polygons in the TSStatic (based on the collisionType). When set to false, the slightest bump will stop the player from walking on top of the object.

.. cpp:member:: TSMeshType fxShapeReplicatedStatic::collisionType

	The type of mesh data to use for collision queries.

.. cpp:member:: TSMeshType fxShapeReplicatedStatic::decalType

	The type of mesh data used to clip decal polygons against.

.. cpp:member:: int  fxShapeReplicatedStatic::forceDetail

	Forces rendering to a particular detail level.

.. cpp:member:: bool  fxShapeReplicatedStatic::meshCulling

	Enables detailed culling of meshes within the TSStatic . Should only be used with large complex shapes like buildings which contain many submeshes.

.. cpp:member:: bool  fxShapeReplicatedStatic::originSort

	Enables translucent sorting of the TSStatic by its origin instead of the bounds.

.. cpp:member:: bool  fxShapeReplicatedStatic::playAmbient

	Enables automatic playing of the animation sequence named "ambient" (if it exists) when the TSStatic is loaded.

.. cpp:member:: float  fxShapeReplicatedStatic::renderNormals

	Debug rendering mode shows the normals for each point in the TSStatic's mesh.

.. cpp:member:: filename  fxShapeReplicatedStatic::shapeName

	Path and filename of the model file (.DTS, .DAE) to use for this TSStatic .

.. cpp:member:: string  fxShapeReplicatedStatic::skin

	The skin applied to the shape. 'Skinning' the shape effectively renames the material targets, allowing different materials to be used on different instances of the same model. Any material targets that start with the old skin name have that part of the name replaced with the new skin name. The initial old skin name is "base". For example, if a new skin of "blue" was applied to a model that had material targets base_body and face , the new targets would be blue_body and face . Note that face was not renamed since it did not start with the old skin name of "base". To support models that do not use the default "base" naming convention, you can also specify the part of the name to replace in the skin field itself. For example, if a model had a material target called shapemat , we could apply a new skin "shape=blue", and the material target would be renamed to bluemat (note "shape" has been replaced with "blue"). Multiple skin updates can also be applied at the same time by separating them with a semicolon. For example: "base=blue;face=happy_face". Material targets are only renamed if an existing Material maps to that name, or if there is a diffuse texture in the model folder with the same name as the new target.
