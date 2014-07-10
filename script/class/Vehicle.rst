Vehicle
=======

Base functionality shared by all Vehicles (FlyingVehicle, HoverVehicle, WheeledVehicle).

Inherit:
	:doc:`ShapeBase`

Description
-----------

This object implements functionality shared by all Vehicle types, but should not be instantiated directly. Create a FlyingVehicle, HoverVehicle, or WheeledVehicle instead.

Fields
------

.. cpp:member:: bool  Vehicle::disableMove

	When this flag is set, the vehicle will ignore throttle changes.

.. cpp:member:: float  Vehicle::workingQueryBoxSizeMultiplier  [static]

	How much larger the mWorkingQueryBox should be made when updating the working collision list. The larger this number the less often the working list will be updated due to motion, but any non-static shape that moves into the query box will not be noticed.

.. cpp:member:: int  Vehicle::workingQueryBoxStaleThreshold  [static]

	The maximum number of ticks that go by before the mWorkingQueryBox is considered stale and needs updating. Other factors can cause the collision working query box to become invalidated, such as the vehicle moving far enough outside of this cached box. The smaller this number, the more times the working list of triangles that are considered for collision is refreshed. This has the greatest impact with colliding with high triangle count meshes.
