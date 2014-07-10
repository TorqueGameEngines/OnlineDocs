SFXEmitter
==========

An invisible 3D object that emits sound.

Inherit:
	:doc:`SceneObject`

Description
-----------

Sound emitters are used to place sounds in the level. They are full 3D objects with their own position and orientation and when assigned 3D sounds, the transform and velocity of the sound emitter object will be applied to the 3D sound.

Sound emitters can be set up of in either of two ways:

* By assigning an existing SFXTrack to the emitter's track property. In this case the general sound setup (3D, streaming, looping, etc.) will be taken from track. However, the emitter's own properties will still override their corresponding properties in the track's SFXDescription.
* By directly assigning a sound file to the emitter's fileName property. In this case, the sound file will be set up for playback according to the properties defined on the emitter.

Using playOnAdd emitters can be configured to start playing immediately when they are added to the system (e.g. when the level objects are loaded from the mission file).

.. note::

	A sound emitter need not necessarily emit a 3D sound. Instead, sound emitters may also be used to play non-positional sounds. For placing background audio to a level, however, it is usually easier to use LevelInfo::soundAmbience.

Sound Emitters and Networking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is important to be aware of the fact that sounds will only play client-side whereas SFXEmitter objects are server-side entities. This means that a server-side object has no connection to the actual sound playing on the client. It is thus not possible for the server-object to perform queries about playback status and other source-related properties as these may in fact differ from client to client.

Methods
-------

.. cpp:function:: SFXSource  SFXEmitter::getSource()

	Get the sound source object from the emitter.

	:return: The sound source used by the emitter or null.

.. cpp:function:: void SFXEmitter::play()

	Manually start playback of the emitter's sound. If this is called on the server-side object, the play command will be related to all client-side ghosts.

.. cpp:function:: void SFXEmitter::stop()

	Manually stop playback of the emitter's sound. If this is called on the server-side object, the stop command will be related to all client-side ghosts.

Fields
------

.. cpp:member:: int  SFXEmitter::coneInsideAngle

	Angle of inner volume cone of 3D sound in degrees.

.. cpp:member:: int  SFXEmitter::coneOutsideAngle

	Angle of outer volume cone of 3D sound in degrees.

.. cpp:member:: float  SFXEmitter::coneOutsideVolume

	Volume scale factor of outside of outer volume 3D sound cone.

.. cpp:member:: float  SFXEmitter::fadeInTime

	Number of seconds to gradually fade in volume from zero when playback starts.

.. cpp:member:: float  SFXEmitter::fadeOutTime

	Number of seconds to gradually fade out volume down to zero when playback is stopped or paused.

.. cpp:member:: filename  SFXEmitter::fileName

	The sound file to play. Use either this property or track . If both are assigned, track takes precendence. The primary purpose of this field is to avoid the need for the user to define SFXTrack datablocks for all sounds used in a level.

.. cpp:member:: bool  SFXEmitter::is3D

	Whether to play fileName as a positional (3D) sound or not. If a track is assigned, the value of this field is ignored.

.. cpp:member:: bool  SFXEmitter::isLooping

	Whether to play fileName in an infinite loop. If a track is assigned, the value of this field is ignored.

.. cpp:member:: bool  SFXEmitter::isStreaming

	Whether to use streamed playback for fileName . If a track is assigned, the value of this field is ignored. Streaming vs. Buffered Audio

.. cpp:member:: float  SFXEmitter::maxDistance

	Distance at which to stop volume attenuation of the 3D sound.

.. cpp:member:: float  SFXEmitter::pitch

	Pitch shift to apply to the sound. Default is 1 = play at normal speed.

.. cpp:member:: bool  SFXEmitter::playOnAdd

	Whether playback of the emitter's sound should start as soon as the emitter object is added to the level. If this is true, the emitter will immediately start to play when the level is loaded.

.. cpp:member:: float  SFXEmitter::referenceDistance

	Distance at which to start volume attenuation of the 3D sound.

.. cpp:member:: Point3F  SFXEmitter::scatterDistance

	Bounds on random offset to apply to initial 3D sound position.

.. cpp:member:: SFXSource SFXEmitter::sourceGroup

	The SFXSource to which to assign the sound of this emitter as a child.

.. cpp:member:: SFXTrack SFXEmitter::track

	The track which the emitter should play.

.. cpp:member:: bool  SFXEmitter::useTrackDescriptionOnly

	If this is true, all fields except for playOnAdd and track are ignored on the emitter object. This is useful to prevent fields in the track 's description from being overridden by emitter fields.

.. cpp:member:: float  SFXEmitter::volume

	Volume level to apply to the sound.
