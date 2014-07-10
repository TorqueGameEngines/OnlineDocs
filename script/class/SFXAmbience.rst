SFXAmbience
===========

A datablock that describes an ambient sound space.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Each ambience datablock captures the properties of a unique ambient sound space. A sound space is comprised of:

* an ambient audio track that is played when the listener is inside the space,
* a reverb environment that is active inside the space, and
* a number of SFXStates that are activated when entering the space and deactivated when exiting it.

Each of these properties is optional.

An important characteristic of ambient audio spaces is that their unique nature is not determined by their location in space but rather by their SFXAmbience datablock. This means that the same SFXAmbience datablock assigned to multiple locations in a level represents the same unique audio space to the sound system.

This is an important distinction for the ambient sound mixer which will activate a given ambient audio space only once at any one time regardless of how many intersecting audio spaces with the same SFXAmbience datablock assigned the listener may currently be in.

All SFXAmbience instances are automatically added to the global SFXAmbienceSet.

At the moment, transitions between reverb environments are not blended and different reverb environments from multiple active SFXAmbiences will not be blended together. This will be added in a future version.

Example::

	singleton SFXAmbience( Underwater )
	{
	   environment = AudioEnvUnderwater;
	   soundTrack = ScubaSoundList;
	   states[ 0 ] = AudioLocationUnderwater;
	};

Fields
------

.. cpp:member:: float  SFXAmbience::dopplerFactor

	The factor to apply to the doppler affect in this space. Defaults to 0.5. Doppler Effect

.. cpp:member:: SFXEnvironment SFXAmbience::environment

	Reverb environment active in the ambience zone. Audio Reverb

.. cpp:member:: float  SFXAmbience::rolloffFactor

	The rolloff factor to apply to distance-based volume attenuation in this space. Defaults to 1.0. Volume Attenuation

.. cpp:member:: SFXTrack SFXAmbience::soundTrack

	Sound track to play in the ambience zone.

.. cpp:member:: SFXState SFXAmbience::states [4]

	States to activate when the ambient zone is entered. When the ambient sound state is entered, all states associated with the state will be activated (given that they are not disabled) and deactivated when the space is exited again.
