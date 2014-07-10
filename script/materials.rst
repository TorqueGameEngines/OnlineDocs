Materials
=========

Classes, structures, functions, and variables related to Torque 3D's material system.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/CustomMaterial

Functions
---------

.. cpp:function:: void addMaterialMapping(string texName, string matName)

	Maps the given texture to the given material. Generates a console warning before overwriting. Material maps are used by terrain and interiors for triggering effects when an object moves onto a terrain block or interior surface using the associated texture.

.. cpp:function:: string getMaterialMapping(string texName)

	Returns the name of the material mapped to this texture. If no materials are found, an empty string is returned.

	:param texName: Name of the texture

Variables
---------

.. cpp:member:: int $pref::Video::defaultAnisotropy

	Global variable defining the default anisotropy value. Controls the default anisotropic texture filtering level for all materials, including the terrain. This value can be changed at runtime to see its affect without reloading.

.. cpp:member:: void  dumpMaterialInstances

	Dumps a formatted list of currently allocated material instances to the console.

.. cpp:member:: void  reInitMaterials

	Flushes all procedural shaders and re-initializes all active material instances.
