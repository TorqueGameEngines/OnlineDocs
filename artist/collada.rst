COLLAD
======

COLLADA is an XML based file format, meaning DAE files may be opened, viewed and edited (if desired) in any text editor.

COLLADA is emerging as the format for interchanging models between DCC (digital-content-creation) applications. Torque 3D can load geometry, material and animation data directly from COLLADA (.dae) files. The Torque 3D COLLADA loader is based on version 1.4.1 of the COLLADA specification.

Many 3D modeling applications come with built-in COLLADA import and export functionality, but 3rd party plugins are also available that may be more stable, updated more frequently and give better results. In particular, OpenCOLLADA is recommended for both Autodesk 3ds Max and Maya.

COLLADA <unit> scale
--------------------

When creating a model, it makes sense to work in units appropriate to the type of object being modeled. For example, it may be convenient to model a building in meters (or feet), but a small object like a pen would be better modeled in cm (or inches). Normally the modeler would be forced to choose a single unit for both objects, and one object would end up having awkward measurements; like a building that is 2000 units high, or a pen that is only 0.14 units long.

This was often the case when exporting DTS models, since the convention for Torque 3D is that 1 Torque unit = 1 meter; forcing the modeler to always work in meters or apply a model-specific scale factor prior to export.

COLLADA provides a mechanism to specify the units used when modeling the object. This is very important, since it allows a set of objects modeled in completely different units to be imported into Torque 3D with the correct scale relative to each other. This is done using the COLLADA <unit> element, which appears near the top of the .dae file and specifies the units-per-meter used for all positional values in the file such as vertex and node positions, translation animations etc. Torque 3D uses this value as a global scale factor which is applied to the entire model on import.

Many modeling applications allow the user to specify the units to be used, or alternatively, the option may be available when exporting the model to COLLADA.

For example, if the model was created using feet as the unit, it would have a <unit> element as follows::

	<unit meter="0.3048" name="foot"/>

Torque 3D would scale the entire model by 0.3048 to convert it to a common reference of 1 Torque unit-per-meter. If another model was loaded that had been modeled in meters, its <unit>element would look like this::

	<unit meter="1.0" name="meter"/>

In this case, the model is already measured in meters and would not be scaled on import.

It is up to the modeler to ensure that models are created with appropriate units in mind. For example, if a chair was modeled at 5 units high in the modeling application (simply because that was a convenient value for the modeler), then exported to DAE with units set to feet, then the chair would appear to be the equivalent of 5 feet high in Torque 3D! The Torque 3D COLLADA import dialog allows you to override the <unit> scale specified in the DAE file, for cases like this when the modeler has not taken units into account.

Up Axis
-------

COLLADA defines the following coordinate systems using the <up_axis> element:

.. image:: images/torque_axes.png

The coordinate system in Torque 3D is equivalent to Z_UP, and the loader will automatically convert models using X_UP or Y_UP to this coordinate system. Some COLLADA exporters may generate models with a wrong or missing <up_axis> element (Z_UP is assumed if <up_axis> is not specified). In this case, the COLLADA import dialog can be used to override the value.

COLLADA for Torque 3D
---------------------

The COLLADA loader supports polygonal geometry, simple materials (no support for embedded CG/GLSL shaders) and all forms of animation available in Torque 3D. COLLADA camera, and physics elements are not supported. COLLADA lights may be instantiated in the current mission as part of importing the model.

Import Dialog
~~~~~~~~~~~~~

When a COLLADA model is first added using the World Editor, or opened in the Shape Editor, the COLLADA import dialog is displayed to control how Torque 3D will import the model.

LOD
	Controls how level-of-detail is generated for the model:

	DetectDTS
		Attempts to detect whether the shape uses the DTS node markup scheme, and if found, uses TrailingNumber mode (below). If not detected, SingleSize mode is used. The shape is determined to be using DTS markup if there is a root level node called "base*" (where * is anything) with a child node called "start*". See Scene hierarchy and LOD for more details.

	SingleSize
		All geometry in the shape will be added to a single detail level, with size given by the value in the gui. The exception is collision meshes which will be at a fixed negative detail size.

	TrailingNumber
		The detail size for geometry in the shape will be determined by the number at the end of the node (or mesh, if the modeling app does not distinguish between the two) name. An underscore before the number will be interpreted as a negative sign. eg. "mesh1" (size=1), "mesh3 1" (size=1), "mesh_1" (size=-1)

Materials Prefix
	Some COLLADA exporters generate <material> elements with generic names such as "texture1", "texture2" etc. This causes problems when the model is used in Torque since the names may clash with existing Materials. This option can be used to prefix all material names in the model so they will be unique. Press return after editing the field to update the tree view. The icon (and tooltip) next to the material name indicates whether there is already a script Material object mapped to that name.

Import Nodes
	A list of semicolon separated node names (with wildcards) to always import, even if the name matches the Ignore Nodes list. This is similar to the AlwaysExport list used with DTS exporting. For example: mount*;cam;eye nodes. Press return after editing the field to update the tree view.

Ignore Nodes
	A list of semicolon separated node names (with wildcards) to ignore on import, similar to the NeverExport list used with DTS exporting. For example: *-PIVOT;dummy. Press return after editing the field to update the tree view. Nodes that will be ignored are marked with a . Child nodes and geometry attached to an ignored node will still be imported.

Import Meshes
	A list of semicolon separated mesh names (with wildcards) to always import, even if the name matches the Ignore Meshes list. For example: bounds;Body*. Press return after editing the field to update the tree view.

Ignore Meshes
	A list of semicolon separated mesh names (with wildcards) to ignore on import. For example: *dummy. Press return after editing the field to update the tree view. Meshes that will be ignored are marked with a .

Override up_axis
	Set this option to override the up_axis specified in the DAE file. A value of Z_UP means no coordinate transformation will be applied.

Override scale
	Set this option to override the scale factor applied to the model on import. A value of 1.0 means the model will not be scaled.

Ignore bone scaling
	Because of the way Torque bakes scale information into the mesh vertices, some skinned models will load with strange geometry (the mesh is still attached to the skeleton, but appears thin and stretched out). Re-importing the model with this option set should resolve the issue.

Center model
	Setting this option causes the model to be translated such that the origin is at the center of the shape's bounding box.

Floor model
	Setting this option causes the model to be translated (in the Z axis only) such that the origin is at the bottom of the shape's bounding box. It can be used along with Center Model so that the origin is also centered (ie. at the center of the feet of a character model).

Force update materials.cs
	Setting this option causes the COLLADA loader to write all materials in the DAE file into a materials.cs script in the same folder, even if they are already mapped to another Torque Material. If not set, the COLLADA loader only creates Materials for material names that are unmapped.

Add lights to scene
	If this option is set, a SimGroup will be created (suitable for converting to a prefab) containing the imported shape as well as PointLight and SpotLight objects for any lights in the DAE file. This option is only available when adding a model through the World Editor.

	Unlike the other import options, this setting is not persistent, so you will need to set it each time you want to import the lights. Prefabs are recommended where it makes sense for the model to always include the lights. For example, a streetlamp model may include a light source in the DAE file. The first time this model is imported into Torque, the Add lights to scene setting should be set, and the resulting SimGroup saved to a prefab so you can easily instantiate the model and light multiple times in the scene.

Load from .cfg
	Loads the AlwaysImport and NeverImport lists from a DTS config file (either model_name.cfg or dtsScene.cfg, whichever is found first). This feature is useful when importing a scene previously setup for DTS export that used a config file to specify the AlwaysExport and NeverExport lists.

Save to .cfg
	Saves the AlwaysImport and NeverImport lists to a DTS config file (model_name.cfg).

Geometry
~~~~~~~~

The Torque 3D COLLADA importer supports all of the COLLADA polygonal geometry elements: <triangles>, <tristrips>, <trifans>, <polygons> and <polylist>, with non-triangular polygons automatically converted to triangles during loading. Note that if polygons are non-planar, this may introduce seams on the model, so the best option is to triangulate in the modeling application prior to exporting.

In previous versions of Torque, when exporting to DTS, a single mesh could not have more than around 11,000 triangles (the exact limit depends on the materials assigned to the mesh, and the number of shared vertices). The Torque 3D COLLADA loader however does not impose any limit on the number of vertices or polygons within a single mesh; it is up to the user to determine appropriate polygon counts for each model to ensure acceptable rendering performance.

Torque still uses 16-bit triangle indexing internally, so the COLLADA loader will automatically split meshes with too many polygons into multiple draw calls as required.

Scene hierarchy and LOD
~~~~~~~~~~~~~~~~~~~~~~~

When exporting to DTS, it was required to adhere to a strict scene hierarchy in order to specify LOD. The COLLADA loader is a bit more flexible, and is designed to import scenes regardless of whether they have been prepared for DTS export or not. The traditional DTS scene export hierarchy appears below.

::

	+-bounds                    bounds node
	+-base01                    subshape
	| +-start01                 shape branch
	| | +-Collision-1           collision mesh
	| | +-Shape128              mesh
	| |
	| +-detail128               detail
	| +-detail2                 detail
	| +-collision-1             collision detail
	|
	+-Shape2                    lower-detail
	mesh

These models are loaded as normal (ie. the loader collects the detail markers and uses them to group meshes into a single object with multiple detail levels). The above model would appear in-game as::

	+-base01
	+-start01
	  +-Collision               Object Collision with details: -1
	  +-Shape                   Object Shape with details: 32 2

The loader also supports models that do not use the above layout. These scenes are detected by the absence of the baseXXX->startXXX hierarchy (where XXX is any string), and the entire scene is added to a single subshape with a single detail level size of 2 (the fixed size can be selected in the COLLADA import dialog).

For example, this model::

	+-shape1
	| +-Box01                   mesh
	+-shape2
	  +-Cylinder01              mesh
	  +-Cylinder02              mesh
	  +-Box02                   mesh

Will be imported as::

	+-shape1
	| +-Box01                   Object Box01 with details: 2
	|-shape2
	+-Cylinder01                Object Cylinder01 with details: 2
	+-Cylinder01                Object Cylinder02 with details: 2
	  +-Box3                    Object Box03 with details: 2

Note the following:

* all objects have a single detail of size 2
* trailing numbers have not been stripped from the object names

To summarize, if you're used to exporting scenes to DTS, you are welcome to keep using the DTS scene hierarchy, and the exported COLLADA model should import exactly the same. If you're new to Torque, or don't want to use the DTS scene markup anymore, just put the detail size as a number at the end of the mesh name, and select TrailingNumber as the LOD type in the COLLADA Import interface.

Bounding Box
~~~~~~~~~~~~

A 3Space bounding box is simply an axis-aligned cuboid that fits around the shape. Torque 3D uses the centre of the bounding box as the object's origin when placed in the world editor, and it may also be used for simple collision detection.

It is important therefore for the shape bounding box to have the correct size and position. When exporting DTS models, this was done by adding a mesh called bounds to the root level of the scene. The DTS exporter would detect this special name and use the bounds mesh geometry to compute the shape bounding box.

This option is still available to models exported to COLLADA, and may be preferable if the model is animated and you want exact control over the size and position of the bounding box. For example, a walking character animation may move the feet or arms of the model outside the box containing the shape in its root pose, so you can use a custom bounding box to explicitly specify the bounding box extents.

If the DAE model does not contain a root level <node> called bounds with geometry attached to it, the Torque 3D COLLADA importer will automatically calculate a bounding box that encloses all of the geometry in the scene. For animated models, only the root (non-animated) pose is considered. For static objects this is usually adequate.

Collision Meshes
~~~~~~~~~~~~~~~~

Meshes exported to COLLADA can be marked as collision or line-of-sight collision meshes by setting the node or mesh name to Collision-X or LOSCol-X respectively, where X is a number from 1 to 8 in the case of collision meshes, or 9-16 in the case of LOS collision meshes. If your modeling application does not support -'s in names, use an underscore instead (eg. collision_1). The number at the end of the name denotes the detail size of the mesh.

Note that both types of mesh must be convex.

Billboards
~~~~~~~~~~

A mesh can be marked as a billboard prior to exporting to COLLADA by prefixing the name of the node that instantiates the mesh (or the mesh itself if the modeling application does not make that distinction) with BB:: (or BB_ if the app does not allow colons in names). Z billboards only rotate around their Z (vertical) axis to face the camera, and are specified by prefixing the node (or mesh) name with BBZ:: (or BBZ_).

Imposters (AutoBillboards)
~~~~~~~~~~~~~~~~~~~~~~~~~~

To define an imposter detail level for a shape for export to COLLADA, simply create a node at the root level with no children or geometry attached, and prefix its name with BB:: (or BB_). Then set the following user properties on the node itself:

* BB::DL
* BB::DIM
* BB::EQUATOR_STEPS
* BB::POLAR_STEPS
* BB::INCLUDE_POLES
* BB::POLAR_ANGLE

.. note:: 
	
	At the time of writing, only the OpenCOLLADA MAX exporter generates DAE files with the appropriate user properties to specify imposter settings. For other users, the Torque 3D Shape Editor can add and edit imposter detail levels.

Materials
~~~~~~~~~

In previous versions of Torque, and still when exporting to DTS, a Material was identified only by its diffuse texture. In Torque 3D, Materials encompass much more than just the diffuse texture (and may not have a diffuse texture at all), and are more akin to the materials defined in a modeling application. For this reason, the COLLADA loader names materials using the <material> element name, rather than the diffuse texture filename. For example, here is a typical material definition in a DAE file::

	<library_images>
	  <image id="myTexture.png" name="myTexture_png">
	    <init_from>myTexture.png</init_from>
	  </image>
	</library_images>
	<library_materials>
	  <material id="COLLADAMat" name="COLLADAMat">
	    <instance_effect url="#COLLADAMat-fx"/>
	  </material>
	</library_materials>
	And the corresponding Torque Material definition:

	new Material(myMat)
	{
	   diffuseMap[0] = "myTexture";
	   mapTo = "COLLADAMat";
	};

The mapTo field of the Torque Material must be set to the name of the <material> element in the DAE file (in this case "COLLADAMat"). For most COLLADA exporters, this will not be the same as the diffuse texture filename, and therefore the material will not display correctly without a script Material definition.

Fortunately, the COLLADA loader will auto-generate the materials.cs script for any unmapped materials defined in the DAE file. The initial properties of the Material are determined from the COLLADA <material>. For many Materials, these initial settings will be sufficient, but the Material Editor can be used to fine-tune properties if needed.

It should be noted that to avoid overwriting existing Materials, the COLLADA loader only generates Materials for unmapped material names. The COLLADA import dialog shows which materials are unmapped (and therefore, which Materials will be generated), and also allows you to force an update of materials.cs, including any mapped materials.

The COLLADA loader uses the following rules to determine the texture paths for the autogenerated Materials based on the path specified in the DAE file:

#. Absolute paths that reference outside the Torque game folder will be ignored, and the texture path set to the model folder. For example, "D:\images\myTexture.jpg" will become "myTexture.jpg".
#. Absolute paths that reference inside the Torque game folder will be used as expected. For example, "D:\Torque\game\art\myTexture.jpg" will become "art/myTexture.jpg".
#. Relative paths will be appended to the model folder. For example, "./textures/myTexture.jpg" for a model in the "art/shapes/trees" folder will become "art/shapes/trees/textures/myTexture.jpg".

Animation
~~~~~~~~~

The following table summarizes the type of animations available using the COLLADA loader.

Node transform
	Supported using animated COLLADA node transforms (rotate, translate etc).

Skeletal animation
	Supported using animated COLLADA node transforms (rotate, translate etc) with a <skin> controller to provide vertex weights.

Visibility
	Supported using the FCOLLADA <node> extension (with animated visibility).

UV (texture mapping)
	UV keyframe animation is not supported in Torque 3D. Certain UV transformations such as offset and rotation can be animated using the Material Editor.

Morph
	Morph (vertex keyframe) animation is not supported in Torque 3D.

Torque animation sequences are implemented using COLLADA <animation_clip> elements. If the DAE file contains <animation> elements, but does not contain any <animation_clip>s, the loader will automatically create a cyclic animation sequence called ambient using all of the <animation>s. You can use the Shape Editor tool to split this combined sequence into multiple sequences if required.

DAE to DTS
~~~~~~~~~~

Torque's native model format, DTS, is much faster to read than COLLADA, so once a DAE file has been imported, the loader automatically saves the 3space model to a DTS file. For example, importing myShape.dae will generate myShape.cached.dts. The next time Torque attempts to load the DAE file, it compares the timestamps of the two files, and if the cached DTS is newer, then it loads that instead. Re-exporting the DAE (or modifying it by hand) will cause the DAE to be re-imported, and the cached DTS overwritten with the latest model.

Demos and released games can ship only the cached DTS files if desired. Torque will automatically load the cached DTS if the DAE is missing. Datablocks and mission files should continue to refer to the DAE file.

A console function is available to batch-convert a set of DAE files to DTS. The function takes a single argument that specifies a wildcard pattern to match DAE files to be converted. For example::

	// convert ALL dae files in the game directory
	convertCOLLADAModels("");

	// convert all dae files in the art/shapes folder
	convertCOLLADAModles("art/shapes/*.dae");

	// convert dae files in the art folder with 'tree' in the filename
	convertCOLLADAModels("art/*tree*.dae");

A command line tool, dae2dts, is also available for batch model conversion, or even for integration into a custom art pipeline. For example, a modeling app could be scripted to export to COLLADA, then call dae2dts to convert to DTS.

Google Earth (KMZ) models
~~~~~~~~~~~~~~~~~~~~~~~~~

Models exported from Google Sketchup or downloaded from the Google 3D warehouse can be loaded directly into Torque 3D. Just export the Sketchup (.skp) file to GoogleEarth 4 format (in Sketchup: File->Export->3D Model), which will produce a .kmz file. This is a normal zip file containing the DAE file and textures. For example:

cowboy.kmz
+-doc.kml
+-models
| +-cowboy.dae
+-images
  +-texture0.jpg
  +-texture1.jpg
  +-texture2.jpg

Torque understands that this is really just a zip file, and you don't even need to unzip it to load the COLLADA model! KMZ files will appear in the Torque 3D World Editor in the same way as DTS and DAE files. When the model is imported, Torque 3D will automatically extract the converted DAE file and textures into the KMZ folder, but mission files and datablocks should continue to refer to the KMZ file itself. For example::

	datablock PlayerData(CowboyData : DefaultPlayerData)
	{
	   shapeFile = "~/data/shapes/players/cowboy.kmz";
	   renderFirstPerson = false;
	   emap = true;
	};

.. note::

	Note that the .kmz file is treated as a normal directory ("cowboy" with no .kmz extension), and the path inside the .kmz file is required (models/cowboy.dae).

	Sketchup 7 and later can export directly to COLLADA, so there is no need to use KMZ files unless desired.

	There is a known bug in the Google Sketchup 6 COLLADA exporter, in that it exports materials with the transparency inverted (1.0 - transparency). The Torque COLLADA loader automatically corrects this.

	One caution with this type of file is that all materials are exported as double-sided (using the GOOGLEEARTH extension). For most models this is not desired, as it means the GPU will not cull backfaces (triangles not facing the camera) and render polygons twice. The double-sided property can be disabled for the relevant Material using the Material Editor.

Troubleshooting
---------------

Torque crashes when loading or displaying a COLLADA model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Support for COLLADA in Torque 3D is still relatively new - it is possible that bugs or non-standard models will cause Torque to crash. If you think this is the case, please report the issue in the Torque 3D bug report forums, along with the model (if possible) and a description of how to reproduce the problem. Providing a sample model and a clear, detailed bug report is by far the most effective way to get the problem resolved.

Materials are missing/wrong
~~~~~~~~~~~~~~~~~~~~~~~~~~~

A major difference between a COLLADA and a DTS model is in the naming of materials. Materials in DTS files are generally named using the diffuse texture filename. For example, a DTS material that uses the texture wood.jpg would be called wood. When Torque loads this model, if there are no script Materials defined that mapTo wood, the engine looks for a JPG, PNG or BMP file with that name in the same directory as the model.

However, in a modeling application, a material usually encompasses much more than just the diffuse texture. When a model is exported to the COLLADA file format, the name of the material in the modeling app is stored in the <material> tag in the COLLADA file.

It is this <material> name that is used by the COLLADA loader as the name of the Material in Torque. If no script Material is defined that maps to this name, the engine will look for a JPG, PNG, TGA or BMP texture in the same way. So there are two approaches to get materials to show up correctly for COLLADA models:

#. Name the material in the 3D app the same as the diffuse texture file.
#. Create a materials.cs file in the same directory as the model, and define a script Material object that maps to each COLLADA material. This is the recommended approach.

After importing, use the Material Editor tool (or manually inspect the materials.cs script) to modify material settings if required.

COLLADA models are slow to load or render
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Torque DTS file format is a binary format designed to make loading models into Torque extremely fast - in many cases, whole arrays of data are loaded directly into memory with no conversion at all.

By contrast, the COLLADA file format is an extremely flexible human-readable text format - but that flexibility comes at a cost. Arrays of numbers need to be converted to their binary equivalents, and the structure and layout of a COLLADA model needs to be converted into the form expected by Torque. It will always be much slower to load a COLLADA file than a Torque DTS model.

To get around this limitation, the loader automatically saves the converted COLLADA model to a DTS file. For example, myModel.dae will be saved to myModel.cached.dts when it is first loaded by Torque. The next time the model is loaded, the cached DTS will be loaded instead, which will be much faster. If the COLLADA model changes (ie. myModel.dae has a modification time later than myModel.cached.dts), Torque will reload the COLLADA file, and overwrite the cached DTS file with the new model data.

These 'cached' DTS files can be shipped instead of the DAE files with a demo or game to avoid having to release the text-format COLLADA files. If the DAE is not present, Torque will always load the cached DTS. Datablocks and mission files should continue to point at the DAE file.

Another thing to consider is the polygon count of the model. COLLADA models are essentially unlimited in the number of polygons that they support. All that data needs to be loaded into memory before converting to 3space (which supports only 16 bit triangle indices, meaning larger meshes may need to be split up). As well as being slow to load, a model with too many polygons will also lead to poor rendering performance.

Model transparency is incorrect
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some exporters do not comply with the COLLADA specification when it comes to material transparency. For example Google Sketchup 6 always exports materials with the transparency inverted (1.0 - transparency). The Torque COLLADA loader attempts to detect inverted transparency automatically (a warning message will be generated in the console for all converted elements).

Check the transparency elements of each material in the .dae file. If the opaque attribute of the <transparent> element is missing or set to A_ONE, then the COLLADA loader calculates transparency as::

	1.0 - (<transparency> * <transparent>[3])

If the opaque attribute is set to RGB_ZERO, then transparency is calculated as::

	<transparency> * ((<transparent>[0] + <transparent>[1] + <transparent>[2]) / 3)

Transparency, as well as other Material properties, can be easily corrected in the Material Editor.

Geometry is missing or the wrong size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Check the console for warnings or errors. In particular, note that the COLLADA loader only supports polygonal geometry, and will generate a warning message such as:
COLLADA <xxx> element in YYY is not supported. If it encounters unsupported geometry such as <line>, <spline> <capsule> etc. The best option is to convert non-polygonal geometry in your modeling application prior to export, but you could also try the COLLADA Refinery toolchain.
Try importing the model back into your modeling application. If this fails, or gives unexpected results, there may be a problem with the COLLADA export feature of your modeling application.
* Check that you have set up your scene correctly for LOD. The Shape Editor tool may be used to inspect the detail levels present in the model.
* Check the scale of the object. At the top of the .dae file, there is usually an element similar to this::

	<unit name="inches" meter="0.0254"/>

This value represents the units that the model is measured in, and is applied as a global scaler to the entire model by the COLLADA loader. Unfortunately, not all applications have the same idea of scale, so a model that is 1 meter high might be very large in one application but very small in another. The <unit> value is displayed and can be overridden in the COLLADA import dialog, so try increasing or decreasing the value by a factor of 10 or 100 to see if the model becomes visible.

Skinned meshes are distorted
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Check the console for warnings or errors. The COLLADA loader will generate such messages if it encounters problems with the model.
* If the mesh is correctly attached to the skeleton, but appears "stretched out", try re-importing the model with the Ignore bone scaling option set in the Import Dialog.
* Try re-importing the model with the Override up_axis set to Z_UP (to prevent the loader applying a coordinate-system transformation) and Override scale set to 1.0 (to prevent the loader applying a global scaler).
* Try re-exporting the model with the Bake Transforms or Single Matrix option set in the exporter.
* If bones are missing from the shape (making the skinned mesh appear crushed in on itself), make sure everything in the scene is unhidden/unfrozen prior to exporting. Some COLLADA exporters will not export correctly if scene elements are hidden or frozen.

Some bones do not animate correctly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Torque stores animations as a series of regularly spaced keyframes. COLLADA supports this method as well, but animations may also be exported as animation curves defined by control points. In both cases, the COLLADA loader samples the animation data to produce a set of keyframes for Torque. The sampling frequency is determined by finding the minimum time between exported keyframes (clamped to a rate of 15-60 frames per second).

For COLLADA animations exported with the Sample Animation option set, this method will sample the exact exported keyframes, meaning no interpolation is required, and the animation should play perfectly in Torque.

For animations exported as curve control points, the loader must interpolate between points. This can sometimes cause problems if the animation curves are not continuous; for example, if a rotation angle wraps around from +180 to -180 degrees. The symptom of this issue is bones flipping around on some frames when the animation is played in Torque. This can be resolved by setting the Sample Animation and/or Single Matrix/Baked Transform export options.

Appendix 1: Material settings
-----------------------------

*TBD*

Appendix 2: Supported Extensions
--------------------------------

*TBD*

Appendix 3: Supported COLLADA elements
--------------------------------------

*TBD*
