CubemapData
===========

Used to create static or dynamic cubemaps.

Inherit:
	:doc:`SimObject`

Description
-----------

This object is used with Material, WaterObject, and other objects for cubemap reflections.

A simple declaration of a static cubemap:

Example::

	singleton CubemapData( SkyboxCubemap )
	{
	   cubeFace[0] = "./skybox_1";
	   cubeFace[1] = "./skybox_2";
	   cubeFace[2] = "./skybox_3";
	   cubeFace[3] = "./skybox_4";
	   cubeFace[4] = "./skybox_5";
	   cubeFace[5] = "./skybox_6";
	};

Methods
-------

.. cpp:function:: string CubemapData::getFilename()

	Returns the script filename of where the CubemapData object was defined. This is used by the material editor. Reimplemented from SimObject .

.. cpp:function:: void CubemapData::updateFaces()

	Update the assigned cubemaps faces.

Fields
------

.. cpp:member:: filename  CubemapData::cubeFace [6]

	The 6 cubemap face textures for a static cubemap. They are in the following order: 
	
	* cubeFace[0] is -X
	* cubeFace[1] is +X
	* cubeFace[2] is -Z
	* cubeFace[3] is +Z
	* cubeFace[4] is -Y
	* cubeFace[5] is +Y 

.. cpp:member:: bool  CubemapData::dynamic

	Set to true if this is a dynamic cubemap. The default is false.

.. cpp:member:: float  CubemapData::dynamicFarDist

	The far clip distance used when rendering to the dynamic cubemap.

.. cpp:member:: float  CubemapData::dynamicNearDist

	The near clip distance used when rendering to the dynamic cubemap.

.. cpp:member:: int  CubemapData::dynamicObjectTypeMask

	The typemask used to filter the objects rendered to the dynamic cubemap.

.. cpp:member:: int  CubemapData::dynamicSize

	The size of each dynamic cubemap face in pixels.
