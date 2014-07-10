ConvexShape
===========

A renderable, collidable convex shape defined by a collection of surface planes.

Inherit:
	:doc:`SceneObject`

Description
-----------

ConvexShape is intended to be used as a temporary asset for quickly blocking out a scene or filling in approximate shapes to be later replaced with final assets. This is most easily done by using the WorldEditor's Sketch Tool.

Fields
------

.. cpp:member:: string  ConvexShape::Material

	Material used to render the ConvexShape surface.

.. cpp:member:: string  ConvexShape::surface

	Do not modify, for internal use.
