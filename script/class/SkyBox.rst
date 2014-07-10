SkyBox
======

Represents the sky with an artist-created cubemap.

Inherit:
	:doc:`SceneObject`

Description
-----------

Represents the sky with an artist-created cubemap.

SkyBox is not a directional light and should be used in conjunction with a Sun object.


Fields
------


.. cpp:member:: bool  SkyBox::drawBottom

	If false the bottom of the skybox is not rendered.

.. cpp:member:: float  SkyBox::fogBandHeight

	The height (0-1) of the fog band from the horizon to the top of the SkyBox .

.. cpp:member:: string  SkyBox::Material

	The name of a cubemap material for the sky box.

.. cpp:member:: void  SkyBox::postApply

