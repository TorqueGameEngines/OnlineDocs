DAE to DTS
************

The dae2dts tool is a command-line application used to convert COLLADA (DAE) models to Torque shape (DTS) or animation (DSQ) files. The tool is invoked from the windows command prompt as follows::

	dae2dts [options] daeFilename
	
Where daeFilename is the path to the COLLADA (.dae) file to convert (the DAE file does not need to be in the same folder as the dae2dts tool). The tool exit code is zero on success or non-zero on failure, making it suitable for use within a larger batch conersion process. The following options are available:


* **--config cfgFilename** Set the conversion configuration filename. Reserved for future use; not currently supported.
* **--output dtsFilename** Set the output DTS filename. If not specified, the output will have the same base name as the input DAE file, but with DTS (or DSQ) extension.
* **--dsq** If set, all sequences in the shape will be saved to DSQ files (one for each sequence) instead of being embedded in the DTS file. The generated DTS file will not contain any animation sequences.
* **--dsq-only** Same as --dsq, but no DTS file will be saved (handy for animation only input files).
* **--compat** If set, the tool will attempt to write to DTS v24 for compatibility with non-T3D engines (TGE, TGEA, ShowToolPro etc). By default, the dae2dts tool outputs DTS v26 files which can only be loaded in T3D based products (T3D can also load DTS v24 files). DTS v24 supports only a single UV set, around 11000 maximum triangles per mesh, and does not support vertex colors. Also, COLLADA models that use autobillboards may not be saved correctly to DTS v24.
* **--diffuse** If set, the tool will use each material's diffuse texture as the material name (instead of the COLLADA <material> name) for compatibility with simple TGE materials.
* **--materials** If set, the tool will generate a materials.cs script in the output folder to define Materials used in the shape.
* **--verbose** If set, the tool will output progress information 

Examples
==========
A COLLADA model, player.dae, contains 3 animation clips: root, run, shoot::

	# Convert to 'player.dts' (all animations are embedded in the DTS file)
	dae2dts player.dae

	# Convert to 'orc.dts', and generate 'orc_root.dsq', 'orc_run.dsq' and
	# 'orc_shoot.dsq' (all files compatible with TGE, TGEA and ShowToolPro)
	dae2dts --compat --dsq --output orc.dts C:\shapes\player.dae

	# Extract animations only and store in 'player_root.dsq', 'player_run.dsq' and
	# 'player_shoot.dsq'
	dae2dts --dsq-only player.dae

Materias
=========
A major difference between a COLLADA and a DTS model is in the naming of materials. DTS files only support a single material name, which historically (TGE) has been used to reference the diffuse texture. For example, a DTS material that uses the texture wood.jpg would be called wood. When Torque loads this model, if there are no script Materials defined that mapTo wood, the engine looks for a JPG, PNG, or BMP file with that name in the same directory as the model.

However, in a modelling application (and in Torque3D!), a material encompasses much more than just the diffuse texture. When a model is exported to the COLLADA file format, the name of the material in the modelling app is stored in the <material> tag in the COLLADA file.

The default behavior of the dae2dts tool is to use the COLLADA <material> element name as the material name in the DTS file, which means the model will not display correctly in Torque unless materials.cs has been setup correctly. There are two approaches to solve this issue for dae2dts converted models:

#. Name the material in the 3D app the same as the diffuse texture file, or use the --diffuse option to do it automatically at conversion time. This is the recommended approach for engines that do not support scripted Materials (TGE, ShowToolPro).
#. Create a materials.cs file in the same directory as the model (or have the tool create it for you), and define a script Material object that maps to each COLLADA material name. This is the recommended approach if your engine supports scripted Materials as it will give you greater flexibility in naming your materials.

Futher Reading
===============
See the *Torque COLLADA Loader*(Artist Guide/Formats/COLLADA) documentation for more details about how Torque loads COLLADA files, and for which COLLADA features are supported.

TSShapeContructor allows you to modify the loaded COLLADA model in-memory before it is saved to DTS or DSQ. The TSShapeConstructor script can be created by hand, or by using the T3D Shape Editor tool (available in the T3D demo for non-T3D licensees). See TSShapeConstructor in the Torque 3D - Script Manual for more details.