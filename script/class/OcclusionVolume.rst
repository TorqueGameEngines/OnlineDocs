OcclusionVolume
===============

An invisible shape that causes objects hidden from view behind it to not be rendered.

Inherit:
	:doc:`SceneObject`

Description
-----------

OcclusionVolume is a class for scene optimization. It's main use is for outdoor spaces where zones and portals do not help in optimizing scene culling as they almost only make sense for modeling visibility in indoor scenarios (and for connecting indoor spaces to outdoor spaces).

During rendering, every object that is fully behind an occluder

Be aware that occluders add overhead to scene culling. Only if this overhead is outweighed by the time saved by not rendering hidden objects, is the occluder actually effective. Because of this, chose only those spots for placing occluders where a significant number of objects will be culled from points that the player will actually be at during the game.

Like zones and portals, OcclusionVolumes may have a default box shape or a more complex.


Fields
------


.. cpp:member:: string  OcclusionVolume::edge

	For internal use only.

.. cpp:member:: string  OcclusionVolume::plane

	For internal use only.

.. cpp:member:: string  OcclusionVolume::point

	For internal use only.
