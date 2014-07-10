RenderShapeExample
==================

An example scene object which renders a DTS.

Inherit:
	:doc:`SceneObject`

Description
-----------

This class implements a basic SceneObject that can exist in the world at a 3D position and render itself. There are several valid ways to render an object in Torque. This class makes use of the 'TS' (three space) shape system. TS manages loading the various mesh formats supported by Torque as well was rendering those meshes (including LOD and animation...though this example doesn't include any animation over time).

See the C++ code for implementation details.

Fields
------

.. cpp:member:: filename  RenderShapeExample::shapeFile

	The path to the DTS shape file.
