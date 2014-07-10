Miscellaneous
=============

Miscellaneous environmental and level objects.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/ConvexShape
	class/LevelInfo
	class/Marker
	class/MissionArea
	class/MissionMarker
	class/MissionMarkerData
	class/OcclusionVolume
	class/Path
	class/PhysicalZone
	class/Portal
	class/Prefab
	class/ReflectorDesc
	class/SpawnSphere
	class/TerrainMaterial
	class/TimeOfDay
	class/WayPoint
	class/Zone

Enumeration
-----------

.. cpp:member:: enum  MarkerKnotType

	The type of knot that this marker will be.

	:param Normal: Knot will have a smooth camera translation/rotation effect.
	:param Only: Will do the same for translations, leaving rotation un-touched.
	:param Kink: The rotation will take effect immediately for an abrupt rotation change.

.. cpp:member:: enum  MarkerSmoothingType

	The type of smoothing this marker will have for pathed objects.

	:param Spline: Marker will cause the movements of the pathed object to be smooth.
	:param Linear: Marker will have no smoothing effect.

Functions
---------

.. cpp:function:: MissionArea  getMissionAreaServerObject()

	Get the MissionArea object, if any.
