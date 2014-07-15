Overview of Content Pipeline
============================

The main tool for importing and manage content in Torque 3D is the World Editor. However the World Editor is not a tool for creating game objects. Objects must be created using applications appropriate for the object type.

Importing 3D Models
-------------------

Torque 3D uses two different formats for 3D geometry and animation data: *Collada* and *DTS.*

Collada is intended to be the primary model format during development of a Torque 3D game, as there are Collada importers and exporters for almost every 3D modeling application around. Collada is a format for interchanging models between digital content creation applications. Torque 3D can load geometry, material and animation data directly from Collada DAE files and is based on version 1.4.1 of the Collada specification. Collada is an XML based file format, meaning DAE files may be opened, viewed and edited in any text editor.

The Torque 3D supports all of the Collada polygonal geometry elements: <triangles>, <tristrips>, <trifans>, <polygons> and <polylist>, with non-triangular polygons automatically converted to triangles during loading. Note that if polygons are non-planar, this may introduce seams on the model, so the best option is to triangulate in the modeling application prior to exporting.

Many 3D modeling applications come with built-in Collada import and export functionality, but third party plugins are also available that may be more stable, updated more frequently and give better results. In particular, OpenCOLLADA is recommended for both Autodesk 3ds Max and Maya.

While DTS is a format internal engine format intended for the models that ship with the released version of a game. It is an optimized, binary format that loads much faster than Collada and also provides a small measure of protection for art assets.

Shipping 3D Models
------------------

The normal workflow is to use Collada during development, then make sure all models are converted to DTS for a shipping release build. There are several different approaches available to achieve that.

It can be accomplished by either use the cached DTS files that Torque 3D saves in the same folder as the Collada file during import. Every time the DAE file would be loaded, Torque 3D first checks if there is a newer cached.dts file in the same folder and if so, loads that instead. For simple models, this means you can simply strip the DAEs from the released version of the game, leaving only the cached.dts files. All datablocks and mission files still refer to the DAE model, but Torque will automatically load the cached.dts in its place. 

.. note:: 

	The cached.dts file represents the converted DAE model only - changes applied using a TSShapeConstructor script are only made to the in-memory shape and are not included in this file.

Anther way is to use the dae2dts tool as a part of the build process to convert Collada files into DTS. If using this approach, datablocks and mission files should refer to the coverted DTS output file, not the original DAE file. The dae2dts tool bakes any model transformations made using TSShapeConstructor into the final DTS model, so make sure that the TSShapeConstructor script used with dae2dts is not run when loading the DTS output file into Torque 3D (by making the filenames different, or keeping the output DTS file in a different folder) or the changes will be applied twice!

Of course, there is no reason you could not use one TSShapeConstructor script with dae2dts to bake changes, then use another TSShapeConstructor script when loading the baked DTS file into Torque 3D to apply dynamic changes (like auto-loading all sequence files within a folder for example).

There also exist some modeling applications with DTS file export support. However, those are no longer recommended as they place limitations on the exported files while the Torque 3D Collada importer is much more flexible.

Coordinate System
-----------------

Torque uses the same coordinate system as 3ds Max where characters and vehicles should are facing the +Y axis. 

.. figure:: images/torque_coords.png

	The Torque 3D coordinate system.

Thus the coordinate system is equivalent to Z_UP in Collada and the importer will automatically convert models using X_UP or Y_UP to this coordinate system.
However, some Collada exporters may generate models with a wrong or missing <up_axis> element (Z_UP is assumed if <up_axis> is not specified). In this case, the Collada import dialog can be used to override the value.

Units
-----

When exporting to Collada, you are free to work in whatever units you like. They will be scaled appropriately when importing the model into Torque 3D.

When creating a model, it makes sense to work in units appropriate to the type of object being modeled. For example, it may be convenient to model a building in meters (or feet), but a small object like a pen would be better modeled in cm (or inches). Normally the modeler would be forced to choose a single unit for both objects, and one object would end up having awkward measurements; like a building that is 2000 units high, or a pen that is only 0.14 units long.

Collada provides a mechanism to specify the units used when modeling the object. This is very important, since it allows a set of objects modeled in completely different units to be imported into Torque 3D with the correct scale relative to each other. This is done using the Collada <unit> element, which appears near the top of the .dae file and specifies the units-per-meter used for all positional values in the file such as vertex and node positions, translation animations etc. Torque 3D uses this value as a global scale factor which is applied to the entire model on import.

Many modeling applications allow the user to specify the units to be used, or alternatively, the option may be available when exporting the model to Collada.

It is up to the modeler to ensure that models are created with appropriate units in mind. For example, if a chair was modeled at 5 units high in the modeling application (simply because that was a convenient value for the modeler), then exported to DAE with units set to feet, then the chair would appear to be the equivalent of 5 feet high in Torque 3D! The Torque 3D Collada import dialog allows you to override the <unit> scale specified in the DAE file, for cases like this when the modeler has not taken units into account.

Texture Files
-------------

Torque 3D supports several texture file formats: BMP, GIF, JEPG, JPG, JNG, MNG, PNG, TGA, DDS. Note that texture dimensions should be powers of 2 wherever possible such as 16, 32, 64, 128, 256, so forth, although they need not be square. Some older hardware is unable to process non-power-of-2 textures at all, and even modern hardware will pad such textures up to the next largest power of 2 when loaded which wastes VRAM.

Normal/Bump Maps
----------------

Torque 3D uses DirectX style normal maps, where the green (Y) channel contains the DOWN vector. This is opposite to the system OpenGL uses which has the UP vector in the green channel. If your normal maps appear backwards in Torque 3D, you may need to invert the green channel manually.
