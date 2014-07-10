Sound
=====

A broad range of functionality for creating rich game audio. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/SFXAmbience
	class/SFXController
	class/SFXDescription
	class/SFXEmitter
	class/SFXEnvironment
	class/SFXParameter
	class/SFXPlayList
	class/SFXProfile
	class/SFXSound
	class/SFXSource
	class/SFXSpace
	class/SFXState
	class/SFXTrack

Enumeration
-----------

.. cpp:type:: enum  SFXChannel

	Channels are individual properties of sound sources that may be animated over time.

	:param Volume: Channel controls volume level of attached sound sources. See also:SFXDescription::volume
	:param Pitch: Channel controls pitch of attached sound sources. See also:SFXDescription::pitch
	:param Priority: Channel controls virtualizaton priority level of attached sound sources. See also:SFXDescription::priority
	:param PositionX: Channel controls X coordinate of 3D sound position of attached sources.
	:param PositionY: Channel controls Y coordinate of 3D sound position of attached sources.
	:param PositionZ: Channel controls Z coordinate of 3D sound position of attached sources.
	:param RotationX: Channel controls X rotation (in degrees) of 3D sound orientation of attached sources.
	:param RotationY: Channel controls Y rotation (in degrees) of 3D sound orientation of attached sources.
	:param RotationZ: Channel controls Z rotation (in degrees) of 3D sound orientation of attached sources.
	:param VelocityX: Channel controls X coordinate of 3D sound velocity vector of attached sources.
	:param VelocityY: Channel controls Y coordinate of 3D sound velocity vector of attached sources.
	:param VelocityZ: Channel controls Z coordinate of 3D sound velocity vector of attached sources.
	:param ReferenceDistance: Channel controls reference distance of 3D sound of attached sources. See also:SFXDescription::referenceDistance
	:param MaxDistance: Channel controls max volume attenuation distance of 3D sound of attached sources. See also:SFXDescription::maxDistance
	:param ConeInsideAngle: Channel controls angle (in degrees) of 3D sound inner volume cone of attached sources. See also:SFXDescription::coneInsideAngle
	:param ConeOutsideAngle: Channel controls angle (in degrees) of 3D sound outer volume cone of attached sources. See also:SFXDescription::coneOutsideAngle
	:param ConeOutsideVolume: Channel controls volume outside of 3D sound outer cone of attached sources. See also:SFXDescription::coneOutsideVolume
	:param Cursor: Channel controls playback cursor of attached sound sources. Note:Be aware that different types of sound sources interpret play cursor positions differently or do not actually have play cursors (these sources will ignore the channel).
	:param Status: Channel controls playback status of attached sound sources. The channel's value is rounded down to the nearest integer and interpreted in the following way:1: Play2: Stop3: Pause
	:param User0: Channel available for custom use. By default ignored by sources. Note:For FMOD Designer event sources (SFXFMODEventSource), this channel is used for event parameters defined in FMOD Designer and should not be used otherwise.See also:SFXSource::onParameterValueChange
	:param User1: Channel available for custom use. By default ignored by sources. See also:SFXSource::onParameterValueChange
	:param User2: Channel available for custom use. By default ignored by sources. See also:SFXSource::onParameterValueChange
	:param User3: Channel available for custom use. By default ignored by sources. See also:SFXSource::onParameterValueChange

.. cpp:type:: enum  SFXDistanceModel

	Type of volume distance attenuation curve. The distance model determines the falloff curve applied to the volume of 3D sounds over distance. 

	:param Linear: Volume attenuates linearly from the references distance onwards to max distance where it reaches zero.
	:param Logarithmic: Volume attenuates logarithmically starting from the reference distance and halving every reference distance step from there on. Attenuation stops at max distance but volume won't reach zero.

.. cpp:type:: enum  SFXPlayListLoopMode

	Playlist behavior when description is set to loop.

	:param All: Loop over all slots, i.e. jump from last to first slot after all slots have played.
	:param Single: Loop infinitely over the current slot. Only useful in combination with either states or manual playlist control.

.. cpp:type:: enum  SFXPlayListRandomMode

	Randomization pattern to apply to playlist slot playback order.

	:param NotRandom: Play slots in sequential order. No randomization.
	:param StrictRandom: Play a strictly random selection of slots. In this mode, a set of numSlotsToPlay random numbers between 0 and numSlotsToPlay-1 (inclusive), i.e. in the range of valid slot indices, is generated and playlist slots are played back in the order of this list. This allows the same slot to occur multiple times in a list and, consequentially, allows for other slots to not appear at all in a given slot ordering.
	:param OrderedRandom: Play all slots in the list in a random order. In this mode, the numSlotsToPlay slots from the list with valid tracks assigned are put into a random order and played. This guarantees that each slots is played exactly once albeit at a random position in the total ordering.

.. cpp:type:: enum  SFXPlayListReplayMode

	Behavior when hitting the play stage of a slot that is still playing from a previous cycle.

	:param IgnorePlaying: Ignore any sources that may already be playing on the slot and just create a new source.
	:param RestartPlaying: Restart all sources that was last created for the slot.
	:param KeepPlaying: Keep playing the current source(s) as if the source started last on the slot was created in this cycle. For this, the sources associated with the slot are brought to the top of the play stack.
	:param StartNew: Stop all sources currently playing on the slot and then create a new source.
	:param SkipIfPlaying: If there are sources already playing on the slot, skip the play stage.

.. cpp:type:: enum  SFXPlayListStateMode

	Reaction behavior when a state is changed incompatibly on a slot that has already started playing.

	:param StopWhenDeactivated: Stop the sources playing on the slot when a state changes to a setting that is incompatible with the slot's state setting.
	:param PauseWhenDeactivated: Pause all sources playing on the slot when a state changes to a setting that is incompatible with the slot's state setting. When the slot's state is reactivated again, the sources will resume playback.
	:param IgnoreWhenDeactivated: Ignore when a state changes to a setting incompatible with the slot's state setting and just keep playing sources attached to the slot.

.. cpp:type:: enum  SFXPlayListTransitionMode

	Playlist behavior when transitioning in and out of invididual slots. Transition behaviors apply when the playback controller starts processing a playlist slot and when it ends processing a slot. Using transition behaviors, playback can be synchronized.

	:param None: No transition. Immediately move on to processing the slot or immediately move on to the next slot.
	:param Wait: Wait for the sound source spawned last by this playlist to finish playing. Then proceed.
	:param WaitAll: Wait for all sound sources currently spawned by the playlist to finish playing. Then proceed.
	:param Stop: Stop the sound source spawned last by this playlist. Then proceed.
	:param StopAll: Stop all sound sources spawned by the playlist. Then proceed.

.. cpp:type:: enum  SFXStatus

	Playback status of sound source.

	:param Playing: The source is currently playing.
	:param Stopped: Playback of the source is stopped. When transitioning to Playing state, playback will start at the beginning of the source.
	:param Paused: Playback of the source is paused. Resuming playback will play from the current playback position.

Functions
---------

.. cpp:function:: bool sfxCreateDevice(string provider, string device, bool useHardware, int maxBuffers)

	Try to create a new sound device using the given properties. If a sound device is currently initialized, it will be uninitialized first. However, be aware that in this case, if this function fails, it will not restore the previously active device but rather leave the sound system in an uninitialized state. Sounds that are already playing while the new device is created will be temporarily transitioned to virtualized playback and then resume normal playback once the device has been created. In the core scripts, sound is automatically set up during startup in the sfxStartup() function. Providers and Devices

	:param provider: The name of the device provider as returned by sfxGetAvailableDevices().
	:param device: The name of the device as returned by sfxGetAvailableDevices().
	:param useHardware: Whether to enabled hardware mixing on the device or not. Only relevant if supported by the given device.
	:param maxBuffers: The maximum number of concurrent voices for this device to use or -1 for the device to pick its own reasonable default.

	:return: True if the initialization was successful, false if not. 

.. cpp:function:: SFXSource  sfxCreateSource(SFXTrack track)

	Create a new source that plays the given track. The source will be returned in stopped state. Call SFXSource::play() to start playback. In contrast to play-once sources, the source object will not be automatically deleted once playback stops. Call delete() to release the source object. This function will automatically create the right SFXSource type for the given SFXTrack .

	:param track: The track the source should play.

	:return:  for playback of the given track or 0 if no source could be created from the given track.

	Example::

		// Create and play a source from a pre-existing profile:
		%source = sfxCreateSource( SoundFileProfile );
		%source.play();

.. cpp:function:: SFXSource  sfxCreateSource(SFXTrack track, float x, float y, float z)

	Create a new source that plays the given track and position its 3D sounds source at the given coordinates (if it is a 3D sound). The source will be returned in stopped state. Call SFXSource::play() to start playback. In contrast to play-once sources, the source object will not be automatically deleted once playback stops. Call delete() to release the source object. This function will automatically create the right SFXSource type for the given SFXTrack .

	:param track: The track the source should play.
	:param x: The X coordinate of the 3D sound position.
	:param y: The Y coordinate of the 3D sound position.
	:param z: The Z coordinate of the 3D sound position.

	:return:  for playback of the given track or 0 if no source could be created from the given track.

	Example::

		// Create and play a source from a pre-existing profile and position it at (100, 200, 300):
		%source = sfxCreateSource( SoundFileProfile, 100, 200, 300 );
		%source.play();

.. cpp:function:: SFXSound  sfxCreateSource(SFXDescription description, string filename)

	Create a temporary SFXProfile from the given description and filename and then create and return a new source that plays the profile. The source will be returned in stopped state. Call SFXSource::play() to start playback. In contrast to play-once sources, the source object will not be automatically deleted once playback stops. Call delete() to release the source object.

	:param description: The description to use for setting up the temporary SFXProfile.
	:param filename: Path to the sound file to play.

	:return:  for playback of the given track or 0 if no source or no temporary profile could be created.

	Example::

		// Create a source for a music track:
		%source = sfxCreateSource( AudioMusicLoop2D, "art/sound/backgroundMusic" );
		%source.play();

.. cpp:function:: SFXSound  sfxCreateSource(SFXDescription description, string filename, float x, float y, float z)

	Create a temporary SFXProfile from the given description and filename and then create and return a new source that plays the profile. Position the sound source at the given coordinates (if it is a 3D sound). The source will be returned in stopped state. Call SFXSource::play() to start playback. In contrast to play-once sources, the source object will not be automatically deleted once playback stops. Call delete() to release the source object.

	:param description: The description to use for setting up the temporary SFXProfile.
	:param filename: Path to the sound file to play.
	:param x: The X coordinate of the 3D sound position.
	:param y: The Y coordinate of the 3D sound position.
	:param z: The Z coordinate of the 3D sound position.

	:return:  for playback of the given track or 0 if no source or no temporary profile could be created.

	Example::

		// Create a source for a music track and position it at (100, 200, 300):
		%source = sfxCreateSource( AudioMusicLoop3D, "art/sound/backgroundMusic", 100, 200, 300 );
		%source.play();

.. cpp:function:: void sfxDeleteDevice()

	Delete the currently active sound device and release all its resources. SFXSources that are still playing will be transitioned to virtualized playback mode. When creating a new device, they will automatically transition back to normal playback. In the core scripts, this is done automatically for you during shutdown in the sfxShutdown() function. Providers and Devices

.. cpp:function:: void sfxDeleteWhenStopped(SFXSource source)

	Mark the given source for deletion as soon as it moves into stopped state. This function will retroactively turn the given source into a play-once source (see Play-Once Sources ).

	:param source: A sound source.

.. cpp:function:: void sfxDumpSources(bool includeGroups)

	Dump information about all current SFXSource instances to the console. The dump includes information about the playback status for each source, volume levels, virtualization, etc.

	:param includeGroups: If true, direct instances of SFXSources (which represent logical sound groups) will be included. Otherwise only instances of subclasses of SFXSources are included in the dump.

.. cpp:function:: string sfxDumpSourcesToString(bool includeGroups)

	Dump information about all current SFXSource instances to a string. The dump includes information about the playback status for each source, volume levels, virtualization, etc.

	:param includeGroups: If true, direct instances of SFXSources (which represent logical sound groups) will be included. Otherwise only instances of subclasses of SFXSources are included in the dump.

	:return: A string containing a dump of information about all currently instantiated SFXSources. 

.. cpp:function:: string sfxGetActiveStates()

	Return a newline-separated list of all active states.

	:return:  where each element is the name of an active state object.

	Example::

		// Disable all active states.
		foreach$( %state in sfxGetActiveStates() )
		   %state.disable();

.. cpp:function:: string sfxGetAvailableDevices()

	Get a list of all available sound devices. The return value will be a newline-separated list of entries where each line describes one available sound device. Each such line will have the following format:

	:return: A newline-separated list of information about all available sound devices. 

.. cpp:function:: string sfxGetDeviceInfo()

	Return information about the currently active sound device. The return value is a tab-delimited string of the following format:

	:return: A tab-separated list of properties of the currently active sound device or the empty string if no sound device has been initialized. 

.. cpp:function:: SFXDistanceModel  sfxGetDistanceModel()

	Get the falloff curve type currently being applied to 3D sounds. Volume Attenuation 3D Audio

	:return: The current distance model type.

.. cpp:function:: float sfxGetDopplerFactor()

	Get the current global doppler effect setting. Doppler Effect

	:return: =0).

.. cpp:function:: float sfxGetRolloffFactor()

	Get the current global scale factor applied to volume attenuation of 3D sounds in the logarithmic model. Volume Attenuation 3D Audio

	:return: The current scale factor for logarithmic 3D sound falloff curves.

.. cpp:function:: SFXSource  sfxPlay(SFXSource source)

	Start playback of the given source. This is the same as calling SFXSource::play() directly.

	:param source: The source to start playing.

	:return: .

	Example::

		// Create and play a source from a pre-existing profile:
		%source = sfxCreateSource( SoundFileProfile );
		%source.play();

.. cpp:function:: void sfxPlay(SFXTrack track)

	Create a new play-once source for the given track and start playback of the source. This is equivalent to calling sfxCreateSource() on  and SFXSource::play() on the resulting source. Play-Once Sources

	:param track: The sound datablock to play.

	:return: The newly created play-once source or 0 if the creation failed.

.. cpp:function:: void sfxPlay(SFXTrack track, float x, float y, float z)

	Create a new play-once source for the given track , position its 3D sound at the given coordinates (if the track's description is set up for 3D sound) and start playback of the source. This is equivalent to calling sfxCreateSource() on  and SFXSource::play() on the resulting source. Play-Once Sources

	:param track: The sound datablock to play.
	:param x: The X coordinate of the 3D sound position.
	:param y: The Y coordinate of the 3D sound position.
	:param z: The Z coordinate of the 3D sound position.

	:return: The newly created play-once source or 0 if the creation failed.

.. cpp:function:: SFXSource  sfxPlayOnce(SFXTrack track)

	Create a play-once source for the given track . Once playback has finished, the source will be automatically deleted in the next sound system update. Play-Once Sources

	:param track: The sound datablock.

	:return: A newly created temporary source in "Playing" state or 0 if the operation failed.

.. cpp:function:: SFXSource  sfxPlayOnce(SFXTrack track, float x, float y, float z, float fadeInTime)

	Create a play-once source for the given given track and position the source's 3D sound at the given coordinates only if the track's description is set up for 3D sound). Once playback has finished, the source will be automatically deleted in the next sound system update. Play-Once Sources

	:param track: The sound datablock.
	:param x: The X coordinate of the 3D sound position.
	:param y: The Y coordinate of the 3D sound position.
	:param z: The Z coordinate of the 3D sound position.
	:param fadeInTime: If >=0, this overrides the SFXDescription::fadeInTime value on the track's description.

	:return: A newly created temporary source in "Playing" state or 0 if the operation failed.

	Example::

		// Immediately start playing the given track.  Fade it in to full volume over 5 seconds.
		sfxPlayOnce( MusicTrack, 0, 0, 0, 5.f );

.. cpp:function:: SFXSource  sfxPlayOnce(SFXDescription description, string filename)

	Create a new temporary SFXProfile from the given description and filename , then create a play-once source for it and start playback. Once playback has finished, the source will be automatically deleted in the next sound system update. If not referenced otherwise by then, the temporary SFXProfile will also be deleted. Play-Once Sources

	:param description: The description to use for playback.
	:param filename: Path to the sound file to play.

	:return: A newly created temporary source in "Playing" state or 0 if the operation failed.

	Example::

		// Play a sound effect file once.
		sfxPlayOnce( AudioEffects, "art/sound/weapons/Weapon_pickup" );

.. cpp:function:: SFXSource  sfxPlayOnce(SFXDescription description, string filename, float x, float y, float z, float fadeInTime)

	Create a new temporary SFXProfile from the given description and filename , then create a play-once source for it and start playback. Position the source's 3D sound at the given coordinates (only if the description is set up for 3D sound). Once playback has finished, the source will be automatically deleted in the next sound system update. If not referenced otherwise by then, the temporary SFXProfile will also be deleted. Play-Once Sources

	:param description: The description to use for playback.
	:param filename: Path to the sound file to play.
	:param x: The X coordinate of the 3D sound position.
	:param y: The Y coordinate of the 3D sound position.
	:param z: The Z coordinate of the 3D sound position.
	:param fadeInTime: If >=0, this overrides the SFXDescription::fadeInTime value on the track's description.

	:return: A newly created temporary source in "Playing" state or 0 if the operation failed.

	Example::

		// Play a sound effect file once using a 3D sound with a default falloff placed at the origin.
		sfxPlayOnce( AudioDefault3D, "art/sound/weapons/Weapon_pickup", 0, 0, 0 );

.. cpp:function:: void sfxSetDistanceModel(SFXDistanceModel model)

	Set the falloff curve type to use for distance-based volume attenuation of 3D sounds.

	:param model: The distance model to use for 3D sound.

.. cpp:function:: void sfxSetDopplerFactor(float value)

	Set the global doppler effect scale factor. Doppler Effect

	:param value: The new doppler shift scale factor.

.. cpp:function:: void sfxSetRolloffFactor(float value)

	Set the global scale factor to apply to volume attenuation of 3D sounds in the logarithmic model. Volume Attenuation 3D Audio

	:param value: The new scale factor for logarithmic 3D sound falloff curves.

.. cpp:function:: void sfxStop(SFXSource source)

	Stop playback of the given source . This is equivalent to calling SFXSource::stop() .

	:param source: The source to put into stopped state.

.. cpp:function:: void sfxStopAndDelete(SFXSource source)

	Stop playback of the given source (if it is not already stopped) and delete the source . The advantage of this function over directly calling delete() is that it will correctly handle volume fades that may be configured on the source. Whereas calling delete() would immediately stop playback and delete the source, this functionality will wait for the fade-out to play and only then stop the source and delete it. Volume Fades

	:param source: A sound source.

Variables
---------

.. cpp:member:: int $SFX::ambientUpdateTime

	Milliseconds spent on the last ambient audio update. Sound System Updates Ambient Audio

.. cpp:member:: int $SFX::DEVICE_CAPS_DSPEFFECTS

	Sound device capability flag indicating that the sound device supports adding DSP effect chains to sounds.

.. cpp:member:: int $SFX::DEVICE_CAPS_FMODDESIGNER

	Sound device capability flag indicating that the sound device supports FMOD Designer audio projects. FMOD Designer Audio

.. cpp:member:: int $SFX::DEVICE_CAPS_MULTILISTENER

	Sound device capability flag indicating that the sound device supports multiple concurrent listeners.

.. cpp:member:: int $SFX::DEVICE_CAPS_OCCLUSION

	Sound device capability flag indicating that the sound device implements sound occlusion.

.. cpp:member:: int $SFX::DEVICE_CAPS_REVERB

	Sound device capability flag indicating that the sound device supports reverb. Audio Reverb

.. cpp:member:: int $SFX::DEVICE_CAPS_VOICEMANAGEMENT

	Sound device capability flag indicating that the sound device implements its own voice virtualization. For these devices, the sound system will deactivate its own voice management and leave voice virtualization entirely to the device. Sounds and Voices

.. cpp:member:: int $SFX::DEVICE_INFO_CAPS

	Index of device capability flags in device info string.

.. cpp:member:: int $SFX::DEVICE_INFO_MAXBUFFERS

	Index of buffer limit number in device info string.

.. cpp:member:: int $SFX::DEVICE_INFO_NAME

	Index of device name field in device info string.

.. cpp:member:: int $SFX::DEVICE_INFO_PROVIDER

	Index of sound provider field in device info string.

.. cpp:member:: int $SFX::DEVICE_INFO_USEHARDWARE

	Index of use hardware flag in device info string.

.. cpp:member:: int $SFX::numCulled

	Number of SFXSounds that are currently in virtualized playback mode. Sounds and Voices

.. cpp:member:: int $SFX::numPlaying

	Number of SFXSources that are currently in playing state.

.. cpp:member:: int $SFX::numSounds

	Number of SFXSound type objects (i.e. actual single-file sounds) that are currently instantiated.

.. cpp:member:: int $SFX::numSources

	Number of SFXSource type objects that are currently instantiated.

.. cpp:member:: int $SFX::numVoices

	Number of voices that are currently allocated on the sound device.

.. cpp:member:: int $SFX::parameterUpdateTime

	Milliseconds spent on the last SFXParameter update loop. Sound System Updates Interactive Audio

.. cpp:member:: ColorI  SFXEmitter::renderColorInnerCone  [static, inherited]

	The color with which to render dots in the inner sound cone (Editor only).

.. cpp:member:: ColorI  SFXEmitter::renderColorOuterCone  [static, inherited]

	The color with which to render dots in the outer sound cone (Editor only).

.. cpp:member:: ColorI  SFXEmitter::renderColorOutsideVolume  [static, inherited]

	The color with which to render dots outside of the outer sound cone (Editor only).

.. cpp:member:: ColorI  SFXEmitter::renderColorPlayingInRange  [static, inherited]

	The color with which to render a sound emitter's marker cube in the editor when the emitter's sound is playing and in range of the listener.

.. cpp:member:: ColorI  SFXEmitter::renderColorPlayingOutOfRange  [static, inherited]

	The color with which to render a sound emitter's marker cube in the editor when the emitter's sound is playing but out of the range of the listener.

.. cpp:member:: ColorI  SFXEmitter::renderColorRangeSphere  [static, inherited]

	The color of the range sphere with which to render sound emitters in the editor.

.. cpp:member:: ColorI  SFXEmitter::renderColorStoppedInRange  [static, inherited]

	The color with which to render a sound emitter's marker cube in the editor when the emitter's sound is not playing but the emitter is in range of the listener.

.. cpp:member:: ColorI  SFXEmitter::renderColorStoppedOutOfRange  [static, inherited]

	The color with which to render a sound emitter's marker cube in the editor when the emitter's sound is not playing and the emitter is out of range of the listener.

.. cpp:member:: bool  SFXEmitter::renderEmitters  [static, inherited]

	Whether to render enhanced range feedback in the editor on all emitters regardless of selection state.

.. cpp:member:: float  SFXEmitter::renderPointDistance  [static, inherited]

	The distance between individual points in the sound emitter rendering in the editor as the points move from the emitter's center away to maxDistance.

.. cpp:member:: float  SFXEmitter::renderRadialIncrements  [static, inherited]

	The stepping (in degrees) for the radial sweep along the axis of the XY plane sweep for sound emitter rendering in the editor.

.. cpp:member:: float  SFXEmitter::renderSweepIncrements  [static, inherited]

	The stepping (in degrees) for the radial sweep on the XY plane for sound emitter rendering in the editor.

.. cpp:member:: int $SFX::sourceUpdateTime

	Milliseconds spent on the last SFXSource update loop. Sound System Updates


FMOD
----

Functionality specific to the FMOD SFX implementation. 

Classes
~~~~~~~

.. toctree::
	:maxdepth: 1

	class/SFXFMODEvent
	class/SFXFMODEventGroup
	class/SFXFMODEventSource
	class/SFXFMODProject

Description
~~~~~~~~~~~

When using FMOD for audio output in combination with Torque's sound system, an extended set of features is available to the user. This includes:

* Reverb support
* Enhanced voice virtualization
* Support for multiple listeners
* Enhanced sound format support: .aiff, .asf, .asx, .dls, .flac .fsb, .it, .m3u, .mid, .mod, .mp2, .mp3, .ogg, .pls, .s3m, .vag, .wav, .wax, .wma, .xm, .xma (on Xbox only)
* FMOD Designer enhanced audio design support

Functions
~~~~~~~~~

.. cpp:function:: void fmodDumpDSPInfo()

	Dump information about the standard DSP effects.

.. cpp:function:: void fmodDumpMemoryStats()

	:return: Prints the current memory consumption of the FMOD module 

Variables
~~~~~~~~~

.. cpp:member:: bool $pref::SFX::FMOD::disableSoftware

	Whether to disable the FMOD software mixer to conserve memory. All sounds not created with SFXDescription::useHardware or using DSP effects will fail to load.

.. cpp:member:: string $pref::SFX::FMOD::DSoundHRTF

	The type of HRTF to use for hardware-mixed 3D sounds when FMOD is using DirectSound for sound output and hardware-acceleration is not available. Options are 
	
	* "none": simple stereo panning/doppler/attenuation
	* "light": slightly higher quality than "none"
	* "full": full quality 3D playback

.. cpp:member:: bool $pref::SFX::FMOD::enableProfile

	Whether to enable support for FMOD's profiler. Using the FMOD Profiler with Torque

.. cpp:member:: int $SFX::Device::fmodCoreMem

	Current number of bytes allocated by the core FMOD sound system.

.. cpp:member:: int $SFX::Device::fmodEventMem

	Current number of bytes allocated by the FMOD Designer event system.

.. cpp:member:: int $SFX::Device::fmodNumEventSources

	The current number of SFXFMODEventSource instances in the system. This tells the number of sounds in the system that are currently playing FMOD Designer events.

.. cpp:member:: string $pref::SFX::FMOD::pluginPath

	Path to additional FMOD plugins.

.. cpp:member:: bool $pref::SFX::FMOD::useSoftwareHRTF

	Whether to enable HRTF in FMOD's software mixer. This will add a lowpass filter effect to the DSP effect chain of all sounds mixed in software.
