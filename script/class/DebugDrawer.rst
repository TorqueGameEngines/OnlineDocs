DebugDrawer
===========

A debug helper for rendering debug primitives to the scene.

Inherit:
	:doc:`SimObject`

Description
-----------

The DebugDrawer is used to render debug primitives to the scene for testing. It is often useful when debugging collision code or complex 3d algorithms to have them draw debug information, like culling hulls or bounding volumes, normals, simple lines, and so forth.

A key feature of the DebugDrawer is that each primitive gets a "time to live" (TTL) which allows them to continue to render to the scene for a fixed period of time. You can freeze or resume the system at any time to allow you to examine the output.

Example::

	DebugDraw.drawLine( %player.getMuzzlePoint( 0 ), %hitPoint );
	DebugDraw.setLastTTL( 5000 ); // 5 seconds.

The DebugDrawer renders solely in world space and all primitives are rendered with the cull mode disabled.

Methods
-------

.. cpp:function:: void DebugDrawer::drawBox(Point3F a, Point3F b, ColorF color)

	Draws an axis aligned box primitive within the two 3d points.

.. cpp:function:: void DebugDrawer::drawLine(Point3F a, Point3F b, ColorF color)

	Draws a line primitive between two 3d points.

.. cpp:function:: void DebugDrawer::setLastTTL(int ms)

	Sets the "time to live" (TTL) for the last rendered primitive.

.. cpp:function:: void DebugDrawer::setLastZTest(bool enabled)

	Sets the z buffer reading state for the last rendered primitive.

.. cpp:function:: void DebugDrawer::toggleDrawing()

	Toggles the rendering of DebugDrawer primitives.

.. cpp:function:: void DebugDrawer::toggleFreeze()

	Toggles freeze mode which keeps the currently rendered primitives from expiring.
