CloudLayer
==========

A layer of clouds which change shape over time and are affected by scene lighting.

Inherit:
	:doc:`SceneObject`

Description
-----------

CloudLayer always renders overhead, following the camera. It is intended as part of the background of your level, rendering in front of Sky/Sun type objects and behind everything else.

The illusion of clouds forming and changing over time is controlled by the normal/opacity texture and the three sets of texture animation parameters. The texture is sampled three times. The first sample defines overall cloud density, where clouds are likely to form and their general size and shape. The second two samples control how it changes over time; they are combined and used as modifiers to the first sample.

CloudLayer is affected by scene lighting and is designed to be used in scenes with dynamic lighting or time of day changes.

Fields
------

.. cpp:member:: ColorF  CloudLayer::baseColor

	Base cloud color before lighting.

.. cpp:member:: float  CloudLayer::coverage

	Fraction of sky covered by clouds 0-1.

.. cpp:member:: float  CloudLayer::exposure

	Brightness scale so CloudLayer can be overblown if desired.

.. cpp:member:: float  CloudLayer::height

	Abstract number which controls the curvature and height of the dome mesh.

.. cpp:member:: Point2F  CloudLayer::texDirection [3]

	Controls the direction this slot scrolls.

.. cpp:member:: float  CloudLayer::texScale [3]

	Controls the texture repeat of this slot.

.. cpp:member:: float  CloudLayer::texSpeed [3]

	Controls the speed this slot scrolls.

.. cpp:member:: filename  CloudLayer::texture

	An RGBA texture which should contain normals and opacity (density).

.. cpp:member:: float  CloudLayer::windSpeed

	Overall scalar to texture scroll speed.
