TSShapeConstructor
==================

An object used to modify a DTS or COLLADA shape model after it has been loaded by Torque.

Inherit:
	:doc:`SimObject`

Description
-----------

An object used to modify a DTS or COLLADA shape model after it has been loaded by Torque.

TSShapeConstructor is a special object used to modify a DTS or COLLADA shape model after it has been loaded by Torque, but before it is used by any other object.

It is often used to share animations from DSQ files between shapes with a common skeleton.

It may also be used to 'Torquify' a model that is missing the nodes and/or sequences required to function as a particular Torque object. A model used for a Player character for example should have an eye and a cam node, but these might not be present in a model not specifically created for Torque. TSShapeConstructor allows the missing nodes to be added and positioned so that the shape does not need to be re-worked or re-exported by an artist.

TSShapeConstructor also includes features to aid in loading COLLADA models, such as allowing the <up_axis> and <unit> elements to be overridden, and can also apply a user specified prefix to the names of COLLADA materials as shown below. Prefixing material names is useful to avoid name clashes, particularly for 3D apps like Google SketchUp that export models with generic material names like "material0". These options are most easily accessed using the COLLADA import gui, which will be displayed automatically the first time a COLLADA model is imported into Torque.

Settings from the import gui are automatically saved to a TSShapeConstructor script in the same folder as the model.

To create your own TSShapeConstructor object, simply create a TorqueScript file in the same folder as your DTS or COLLADA model, with the same filename but .cs extension. For example, if your model file was called myShape.dts, you would create a file called myShape.cs. Some example appear below:

The name of the TSShapeConstructor object (MyShapeDae and MyShape2Dae in the code samples above) is up to you, but you should choose a name that does not conflict with other objects or datablocks. A common convention for TSShapeConstructor objects is the name of the shape file. eg. MyShapeDae for a file called myshape.dae.

When Torque loads a DTS (.dts) or COLLADA (.dae) file, it first looks in the same folder for a TorqueScript file with the same filename (but .cs extension) in order to create the TSShapeConstructor object. Such scripts are executed automatically by Torque 3D, so there is no need to manually call exec("myShape.cs") from another script. Also, you should avoid adding other object and datablock declarations to this script because it will be executed every time the model is loaded, which may cause unexpected results if the datablocks already exist.

After Torque has loaded the model from the DTS or COLLADA file, it executes the TSShapeConstructor onLoad method to apply the desired set of changes to the shape. It should be noted that the changes are applied to the loaded model in memory rather than to the DTS or COLLADA file itself. This means the model can be re-exported to DTS or COLLADA without overwriting the TSShapeConstructor changes. TSShapeConstructor should be thought of as a post-export processing step, and is intended to be used alongside existing object and datablock setups.

Note that DSQ sequences may still be specified within the TSShapeConstructor object as normal:

Note that most of the features in TSShapeConstructor are far more easily accessible in the Shape Editor tool. This tool uses TSShapeConstructor 'under-the-hood' to edit the nodes, sequences and details of a shape, and the changes are saved to a TSShapeConstructor script object.

Shape Terminology
-----------------

The following definitions should be understood before reading the TSShapeConstructor examples and function reference:

Example 1: Adding a Collision Mesh To an Existing Shape
-------------------------------------------------------

Imagine you have a model that you want to add to the scene as a StaticShape, but it is missing a collision mesh. TSShapeConstructor makes it simple to modify an existing DTS shape to add a collision (or line-of-sight collision) detail level.

First, define the StaticShapeData datablock as normal. Create a script called myShape.cs in the art/datablocks folder, and define the datablock:

We need to tell Torque to execute this script so add exec("./myShape.cs"); to art/datablocks/datablockExec.cs.

Now we define the TSShapeConstructor object by creating a new script called myShape.cs in the art/shapes/myShape folder:

This script will add a box mesh with the same center and dimensions as the original model using the "Col" detail level at size -1. The negative detail size means that the mesh will not be rendered in-game, and the use of the special "Col" name means that this mesh will be detected as a collision mesh by the Torque engine.

When a Torque mission is started, the following steps occur:

Example 2: Adding a Mesh From an Existing DTS File
--------------------------------------------------

The image below shows a boulder.dts shape in the Torque Show Tool Pro (TSTPro). The circled items indicate the geometry and material that will be copied into a different shape using TSShapeConstructor.

The following shows how to include the boulder1 mesh in another shape:

The output of the dumpShape command is shown below:

Note that the new detail ("detail128"), object ("test") and material ("MossyRock02") have been added to the normal rock1.dts shape.

Example 3: Auto-loading animations
----------------------------------

Instead of manually specifying all of the animations to load, it's easy to write some TorqueScript that will scan a folder for any matching animations and add them to the shape automatically. Imagine that we have the following shape (DTS) and sequence (DSQ) files:

The following script will scan the animations folder and add the sequences to the shape.

Example 4: Splitting COLLADA animations
---------------------------------------

Many COLLADA exporters do not support the <animation_clip> element, meaning that animated models imported into Torque appear to have only a single sequence containing all of the animations. TSShapeConstructor can be used to split this combined animation into individual sequences. This is most easily done using the Shape Editor tool, but can also be done manually as follows:

Example 5: LOD using separate files
-----------------------------------

In the past, using LOD required the artist to export all detail levels into a single DTS file. Using TSShapeConstructor, we can combine separate model files together. In fact, we can even use the folder-scanning approach from Example 3 to automatically construct the shape detail levels using all of the model files in the folder!

Note that the detail level models must contain the same object name, and for skinned models, the skin must be applied to the same skeleton for this script to work.

Imagine that we have the following shape (DAE) files:

Example 6: Add lights to the scene
----------------------------------

Although most often used to modify a shape before it is used, TSShapeConstructor can also be used as a general purpose interface to a 3D shape. For example, a 3D modeling package could be used to layout positions for lights in the scene. On import, the shape hierarchy might look like this:

The following code demonstrates how to create a TSShapeConstructor object on-demand in order to access the 3D shape data. This example adds lights to the current scene at position of the lightX nodes in the shape:

The original shape can be placed anywhere in the scene, then AddLights is called to create and place a PointLight at each node.

Example 7: Rigid-body Player Character
--------------------------------------

Using the addNode and addMesh functions, it is possible to create a rigid-body (ie. non-skinned) player model compatible with the default animations, completely from TorqueScript!

The default player skeleton node transforms were obtained by adding the following code to the TSShapeConstructor onLoad function for a shape that already contained the default skeleton:

The contents of the console can then be copied and pasted into a new script. The script below shows the player model creation process: first pick a dummy dts file (rock1.dts in this case), and delete its existing nodes and meshes. Then create the default player skeleton. Finally, some box meshes are added at certain nodes to build up a rigid-body player character.

This produces the following shape:


Methods
-------


.. cpp:function:: bool TSShapeConstructor::addCollisionDetail(int size, string type, string target, int depth, float merge, float concavity, int maxVerts, float boxMaxError, float sphereMaxError, float capsuleMaxError)

	Autofit a mesh primitive or set of convex hulls to the shape geometry. Hulls may optionally be converted to boxes, spheres and/or capsules based on their volume.

	:param size: size for this detail level
	:param type: one of: box, sphere, capsule, 10-dop x, 10-dop y, 10-dop z, 18-dop, 26-dop, convex hulls. See the Shape Editor documentation for more details about these types.
	:param target: geometry to fit collision mesh(es) to; either "bounds" (for the whole shape), or the name of an object in the shape
	:param depth: maximum split recursion depth (hulls only)
	:param merge: volume % threshold used to merge hulls together (hulls only)
	:param concavity: volume % threshold used to detect concavity (hulls only)
	:param maxVerts: maximum number of vertices per hull (hulls only)
	:param boxMaxError: max % volume difference for a hull to be converted to a box (hulls only)
	:param sphereMaxError: max % volume difference for a hull to be converted to a sphere (hulls only)
	:param capsuleMaxError: max % volume difference for a hull to be converted to a capsule (hulls only)

	:return: true if successful, false otherwise

	Example::

		%this.addCollisionDetail( -1, "box", "bounds" );
		%this.addCollisionDetail( -1, "convex hulls", "bounds", 4, 30, 30, 32, 0, 0, 0 );
		%this.addCollisionDetail( -1, "convex hulls", "bounds", 4, 30, 30, 32, 50, 50, 50 );

.. cpp:function:: int TSShapeConstructor::addImposter(int size, int equatorSteps, int polarSteps, int dl, int dim, bool includePoles, float polarAngle)

	Add (or edit) an imposter detail level to the shape. If the shape already contains an imposter detail level, this command will simply change the imposter settings

	:param size: size of the imposter detail level
	:param equatorSteps: defines the number of snapshots to take around the equator. Imagine the object being rotated around the vertical axis, then a snapshot taken at regularly spaced intervals.
	:param polarSteps: defines the number of snapshots taken between the poles (top and bottom), at each equator step. eg. At each equator snapshot, snapshots are taken at regular intervals between the poles.
	:param dl: the detail level to use when generating the snapshots. Note that this is an array index rather than a detail size. So if an object has detail sizes of: 200, 150, and 40, then setting dl to 1 will generate the snapshots using detail size 150.
	:param dim: defines the size of the imposter images in pixels. The larger the number, the more detailed the billboard will be.
	:param includePoles: flag indicating whether to include the "pole" snapshots. ie. the views from the top and bottom of the object.
	:param polar_angle: if pole snapshots are active (includePoles is true), this parameter defines the camera angle (in degrees) within which to render the pole snapshot. eg. if polar_angle is set to 25 degrees, then the snapshot taken at the pole (looking directly down or up at the object) will be rendered when the camera is within 25 degrees of the pole.

	:return: true if successful, false otherwise

	Example::

		%this.addImposter( 2, 4, 0, 0, 64, false, 0 );
		%this.addImposter( 2, 4, 2, 0, 64, true, 10 );   // this command would edit the existing imposter detail level

.. cpp:function:: bool TSShapeConstructor::addMesh(string meshName, string srcShape, string srcMesh)

	Add geometry from another DTS or DAE shape file into this shape. Any materials required by the source mesh are also copied into this shape.

	:param meshName: full name (object name + detail size) of the new mesh. If no detail size is present at the end of the name, a value of 2 is used. An underscore before the number at the end of the name will be interpreted as a negative sign. eg. "MyMesh_4" will be interpreted as "MyMesh-4".
	:param srcShape: name of a shape file (DTS or DAE) that contains the mesh
	:param srcMesh: the full name (object name + detail size) of the mesh to copy from the DTS/DAE file into this shape

	:return: true if successful, false otherwise

	Example::

		%this.addMesh( "ColMesh-1", "./collision.dts", "ColMesh", "Col-1" );
		%this.addMesh( "SimpleShape10", "./testShape.dae", "MyMesh2",  );

.. cpp:function:: bool TSShapeConstructor::addNode(string name, string parentName, TransformF txfm, bool isWorld)

	Add a new node.

	:param name: name for the new node (must not already exist)
	:param parentName: name of an existing node to be the parent of the new node. If empty (""), the new node will be at the root level of the node hierarchy.
	:param txfm: (optional) transform string of the form: "pos.x pos.y pos.z rot.x rot.y rot.z rot.angle"
	:param isworld: (optional) flag to set the local-to-parent or the global transform. If false, or not specified, the position and orientation are treated as relative to the node's parent.

	:return: true if successful, false otherwise

	Example::

		%this.addNode( "Nose", "Bip01 Head", "0 2 2 0 0 1 0" );
		%this.addNode( "myRoot", "", "0 0 4 0 0 1 1.57" );
		%this.addNode( "Nodes", "Bip01 Head", "0 2 0 0 0 1 0", true );

.. cpp:function:: bool TSShapeConstructor::addPrimitive(string meshName, string type, string params, TransformF txfm, string nodeName)

	Add a new mesh primitive to the shape.

	:param meshName: full name (object name + detail size) of the new mesh. If no detail size is present at the end of the name, a value of 2 is used. An underscore before the number at the end of the name will be interpreted as a negative sign. eg. "MyMesh_4" will be interpreted as "MyMesh-4".
	:param type: one of: "box", "sphere", "capsule"
	:param params: mesh primitive parameters: for box: "size_x size_y size_z", for sphere: "radius", for capsule: "height radius"
	:param txfm: local transform offset from the node for this mesh
	:param nodeName: name of the node to attach the new mesh to (will change the object's node if adding a new mesh to an existing object)

	:return: true if successful, false otherwise

	Example::

		%this.addMesh( "Box4", "box", "2 4 2", "0 2 0 0 0 1 0", "eye" );
		%this.addMesh( "Sphere256", "sphere", "2", "0 0 0 0 0 1 0", "root" );
		%this.addMesh( "MyCapsule-1", "capsule", "2 5", "0 0 2 0 0 1 0", "base01" );

.. cpp:function:: bool TSShapeConstructor::addSequence(string source, string name, int start, int end, bool padRot, bool padTrans)

	Add a new sequence to the shape.

	:param source: the name of an existing sequence, or the name of a DTS or DAE shape or DSQ sequence file. When the shape file contains more than one sequence, the desired sequence can be specified by appending the name to the end of the shape file. eg. "myShape.dts run" would select the "run" sequence from the "myShape.dts" file.
	:param name: name of the new sequence
	:param start: (optional) first frame to copy. Defaults to 0, the first frame in the sequence.
	:param end: (optional) last frame to copy. Defaults to -1, the last frame in the sequence.
	:param padRot: (optional) copy root-pose rotation keys for non-animated nodes. This is useful if the source sequence data has a different root-pose to the target shape, such as if one character was in the T pose, and the other had arms at the side. Normally only nodes that are actually rotated by the source sequence have keyframes added, but setting this flag will also add keyframes for nodes that are not animated, but have a different root-pose rotation to the target shape root pose.
	:param padTrans: (optional) copy root-pose translation keys for non-animated nodes. This is useful if the source sequence data has a different root-pose to the target shape, such as if one character was in the T pose, and the other had arms at the side. Normally only nodes that are actually moved by the source sequence have keyframes added, but setting this flag will also add keyframes for nodes that are not animated, but have a different root-pose position to the target shape root pose.

	:return: true if successful, false otherwise

	Example::

		%this.addSequence( "./testShape.dts ambient", "ambient" );
		%this.addSequence( "./myPlayer.dae run", "run" );
		%this.addSequence( "./player_look.dsq", "look", 0, -1 );     // start to end
		%this.addSequence( "walk", "walk_shortA", 0, 4 );            // start to frame 4
		%this.addSequence( "walk", "walk_shortB", 4, -1 );           // frame 4 to end

.. cpp:function:: bool TSShapeConstructor::addTrigger(string name, int keyframe, int state)

	Add a new trigger to the sequence.

	:param name: name of the sequence to modify
	:param keyframe: keyframe of the new trigger
	:param state: of the new trigger

	:return: true if successful, false otherwise

	Example::

		%this.addTrigger( "walk", 3, 1 );
		%this.addTrigger( "walk", 5, -1 );

.. cpp:function:: void TSShapeConstructor::dumpShape(string filename)

	Dump the shape hierarchy to the console or to a file. Useful for reviewing the result of a series of construction commands.

	:param filename: Destination filename. If not specified, dump to console.

	Example::

		%this.dumpShape();               // dump to console
		%this.dumpShape( "./dump.txt" ); // dump to file

.. cpp:function:: Box3F TSShapeConstructor::getBounds()

	Get the bounding box for the shape.

	:return: Bounding box "minX minY minZ maxX maxY maxZ" 

.. cpp:function:: int TSShapeConstructor::getDetailLevelCount()

	Get the total number of detail levels in the shape.

	:return: the number of detail levels in the shape 

.. cpp:function:: int TSShapeConstructor::getDetailLevelIndex(int size)

	Get the index of the detail level with a given size.

	:param size: size of the detail level to lookup

	:return: index of the detail level with the desired size, or -1 if no such detail exists

	Example::

		if ( %this.getDetailLevelSize( 32 ) == -1 )
		   echo( "Error: This shape does not have a detail level at size 32" );

.. cpp:function:: string TSShapeConstructor::getDetailLevelName(int index)

	Get the name of the indexed detail level.

	:param index: detail level index (valid range is 0 - getDetailLevelCount()-1)

	:return: the detail level name

	Example::

		// print the names of all detail levels in the shape
		%count = %this.getDetailLevelCount();
		for ( %i = 0; %i < %count; %i++ )
		   echo( %i SPC %this.getDetailLevelName( %i ) );

.. cpp:function:: int TSShapeConstructor::getDetailLevelSize(int index)

	Get the size of the indexed detail level.

	:param index: detail level index (valid range is 0 - getDetailLevelCount()-1)

	:return: the detail level size

	Example::

		// print the sizes of all detail levels in the shape
		%count = %this.getDetailLevelCount();
		for ( %i = 0; %i < %count; %i++ )
		   echo( "Detail" @ %i @ " has size " @ %this.getDetailLevelSize( %i ) );

.. cpp:function:: int TSShapeConstructor::getImposterDetailLevel()

	Get the index of the imposter (auto-billboard) detail level (if any).

	:return: imposter detail level index, or -1 if the shape does not use imposters. 

.. cpp:function:: string TSShapeConstructor::getImposterSettings(int index)

	Get the settings used to generate imposters for the indexed detail level.

	:param index: index of the detail level to query (does not need to be an imposter detail level

	:return: 1 if this detail level generates imposters, 0 otherwise

	Example::

		// print the imposter detail level settings
		%index = %this.getImposterDetailLevel();
		if ( %index != -1 )
		   echo( "Imposter settings: " @ %this.getImposterSettings( %index ) );

.. cpp:function:: int TSShapeConstructor::getMeshCount(string name)

	Get the number of meshes (detail levels) for the specified object.

	:param name: name of the object to query

	:return: the number of meshes for this object.

	Example::

		%count = %this.getMeshCount( "SimpleShape" );

.. cpp:function:: string TSShapeConstructor::getMeshMaterial(string name)

	Get the name of the material attached to a mesh. Note that only the first material used by the mesh is returned.

	:param name: full name (object name + detail size) of the mesh to query

	:return:  mapTo field)

	Example::

		echo( "Mesh material is " @ %this.sgetMeshMaterial( "SimpleShape128" ) );

.. cpp:function:: string TSShapeConstructor::getMeshName(string name, int index)

	Get the name of the indexed mesh (detail level) for the specified object.

	:param name: name of the object to query
	:param index: index of the mesh (valid range is 0 - getMeshCount()-1)

	:return: the mesh name.

	Example::

		// print the names of all meshes in the shape
		%objCount = %this.getObjectCount();
		for ( %i = 0; %i < %objCount; %i++ )
		{
		   %objName = %this.getObjectName( %i );
		   %meshCount = %this.getMeshCount( %objName );
		   for ( %j = 0; %j < %meshCount; %j++ )
		      echo( %this.getMeshName( %objName, %j ) );
		}

.. cpp:function:: int TSShapeConstructor::getMeshSize(string name, int index)

	Get the detail level size of the indexed mesh for the specified object.

	:param name: name of the object to query
	:param index: index of the mesh (valid range is 0 - getMeshCount()-1)

	:return: the mesh detail level size.

	Example::

		// print sizes for all detail levels of this object
		%objName = "trunk";
		%count = %this.getMeshCount( %objName );
		for ( %i = 0; %i < %count; %i++ )
		   echo( %this.getMeshSize( %objName, %i ) );

.. cpp:function:: string TSShapeConstructor::getMeshType(string name)

	Get the display type of the mesh.

	:param name: name of the mesh to query

	:return: a normal 3D mesh

	Example::

		echo( "Mesh type is " @ %this.getMeshType( "SimpleShape128" ) );

.. cpp:function:: int TSShapeConstructor::getNodeChildCount(string name)

	Get the number of children of this node.

	:param name: name of the node to query.

	:return: the number of child nodes.

	Example::

		%count = %this.getNodeChildCount( "Bip01 Pelvis" );

.. cpp:function:: string TSShapeConstructor::getNodeChildName(string name, int index)

	Get the name of the indexed child node.

	:param name: name of the parent node to query.
	:param index: index of the child node (valid range is 0 - getNodeChildName()-1).

	:return: the name of the indexed child node.

	Example::

		function dumpNode( %shape, %name, %indent )
		{
		   echo( %indent @ %name );
		   %count = %shape.getNodeChildCount( %name );
		   for ( %i = 0; %i < %count; %i++ )
		      dumpNode( %shape, %shape.getNodeChildName( %name, %i ), %indent @ "" );
		}
		
		function dumpShape( %shape )
		{
		   // recursively dump node hierarchy
		   %count = %shape.getNodeCount();
		   for ( %i = 0; %i < %count; %i++ )
		   {
		      // dump top level nodes
		      %name = %shape.getNodeName( %i );
		      if ( %shape.getNodeParentName( %name ) $=  )
		         dumpNode( %shape, %name, "" );
		   }
		}

.. cpp:function:: int TSShapeConstructor::getNodeCount()

	Get the total number of nodes in the shape.

	:return: the number of nodes in the shape.

	Example::

		%count = %this.getNodeCount();

.. cpp:function:: int TSShapeConstructor::getNodeIndex(string name)

	Get the index of the node.

	:param name: name of the node to lookup.

	:return: the index of the named node, or -1 if no such node exists.

	Example::

		// get the index of Bip01 Pelvis node in the shape
		%index = %this.getNodeIndex( "Bip01 Pelvis" );

.. cpp:function:: string TSShapeConstructor::getNodeName(int index)

	Get the name of the indexed node.

	:param index: index of the node to lookup (valid range is 0 - getNodeCount()-1).

	:return: the name of the indexed node, or "" if no such node exists.

	Example::

		// print the names of all the nodes in the shape
		%count = %this.getNodeCount();
		for (%i = 0; %i < %count; %i++)
		   echo(%i SPC %this.getNodeName(%i));

.. cpp:function:: int TSShapeConstructor::getNodeObjectCount(string name)

	Get the number of geometry objects attached to this node.

	:param name: name of the node to query.

	:return: the number of attached objects.

	Example::

		%count = %this.getNodeObjectCount( "Bip01 Head" );

.. cpp:function:: string TSShapeConstructor::getNodeObjectName(string name, int index)

	Get the name of the indexed object.

	:param name: name of the node to query.
	:param index: index of the object (valid range is 0 - getNodeObjectCount()-1).

	:return: the name of the indexed object.

	Example::

		// print the names of all objects attached to the node
		%count = %this.getNodeObjectCount( "Bip01 Head" );
		for ( %i = 0; %i < %count; %i++ )
		   echo( %this.getNodeObjectName( "Bip01 Head", %i ) );

.. cpp:function:: string TSShapeConstructor::getNodeParentName(string name)

	Get the name of the node's parent. If the node has no parent (ie. it is at the root level), return an empty string.

	:param name: name of the node to query.

	:return: the name of the node's parent, or "" if the node is at the root level

	Example::

		echo( "Bip01 Pelvis parent = " @ %this.getNodeParentName( "Bip01 Pelvis ") );

.. cpp:function:: TransformF TSShapeConstructor::getNodeTransform(string name, bool isWorld)

	Get the base (ie. not animated) transform of a node.

	:param name: name of the node to query.
	:param isWorld: true to get the global transform, false (or omitted) to get the local-to-parent transform.

	:return: the node transform in the form "pos.x pos.y pos.z rot.x rot.y rot.z rot.angle".

	Example::

		%ret = %this.getNodeTransform( "mount0" );
		%this.setNodeTransform( "mount4", %ret );

.. cpp:function:: int TSShapeConstructor::getObjectCount()

	Get the total number of objects in the shape.

	:return: the number of objects in the shape.

	Example::

		%count = %this.getObjectCount();

.. cpp:function:: int TSShapeConstructor::getObjectIndex(string name)

	Get the index of the first object with the given name.

	:param name: name of the object to get.

	:return: the index of the named object.

	Example::

		%index = %this.getObjectIndex( "Head" );

.. cpp:function:: string TSShapeConstructor::getObjectName(int index)

	Get the name of the indexed object.

	:param index: index of the object to get (valid range is 0 - getObjectCount()-1).

	:return: the name of the indexed object.

	Example::

		// print the names of all objects in the shape
		%count = %this.getObjectCount();
		for ( %i = 0; %i < %count; %i++ )
		   echo( %i SPC %this.getObjectName( %i ) );

.. cpp:function:: string TSShapeConstructor::getObjectNode(string name)

	Get the name of the node this object is attached to.

	:param name: name of the object to get.

	:return: the name of the attached node, or an empty string if this object is not attached to a node (usually the case for skinned meshes).

	Example::

		echo( "Hand is attached to " @ %this.getObjectNode( "Hand" ) );

.. cpp:function:: string TSShapeConstructor::getSequenceBlend(string name)

	Get information about blended sequences.

	:param name: name of the sequence to query

	:return: a boolean flag indicating whether this sequence is a blend

	Example::

		%blendData = %this.getSequenceBlend( "look" );
		if ( getField( %blendData, 0 ) )
		   echo( "look is a blend, reference: " @ getField( %blendData, 1 ) );

.. cpp:function:: int TSShapeConstructor::getSequenceCount()

	Get the total number of sequences in the shape.

	:return: the number of sequences in the shape 

.. cpp:function:: bool TSShapeConstructor::getSequenceCyclic(string name)

	Check if this sequence is cyclic (looping).

	:param name: name of the sequence to query

	:return: true if this sequence is cyclic, false if not

	Example::

		if ( !%this.getSequenceCyclic( "ambient" ) )
		   error( "ambient sequence is not cyclic!" );

.. cpp:function:: int TSShapeConstructor::getSequenceFrameCount(string name)

	Get the number of keyframes in the sequence.

	:param name: name of the sequence to query

	:return: number of keyframes in the sequence

	Example::

		echo( "Run has " @ %this.getSequenceFrameCount( "run" ) @ " keyframes" );

.. cpp:function:: string TSShapeConstructor::getSequenceGroundSpeed(string name)

	Get the ground speed of the sequence.

	:param name: name of the sequence to query

	:return: string of the form: "trans.x trans.y trans.z rot.x rot.y rot.z"

	Example::

		%speed = VectorLen( getWords( %this.getSequenceGroundSpeed( "run" ), 0, 2 ) );
		   echo( "Run moves at " @ %speed @ " units per frame" );

.. cpp:function:: int TSShapeConstructor::getSequenceIndex(string name)

	Find the index of the sequence with the given name.

	:param name: name of the sequence to lookup

	:return: index of the sequence with matching name, or -1 if not found

	Example::

		// Check if a given sequence exists in the shapeif ( %this.getSequenceIndex( "walk" ) == -1 )
		   echo( "Could not find walk sequence" );

.. cpp:function:: string TSShapeConstructor::getSequenceName(int index)

	Get the name of the indexed sequence.

	:param index: index of the sequence to query (valid range is 0 - getSequenceCount()-1)

	:return: the name of the sequence

	Example::

		// print the name of all sequences in the shape
		%count = %this.getSequenceCount();
		for ( %i = 0; %i < %count; %i++ )
		   echo( %i SPC %this.getSequenceName( %i ) );

.. cpp:function:: float TSShapeConstructor::getSequencePriority(string name)

	Get the priority setting of the sequence.

	:param name: name of the sequence to query

	:return: priority value of the sequence 

.. cpp:function:: string TSShapeConstructor::getSequenceSource(string name)

	Get information about where the sequence data came from. For example, whether it was loaded from an external DSQ file.

	:param name: name of the sequence to query

	:return: the source of the animation data, such as the path to a DSQ file, or the name of an existing sequence in the shape. This field will be empty for sequences already embedded in the DTS or DAE file.

	Example::

		// print the source for the walk animationecho( "walk source:" SPC getField( %this.getSequenceSource( "walk" ), 0 ) );

.. cpp:function:: int TSShapeConstructor::getTargetCount()

	Get the number of materials in the shape.

	:return: the number of materials in the shape.

	Example::

		%count = %this.getTargetCount();

.. cpp:function:: string TSShapeConstructor::getTargetName(int index)

	Get the name of the indexed shape material.

	:param index: index of the material to get (valid range is 0 - getTargetCount()-1).

	:return: the name of the indexed material.

	Example::

		%count = %this.getTargetCount();
		for ( %i = 0; %i < %count; %i++ )
		   echo( "Target " @ %i @ ": " @ %this.getTargetName( %i ) );

.. cpp:function:: string TSShapeConstructor::getTrigger(string name, int index)

	Get information about the indexed trigger.

	:param name: name of the sequence to query
	:param index: index of the trigger (valid range is 0 - getTriggerCount()-1)

	:return: string of the form "frame state"

	Example::

		// print all triggers in the sequence
		%count = %this.getTriggerCount( "back" );
		for ( %i = 0; %i < %count; %i++ )
		   echo( %i SPC %this.getTrigger( "back", %i ) );

.. cpp:function:: int TSShapeConstructor::getTriggerCount(string name)

	Get the number of triggers in the specified sequence.

	:param name: name of the sequence to query

	:return: number of triggers in the sequence 

.. cpp:function:: void TSShapeConstructor::notifyShapeChanged()

	Notify game objects that this shape file has changed, allowing them to update internal data if needed.

.. cpp:function:: void TSShapeConstructor::onLoad()

	Called immediately after the DTS or DAE file has been loaded; before the shape data is available to any other object ( StaticShape , Player etc). This is where you should put any post-load commands to modify the shape in-memory such as addNode, renameSequence etc.

.. cpp:function:: void TSShapeConstructor::onUnload()

	Called when the DTS or DAE resource is flushed from memory. Not normally required, but may be useful to perform cleanup.

.. cpp:function:: bool TSShapeConstructor::removeDetailLevel(int index)

	Remove the detail level (including all meshes in the detail level).

	:param size: size of the detail level to remove

	:return: true if successful, false otherwise 

	Example::

		%this.removeDetailLevel( 2 );

.. cpp:function:: bool TSShapeConstructor::removeImposter()

	Remove the imposter detail level (if any) from the shape.

	:return: true if successful, false otherwise 

.. cpp:function:: bool TSShapeConstructor::removeMesh(string name)

	Remove a mesh from the shape. If all geometry is removed from an object, the object is also removed.

	:param name: full name (object name + detail size) of the mesh to remove

	:return: true if successful, false otherwise

	Example::

		%this.removeMesh( "SimpleShape128" );

.. cpp:function:: bool TSShapeConstructor::removeNode(string name)

	Remove a node from the shape. The named node is removed from the shape, including from any sequences that use the node. Child nodes and objects attached to the node are re-assigned to the node's parent.

	:param name: name of the node to remove.

	:return: true if successful, false otherwise.

	Example::

		%this.removeNode( "Nose" );

.. cpp:function:: bool TSShapeConstructor::removeObject(string name)

	Remove an object (including all meshes for that object) from the shape.

	:param name: name of the object to remove.

	:return: true if successful, false otherwise.

	Example::

		// clear all objects in the shape
		%count = %this.getObjectCount();
		for ( %i = %count-1; %i >= 0; %i-- )
		   %this.removeObject( %this.getObjectName(%i) );

.. cpp:function:: bool TSShapeConstructor::removeSequence(string name)

	Remove the sequence from the shape.

	:param name: name of the sequence to remove

	:return: true if successful, false otherwise 

.. cpp:function:: bool TSShapeConstructor::removeTrigger(string name, int keyframe, int state)

	Remove a trigger from the sequence.

	:param name: name of the sequence to modify
	:param keyframe: keyframe of the trigger to remove
	:param state: of the trigger to remove

	:return: true if successful, false otherwise

	Example::

		%this.removeTrigger( "walk", 3, 1 );

.. cpp:function:: bool TSShapeConstructor::renameDetailLevel(string oldName, string newName)

	Rename a detail level.

	:param oldName: current name of the detail level
	:param newName: new name of the detail level

	:return: true if successful, false otherwise

	Example::

		%this.renameDetailLevel( "detail-1", "collision-1" );

.. cpp:function:: bool TSShapeConstructor::renameNode(string oldName, string newName)

	Rename a node.

	:param oldName: current name of the node
	:param newName: new name of the node

	:return: true if successful, false otherwise

	Example::

		%this.renameNode( "Bip01 L Hand", "mount5" );

.. cpp:function:: bool TSShapeConstructor::renameObject(string oldName, string newName)

	Rename an object.

	:param oldName: current name of the object
	:param newName: new name of the object

	:return: true if successful, false otherwise

	Example::

		%this.renameObject( "MyBox", "Box" );

.. cpp:function:: bool TSShapeConstructor::renameSequence(string oldName, string newName)

	Rename a sequence.

	:param oldName: current name of the sequence
	:param newName: new name of the sequence

	:return: true if successful, false otherwise

	Example::

		%this.renameSequence( "walking", "walk" );

.. cpp:function:: void TSShapeConstructor::saveShape(string filename)

	Save the shape (with all current changes) to a new DTS file.

	:param filename: Destination filename.

	Example::

		%this.saveShape( "./myShape.dts" );

.. cpp:function:: bool TSShapeConstructor::setBounds(Box3F bbox)

	Set the shape bounds to the given bounding box.

	:param Bounding: box "minX minY minZ maxX maxY maxZ"

	:return: true if successful, false otherwise 

.. cpp:function:: int TSShapeConstructor::setDetailLevelSize(int index, int newSize)

	Change the size of a detail level.

	:param index: index of the detail level to modify
	:param newSize: new size for the detail level

	:return: new index for this detail level

	Example::

		%this.setDetailLevelSize( 2, 256 );

.. cpp:function:: bool TSShapeConstructor::setMeshMaterial(string meshName, string matName)

	Set the name of the material attached to the mesh.

	:param meshName: full name (object name + detail size) of the mesh to modify
	:param matName: name of the material to attach. This could be the base name of the diffuse texture (eg. "test_mat" for "test_mat.jpg"), or the name of a Material object already defined in script.

	:return: true if successful, false otherwise

	Example::

		// set the mesh material
		%this.setMeshMaterial( "SimpleShape128", "test_mat" );

.. cpp:function:: bool TSShapeConstructor::setMeshSize(string name, int size)

	Change the detail level size of the named mesh.

	:param name: full name (object name + current size ) of the mesh to modify
	:param size: new detail level size

	:return: true if successful, false otherwise.

	Example::

		%this.setMeshSize( "SimpleShape128", 64 );

.. cpp:function:: bool TSShapeConstructor::setMeshType(string name, string type)

	Set the display type for the mesh.

	:param name: full name (object name + detail size) of the mesh to modify
	:param type: the new type for the mesh: "normal", "billboard" or "billboardzaxis"

	:return: true if successful, false otherwise

	Example::

		// set the mesh to be a billboard
		%this.setMeshType( "SimpleShape64", "billboard" );

.. cpp:function:: bool TSShapeConstructor::setNodeParent(string name, string parentName)

	Set the parent of a node.

	:param name: name of the node to modify
	:param parentName: name of the parent node to set (use "" to move the node to the root level)

	:return: true if successful, false if failed

	Example::

		%this.setNodeParent( "Bip01 Pelvis", "start01" );

.. cpp:function:: bool TSShapeConstructor::setNodeTransform(string name, TransformF txfm, bool isWorld)

	Set the base transform of a node. That is, the transform of the node when in the root (not-animated) pose.

	:param name: name of the node to modify
	:param txfm: transform string of the form: "pos.x pos.y pos.z rot.x rot.y rot.z rot.angle"
	:param isworld: (optional) flag to set the local-to-parent or the global transform. If false, or not specified, the position and orientation are treated as relative to the node's parent.

	:return: true if successful, false otherwise

	Example::

		%this.setNodeTransform( "mount0", "0 0 1 0 0 1 0" );
		%this.setNodeTransform( "mount0", "0 0 0 0 0 1 1.57" );
		%this.setNodeTransform( "mount0", "1 0 0 0 0 1 0", true );

.. cpp:function:: bool TSShapeConstructor::setObjectNode(string objName, string nodeName)

	Set the node an object is attached to. When the shape is rendered, the object geometry is rendered at the node's current transform.

	:param objName: name of the object to modify
	:param nodeName: name of the node to attach the object to

	:return: true if successful, false otherwise

	Example::

		%this.setObjectNode( "Hand", "Bip01 LeftHand" );

.. cpp:function:: bool TSShapeConstructor::setSequenceBlend(string name, bool blend, string blendSeq, int blendFrame)

	Mark a sequence as a blend or non-blend. A blend sequence is one that will be added on top of any other playing sequences. This is done by storing the animated node transforms relative to a reference frame, rather than as absolute transforms.

	:param name: name of the sequence to modify
	:param blend: true to make the sequence a blend, false for a non-blend
	:param blendSeq: the name of the sequence that contains the blend reference frame
	:param blendFrame: the reference frame in the blendSeq sequence

	:return: true if successful, false otherwise

	Example::

		%this.setSequenceBlend( "look", true, "root", 0 );

.. cpp:function:: bool TSShapeConstructor::setSequenceCyclic(string name, bool cyclic)

	Mark a sequence as cyclic or non-cyclic.

	:param name: name of the sequence to modify
	:param cyclic: true to make the sequence cyclic, false for non-cyclic

	:return: true if successful, false otherwise

	Example::

		%this.setSequenceCyclic( "ambient", true );
		%this.setSequenceCyclic( "shoot", false );

.. cpp:function:: bool TSShapeConstructor::setSequenceGroundSpeed(string name, Point3F transSpeed, Point3F rotSpeed)

	Set the translation and rotation ground speed of the sequence. The ground speed of the sequence is set by generating ground transform keyframes. The ground translational and rotational speed is assumed to be constant for the duration of the sequence. Existing ground frames for the sequence (if any) will be replaced.

	:param name: name of the sequence to modify
	:param transSpeed: translational speed (trans.x trans.y trans.z) in Torque units per frame
	:param rotSpeed: (optional) rotational speed (rot.x rot.y rot.z) in radians per frame. Default is "0 0 0"

	:return: true if successful, false otherwise

	Example::

		%this.setSequenceGroundSpeed( "run", "5 0 0" );
		%this.setSequenceGroundSpeed( "spin", "0 0 0", "4 0 0" );

.. cpp:function:: bool TSShapeConstructor::setSequencePriority(string name, float priority)

	Set the sequence priority.

	:param name: name of the sequence to modify
	:param priority: new priority value

	:return: true if successful, false otherwise 

.. cpp:function:: void TSShapeConstructor::writeChangeSet()

	Write the current change set to a TSShapeConstructor script file. The name of the script file is the same as the model, but with .cs extension. eg. myShape.cs for myShape.dts or myShape.dae.

Fields
------


.. cpp:member:: bool  TSShapeConstructor::adjustCenter

	Translate COLLADA model on import so the origin is at the center. No effect for DTS files.

.. cpp:member:: bool  TSShapeConstructor::adjustFloor

	Translate COLLADA model on import so origin is at the (Z axis) bottom of the model. No effect for DTS files. This can be used along with adjustCenter to have the origin at the center of the bottom of the model.

.. cpp:member:: string  TSShapeConstructor::alwaysImport

	TAB separated patterns of nodes to import even if in neverImport list. No effect for DTS files. Torque allows unwanted nodes in COLLADA (.dae) files to to be ignored during import. This field contains a TAB separated list of patterns to match node names. Any node that matches one of the patterns in the list will always be imported, even if it also matches the neverImport list

	Example::

		singleton TSShapeConstructor(MyShapeDae)
		{
		   baseShape = "./myShape.dae";
		   alwaysImport = "mount*" TAB "eye";
		   neverImport = "*-PIVOT";
		}

.. cpp:member:: string  TSShapeConstructor::alwaysImportMesh

	TAB separated patterns of meshes to import even if in neverImportMesh list. No effect for DTS files. Torque allows unwanted meshes in COLLADA (.dae) files to to be ignored during import. This field contains a TAB separated list of patterns to match mesh names. Any mesh that matches one of the patterns in the list will always be imported, even if it also matches the neverImportMesh list

	Example::

		singleton TSShapeConstructor(MyShapeDae)
		{
		   baseShape = "./myShape.dae";
		   alwaysImportMesh = "body*" TAB "armor" TAB "bounds";
		   neverImportMesh = "*-dummy";
		}

.. cpp:member:: filename  TSShapeConstructor::baseShape

	Specifies the path to the DTS or DAE file to be operated on by this object. Since the TSShapeConstructor script must be in the same folder as the DTS or DAE file, it is recommended to use a relative path so that the shape and script files can be copied to another location without having to modify the path.

.. cpp:member:: bool  TSShapeConstructor::forceUpdateMaterials

	Forces update of the materials.cs file in the same folder as the COLLADA (.dae) file, even if Materials already exist. No effect for DTS files. Normally only Materials that are not already defined are written to materials.cs.

.. cpp:member:: bool  TSShapeConstructor::ignoreNodeScale

	Ignore lt scale gt elements inside COLLADA lt node gt s. No effect for DTS files. This field is a workaround for certain exporters that generate bad node scaling, and is not usually required.

.. cpp:member:: TSShapeConstructorLodType  TSShapeConstructor::lodType

	Control how the COLLADA (.dae) importer interprets LOD in the model. No effect for DTS files. Set to one of the following values:

.. cpp:member:: string  TSShapeConstructor::matNamePrefix

	Prefix to apply to all material map names in the COLLADA (.dae) file. No effect for DTS files. This field is useful to avoid material name clashes for exporters that generate generic material names like "texture0" or "material1".

.. cpp:member:: string  TSShapeConstructor::neverImport

	TAB separated patterns of nodes to ignore on loading. No effect for DTS files. Torque allows unwanted nodes in COLLADA (.dae) files to to be ignored during import. This field contains a TAB separated list of patterns to match node names. Any node that matches one of the patterns in the list will not be imported (unless it matches the alwaysImport list.

.. cpp:member:: string  TSShapeConstructor::neverImportMesh

	TAB separated patterns of meshes to ignore on loading. No effect for DTS files. Torque allows unwanted meshes in COLLADA (.dae) files to to be ignored during import. This field contains a TAB separated list of patterns to match mesh names. Any mesh that matches one of the patterns in the list will not be imported (unless it matches the alwaysImportMesh list.

.. cpp:member:: filename  TSShapeConstructor::sequence

	Legacy method of adding sequences to a DTS or DAE shape after loading.

	Example::

		singleton TSShapeConstructor(MyShapeDae)
		{
		   baseShape = "./myShape.dae";
		   sequence = "../anims/root.dae root";
		   sequence = "../anims/walk.dae walk";
		   sequence = "../anims/jump.dsq jump";
		}

.. cpp:member:: int  TSShapeConstructor::singleDetailSize

	Sets the detail size when lodType is set to SingleSize. No effect otherwise, and no effect for DTS files.

.. cpp:member:: float  TSShapeConstructor::unit

	Override the lt unit gt element in the COLLADA (.dae) file. No effect for DTS files. COLLADA (.dae) files usually contain a lt unit gt element that indicates the 'real world' units that the model is described in. It means you can work in sensible and meaningful units in your modeling app. For example, if you were modeling a small object like a cup, it might make sense to work in inches (1 MAX unit = 1 inch), but if you were modeling a building, it might make more sense to work in feet (1 MAX unit = 1 foot). If you export both models to COLLADA, T3D will automatically scale them appropriately. 1 T3D unit = 1 meter, so the cup would be scaled down by 0.0254, and the building scaled down by 0.3048, given them both the correct scale relative to each other. Omit the field or set to -1 to use the value in the .dae file (1.0 if the lt unit gt element is not present)

.. cpp:member:: TSShapeConstructorUpAxis  TSShapeConstructor::upAxis

	Override the lt up_axis gt element in the COLLADA (.dae) file. No effect for DTS files. Set to one of the following values:
