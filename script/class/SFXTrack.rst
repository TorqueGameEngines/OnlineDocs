SFXTrack
========

Abstract base class for sound data that can be played back by the sound system.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

The term "track" is used in the sound system to refer to any entity that can be played back as a sound source. These can be individual files (SFXProfile), patterns of other tracks (SFXPlayList), or special sound data defined by a device layer (SFXFMODEvent).

Any track must be paired with a SFXDescription that tells the sound system how to set up playback for the track.

All objects that are of type SFXTrack will automatically be added to SFXTrackSet.

Fields
------

.. cpp:member:: SFXDescription SFXTrack::description

	Playback setup description for this track. If unassigned, the description named "AudioEffects" will automatically be assigned to the track. If this description is not defined, track creation will fail.

.. cpp:member:: string  SFXTrack::parameters [8]

	Parameters to automatically attach to SFXSources created from this track. Individual parameters are identified by their internalName .
