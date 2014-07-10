SFXProfile
==========

Encapsulates a single sound file for playback by the sound system.

Inherit:
	:doc:`SFXTrack`

Description
-----------

SFXProfile combines a sound description (SFXDescription) with a sound file such that it can be played by the sound system. To be able to play a sound file, the sound system will always require a profile for it to be created. However, several of the SFX functions (sfxPlayOnce(), sfxCreateSource()) perform this creation internally for convenience using temporary profile objects.

Sound files can be in either OGG or WAV format. However, extended format support is available when using FMOD. See Supported Sound File Formats.

Profile Loading
~~~~~~~~~~~~~~~

By default, the sound data referenced by a profile will be loaded when the profile is first played and the data then kept until either the profile is deleted or until the sound device on which the sound data is held is deleted.

This initial loading my incur a small delay when the sound is first played. To avoid this, a profile may be expicitly set to load its sound data immediately when the profile is added to the system. This is done by setting the preload property to true.

Example::

	datablock SFXProfile( Shore01Snd )
	{
	   fileName     = "art/sound/Lakeshore_mono_01";
	   description  = Shore01Looping3d;
	   preload      = true;
	};

Methods
-------

.. cpp:function:: float SFXProfile::getSoundDuration()

	Return the length of the sound data in seconds.

	:return: The length of the sound data in seconds or 0 if the sound referenced by the profile could not be found. 

Fields
------

.. cpp:member:: filename  SFXProfile::fileName

	Path to the sound file. If the extension is left out, it will be inferred by the sound system. This allows to easily switch the sound format without having to go through the profiles and change the filenames there, too.

.. cpp:member:: bool  SFXProfile::preload

	Whether to preload sound data when the profile is added to system. Profile Loading
