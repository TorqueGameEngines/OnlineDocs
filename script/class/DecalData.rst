DecalData
=========

A datablock describing an individual decal.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

A datablock describing an individual decal.

The textures defined by the decal Material can be divided into multiple rectangular sub-textures as shown below, with a different sub-texture selected by all decals using the same DecalData (via frame) or each decal instance (via randomize).

Example of a Decal imagemap

Example::

	datablock DecalData(BulletHoleDecal)
	{
	   material = "DECAL_BulletHole";
	   size = "5.0";
	   lifeSpan = "50000";
	   randomize = "1";
	   texRows = "2";
	   texCols = "2";
	   clippingAngle = "60";
	};


Methods
-------


.. cpp:function:: void DecalData::postApply()

	Recompute the imagemap sub-texture rectangles for this DecalData .

	Example::

		// Inform the decal object to reload its imagemap and frame data.
		%decalData.texRows = 4;
		%decalData.postApply();

Fields
------


.. cpp:member:: float  DecalData::clippingAngle

	The angle in degrees used to clip geometry that faces away from the decal projection direction.

.. cpp:member:: float  DecalData::fadeEndPixelSize

	LOD value - size in pixels at which decals of this type are fully faded out. This should be a smaller value than fadeStartPixelSize .

.. cpp:member:: float  DecalData::fadeStartPixelSize

	LOD value - size in pixels at which decals of this type begin to fade out. This should be a larger value than fadeEndPixelSize . However, you may also set this to a negative value to disable lod-based fading.

.. cpp:member:: int  DecalData::fadeTime

	Time (in milliseconds) over which to fade out the decal before deleting it at the end of its lifetime.

.. cpp:member:: int  DecalData::frame

	Index of the texture rectangle within the imagemap to use for this decal.

.. cpp:member:: int  DecalData::lifeSpan

	Time (in milliseconds) before this decal will be automatically deleted.

.. cpp:member:: string  DecalData::Material

	Material to use for this decal.

.. cpp:member:: bool  DecalData::randomize

	If true, a random frame from the imagemap is selected for each instance of the decal.

.. cpp:member:: char  DecalData::renderPriority

	Default renderPriority for decals of this type (determines draw order when decals overlap).

.. cpp:member:: float  DecalData::size

	Width and height of the decal in meters before scale is applied.

.. cpp:member:: int  DecalData::texCols

	Number of columns in the supplied imagemap. Use texRows and texCols if the imagemap frames are arranged in a grid; use textureCoords to manually specify UV coordinates for irregular sized frames.

.. cpp:member:: int  DecalData::texRows

	Number of rows in the supplied imagemap. Use texRows and texCols if the imagemap frames are arranged in a grid; use textureCoords to manually specify UV coordinates for irregular sized frames.

.. cpp:member:: int  DecalData::textureCoordCount

	Number of individual frames in the imagemap (maximum 16).

.. cpp:member:: RectF  DecalData::textureCoords [16]

	An array of RectFs (topleft.x topleft.y extent.x extent.y) representing the UV coordinates for each frame in the imagemap.
