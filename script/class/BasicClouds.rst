BasicClouds
===========

Renders up to three layers of scrolling cloud-cover textures overhead.

Inherit:
	:doc:`SceneObject`

Description
-----------

BasicClouds always renders overhead, following the camera. It is intended as part of the background of your level, rendering in front of Sky/Sun type objects and behind everything else.

The parameters controlling the rendering of each texture are refered to and grouped as 'layers'. They are rendered in sequential order, so, layer 1 obscures layer 0, and so on.

BasicClouds is not affected by scene lighting and is therefore not appropriate for scenes in which lighting radically changes, such as day/night.

Fields
------

.. cpp:member:: float  BasicClouds::height [3]

	Abstract number which controls the curvature and height of the dome mesh.

.. cpp:member:: bool  BasicClouds::layerEnabled [3]

	Enable or disable rendering of this layer.

.. cpp:member:: Point2F  BasicClouds::texDirection [3]

	Texture scroll direction for this layer, relative to the world axis.

.. cpp:member:: Point2F  BasicClouds::texOffset [3]

	UV offset for this layer.

.. cpp:member:: float  BasicClouds::texScale [3]

	Texture repeat for this layer.

.. cpp:member:: float  BasicClouds::texSpeed [3]

	Texture scroll speed for this layer.

.. cpp:member:: filename  BasicClouds::texture [3]

	Texture for this layer.
