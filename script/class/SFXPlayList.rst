SFXPlayList
===========

A datablock describing a playback pattern of sounds.

Inherit:
	:doc:`SFXTrack`

Description
-----------

Playlists allow to define intricate playback patterns of invidual tracks and thus allow the sound system to be easily used for playing multiple sounds in single operations.

As playlists are SFXTracks, they can thus be used anywhere in the engine where sound data can be assigned.

Each playlist can hold a maximum of 16 tracks. Longer playlists may be constructed by cascading lists, i.e. by creating a playlist that references other playlists.

Processing of a single playlist slot progresses in a fixed set of steps that are invariably iterated through for each slot (except the slot is assigned a state and its state is deactivated; in this case, the controller will exit out of the slot directly):

#. delayIn: Waits a set amount of time before processing the slot. This is 0 by default and is determined by the delayTimeIn (seconds to wait) and delayTimeInVariance (bounds on randomization) properties.
#. transitionIn: Decides what to do before playing the slot. Defaults to None which makes this stage a no-operation. Alternatively, the slot can be configured to wait for playback of other slots to finish (Wait and WaitAll) or to stop playback of other slots (Stop and StopAll). Note that Wait and Stop always refer to the source that was last started by the list.
#. play: Finally, the track attached to the slot is played. However, this will only start playback of the track and then immediately move on to the next stage. It will not wait for the track to finish playing. Note also that depending on the replay setting for the slot, this stage may pick up a source that is already playing on the slot rather than starting a new one. Several slot properties (fade times, min/max distance, and volume/pitch scale) are used in this stage.
#. delayOut: Waits a set amount of time before transitioning out of the slot. This works the same as delayIn and is set to 0 by default (i.e. no delay).
#. transitionOut: Decides what to do after playing the slot. This works like transitionIn.

This is a key difference to playlists in normal music players where upon reaching a certain slot, the slot will immediately play and the player then wait for playback to finish before moving on to the next slot.

.. note::

	Be aware that time limits set on slot delays are soft limits. The sound system updates sound sources in discrete (and equally system update frequency dependent) intervals which thus determines the granularity at which time-outs can be handled.

Value Randomization
~~~~~~~~~~~~~~~~~~~

For greater variety, many of the values for individual slots may be given a randomization limit that will trigger a dynamic variance of the specified base value.

Any given field xyz that may be randomized has a corresponding field xyzVariance which is a two-dimensional vector. The first number specifies the greatest value that may be subtracted from the given base value (i.e. the xyz field) whereas the second number specifies the greatest value that may be added to the base value. Between these two limits, a random number is generated.

The default variance settings of "0 0" will thus not allow to add or subtract anything from the base value and effectively disable randomization.

Randomization is re-evaluated on each cycle through a list.

Playlists and States
~~~~~~~~~~~~~~~~~~~~

A unique aspect of playlists is that they allow their playback to be tied to the changing set of active sound states. This feature enables playlists to basically connect to an extensible state machine that can be leveraged by the game code to signal a multitude of different gameplay states with the audio system then automatically reacting to state transitions.

Playlists react to states in three ways:

* Before a controller starts processing a slot it checks whether the slot is assigned a state. If this is the case, the controller checks whether the particular state is active. If it is not, the entire slot is skipped. If it is, the controller goes on to process the slot.
* If a controller is in one of the delay stages for a slot that has a state assigned and the state is deactivated, the controller will stop the delay and skip any of the remaining processing stages for the slot.
* Once the play stage has been processed for a slot that has a state assigned, the slot's stateMode will determine what happens with the playing sound source if the slot's state is deactivated while the sound is still playing.

A simple example of how to make use of states in combination with playlists would be to set up a playlist for background music that reacts to the mood of the current gameplay situation. For example, during combat, tenser music could play than during normal exploration. To set this up, different SFXStates would represent different moods in the game and the background music playlist would have one slot set up for each such mood. By making use of volume fades and the PauseWhenDeactivatedstateMode, smooth transitions between the various audio tracks can be produced.

Example::

	// Create a play list from two SFXProfiles.
	%playList = newSFXPlayList()
	{
	   // Use a looped description so the list playback will loop.description = AudioMusicLoop2D;
	
	   track[ 0 ] = Profile1;
	   track[ 1 ] = Profile2;
	};
	
	// Play the list.sfxPlayOnce( %playList );

Fields
------

.. cpp:member:: float  SFXPlayList::delayTimeIn [16]

	Seconds to wait after moving into slot before transitionIn .

.. cpp:member:: Point2F  SFXPlayList::delayTimeInVariance [16]

	Bounds on randomization of delayTimeIn . Value Randomization

.. cpp:member:: float  SFXPlayList::delayTimeOut [16]

	Seconds to wait before moving out of slot after transitionOut .

.. cpp:member:: Point2F  SFXPlayList::delayTimeOutVariance [16]

	Bounds on randomization of delayTimeOut . Value Randomization

.. cpp:member:: float  SFXPlayList::fadeTimeIn [16]

	Seconds to fade sound in (-1 to use the track's own fadeInTime.).

.. cpp:member:: Point2F  SFXPlayList::fadeTimeInVariance [16]

	Bounds on randomization of fadeInTime. Value Randomization

.. cpp:member:: float  SFXPlayList::fadeTimeOut [16]

	Seconds to fade sound out (-1 to use the track's own fadeOutTime.).

.. cpp:member:: Point2F  SFXPlayList::fadeTimeOutVariance [16]

	Bounds on randomization of fadeOutTime. Value Randomization

.. cpp:member:: SFXPlayListLoopMode SFXPlayList::loopMode

	Behavior when description has looping enabled. The loop mode determines whether the list will loop over a single slot or loop over all the entire list of slots being played.

.. cpp:member:: float  SFXPlayList::maxDistance [16]

	maxDistance to apply to 3D sounds in this slot ( lt 1 to use maxDistance of track's own description).

.. cpp:member:: Point2F  SFXPlayList::maxDistanceVariance [16]

	Bounds on randomization of maxDistance . Value Randomization

.. cpp:member:: int  SFXPlayList::numSlotsToPlay

	Number of slots to play. Up to a maximum of 16, this field determines the number of slots that are taken from the list for playback. Only slots that have a valid track assigned will be considered for this.

.. cpp:member:: float  SFXPlayList::pitchScale [16]

	Scale factor to apply to pitch of sounds played on this list slot. This value will scale the actual pitch set on the track assigned to the slot, i.e. a value of 0.5 will cause the track to play at half its assigned speed.

.. cpp:member:: Point2F  SFXPlayList::pitchScaleVariance [16]

	Bounds on randomization of pitchScale . Value Randomization

.. cpp:member:: SFXPlayListRandomMode SFXPlayList::random

	Slot playback order randomization pattern. By setting this field to something other than "NotRandom" to order in which slots of the playlist are processed can be changed from sequential to a random pattern. This allows to to create more varied playback patterns. Defaults to "NotRandom".

.. cpp:member:: float  SFXPlayList::referenceDistance [16]

	referenceDistance to set for 3D sounds in this slot ( lt 1 to use referenceDistance of track's own description).

.. cpp:member:: Point2F  SFXPlayList::referenceDistanceVariance [16]

	Bounds on randomization of referenceDistance . Value Randomization

.. cpp:member:: int  SFXPlayList::repeatCount [16]

	Number of times to loop this slot.

.. cpp:member:: SFXPlayListReplayMode SFXPlayList::replay [16]

	Behavior when an already playing sound is encountered on this slot from a previous cycle. Each slot can have an arbitrary number of sounds playing on it from previous cycles. This field determines how SFXController will handle these sources.

.. cpp:member:: SFXState SFXPlayList::state [16]

	State that must be active for this slot to play. Playlists and States

.. cpp:member:: SFXPlayListStateMode SFXPlayList::stateMode [16]

	Behavior when assigned state is deactivated while slot is playing. Playlists and States

.. cpp:member:: bool  SFXPlayList::trace

	Enable/disable execution tracing for this playlist (local only). If this is true, SFXControllers attached to the list will automatically run in trace mode.

.. cpp:member:: SFXTrack SFXPlayList::track [16]

	Track to play in this slot. This must be set for the slot to be considered for playback. Other settings for a slot will not take effect except this field is set.

.. cpp:member:: SFXPlayListTransitionMode SFXPlayList::transitionIn [16]

	Behavior when moving into this slot. After the delayIn time has expired (if any), this slot determines what the controller will do before actually playing the slot.

.. cpp:member:: SFXPlayListTransitionMode SFXPlayList::transitionOut [16]

	Behavior when moving out of this slot. After the detailTimeOut has expired (if any), this slot determines what the controller will do before moving on to the next slot.

.. cpp:member:: float  SFXPlayList::volumeScale [16]

	Scale factor to apply to volume of sounds played on this list slot. This value will scale the actual volume level set on the track assigned to the slot, i.e. a value of 0.5 will cause the track to play at half-volume.

.. cpp:member:: Point2F  SFXPlayList::volumeScaleVariance [16]

	Bounds on randomization of volumeScale . Value Randomization
