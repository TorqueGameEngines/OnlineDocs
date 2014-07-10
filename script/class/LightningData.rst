LightningData
=============

emitter object.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Common data for a Lightning emitter object.


Fields
------


.. cpp:member:: SFXTrack LightningData::strikeSound

	Sound profile to play when a lightning strike occurs.

.. cpp:member:: string  LightningData::strikeTextures [8]

	List of textures to use to render lightning strikes.

.. cpp:member:: SFXTrack LightningData::thunderSounds [8]

	List of thunder sound effects to play. A random one of these sounds will be played shortly after each strike occurs.
