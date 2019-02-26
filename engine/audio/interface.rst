Interface
**********

Overview
==========
SFXSources are the interface to sound playback. They are created through the SFXSystem and control all aspects of playback. The SFX system can be interfaced through a number of console methods.

**Note:** *Do not create SFXSources directly through object declarations (i.e. new or singleton). This is inhibited by the SFX system.*

**SFXSources** are either created from SFXProfiles or directly from SFXStreams. The latter method is only available internally from within the engine and not exposed to script.

**SFXProfiles** are created by the user. They combine sound files with SFXDescriptions that describe how to play back the particular file.

**SFXDescriptions** are datablocks with a series of properties that describe aspects of sound playback.

**SFXSources** create SFXVoices (playback controllers) and SFXBuffers (sample data buffers) on SFXDevices. This happens internally.

**SFXStreams** are used to load sample data into SFXBuffers. For streaming buffers, this is a continuous process. This happens internally.

An **SFXListener** instance is coupled to the SFXSystem and defines the location and velocity of the listener in 3D space. This is used for volume attenuation of 3D sounds. This happens internally. The listener is automatically updated from the game's control object. 

Channels
==========
To allow volume level adjustment to a whole batch of sounds, sounds are grouped into logical volume channels. Music can thus be separated from sound effects or voices and have its volume adjusted independently.

Volume channels are numbered from 0 onwards. There is a maximum of 32 channels. The core scripts currently define and use three separate channels (defined in **core/scripts/client/audio.cs**):

* $GuiAudioType = 1;

	* Use for sounds relating to the interface.
	
* $SimAudioType = 2;

	* Use for in-game sound effect and environmental sounds.

* $MessageAudioType = 3;

	* Use for notifications (such as from chat) and possibly voices.

* $MusicAudioType = 4;

	* Use for background music.

**Note:** *The master volume set on the SFX system simultaneously scales all of the volume channels.*


A set of SFXDescriptions preset to this set of channels is made available through core/scripts/client/audio.cs. These should best be used as copy-sources for custom SFXDescriptions.

* AudioGui
* AudioSim
* AudioMessage
* AudioMusic


Descriptions
=============
Playback setups are described in SFXDescriptions. These are defined in **art/datablocks/audioProfiles.cs**. Some useful examples are below::

	*3D Sounds
	   o Single-Shot Sounds
	             + AudioDefault3D
	                # is3D = true
	                # referenceDistance = 20.0
	                # maxDistance = 100.0
	                # channel = $SimAudioType
	             + AudioClose3D
	                # is3D = true
	                # referenceDistance = 10.0
	                # maxDistance = 60.0
	                # channel = $SimAudioType
	             + AudioClosest3D
	                # is3D = true
	                # referenceDistance = 5.0
	                # maxDistance = 30.0
	                # channel = $SimAudioType
	   o Looping Sounds
	             + AudioDefaultLoop3D
	                # is3D = true
	                # isLooping = true
	                # referenceDistance = 20.0
	                # maxDistance = 100.0
	                # channel = $SimAudioType
	             + AudioCloseLoop3D
	                # is3D = true
	                # isLooping = true
	                # referenceDistance = 10.0
	                # maxDistance = 60.0
	                # channel = $SimAudioType
	             + AudioClosestLoop3D
	                # is3D = true
	                # isLooping = true
	                # referenceDistance = 5.0
	                # maxDistance = 30.0
	                # channel = $SimAudioType
	*2D Sounds
	   o Audio2D
	             + channel = $SimAudioType
	
	   o AudioStream2D
	             + isStreaming = true
	             + channel = $SimAudioType
	
	   o AudioLoop2D
	             + isLooping = true
	             + channel = $SimAudioType
	
	   o AudioStreamLoop2D
	             + isLooping = true
	             + isStreaming = true
	             + channel = $SimAudioType
	
	*Music
	   o AudioMusic2D
	             + isStreaming = true
	             + channel = $MusicAudioType
	
	   o AudioMusicLoop2D
	             + isStreaming = true
	             + isLooping = true
	             + channel = $MusicAudioType
	
	   o AudioMusic3D
	             + isStreaming = true
	             + is3D = true
	             + channel = $MusicAudioType
	
	   o AudioMusicLoop3D
	             + isStreaming = true
	             + isLooping = true
	             + is3D = true
	             + channel = $MusicAudioType


Configuring 3D Playback
=========================
There are multiple options available for configuring volume attenuation of 3D sounds on the device. The settings are exposed as script variables and must be set in script (either from the console or add them to **scripts/client/prefs.cs**). 

$pref::SFX::distanceModel
---------------------------
The distance model determines the rolloff function for 3D sounds, i.e. the way the volume attenuates as you move away from a 3D sound. The chosen model affects distance attenuation of all 3D sounds. Currently, there are two models available: 

**"linear"**

Starting from a sound's reference distance, the volume fades linearly towards its set maximum distance at which point it reaches zero.


**Notes:**

* Linear rolloff is not supported with DirectSound.
* Linear rolloff is unaffected by the rolloff factor set on the device.


**"logarithmic"**

Starting from a sound's reference distance, the volume halves every reference distance steps. This is the more realistic behavior for distance attenuation. In this model, the maximum distance only determines at which distance volume no longer decreases.


Instead, attenuation simply stops at the set maximum distance. Attenuation can be scaled by the rolloff factor to be faster or slower. 

$pref::SFX::dopplerFactor
---------------------------
The doppler shift to apply to 3D sounds based on the relative velocity to the listener. Higher values give more pronounced doppler effects. Default is 0.5. 

$pref::SFX::rolloffFactor
--------------------------
The rolloff factor scales the reference distance of a sound to determine how fast attenuation decreases a sound's volume. At 1.0, every reference distance steps will halve the volume of a sound. At 0.5, every reference distance steps will have the quarter of the previous step's volume.

**Note:** *The rolloff factor only affects logarithmic distance attenuation.*

Script Classes
===============

SFXDescription
----------------

Description
^^^^^^^^^^^^^

SFXDescriptions tell the sound system how to play back a sound, i.e. they provide the parameters when setting up playback for a sound on the device. 

Properties
^^^^^^^^^^^^

* **volume [float]:** Base volume level for the sound. This will be the starting point for volume attenuation on the sound. Must be between 0 (min) and 1 (max). Default is 1.

* **pitch [float]:** Pitch scale. This speeds up or slows down playback. Must be greater than 0. Default is 1.

* **isLooping [bool]:** If true, the sound will be played in an endless loop. Default is false.

* **isStreaming [bool]:** If true, the sound will be progressively streamed; if false, the sound will be buffered in whole. Default is false.

* **is3D [bool]:** If true, the sound is positional and mixed according to its spatial properties. Default is false.

* **referenceDistance [float]:** Distance at which volume attenuation begins. Up to this distance, the sound retains its base volume. Also, in the exponential distance model, the reference distance determine how fast the sound volume decreases with distance. Each referenceDistance steps (scaled by the rolloff factor), the volume halves. A rule of thumb is that for sounds that require you to be close to hear them in the real world, set the reference distance to small values whereas for sounds that are widely audible set it to larger values. Only for 3D sounds.

* **maxDistance [float]:** The distance at which attenuation stops. In the linear distance model, the attenuated volume will be zero at this distance. In the logarithmic model, attenuation will simply stop at this distance and the sound will keep its attenuated volume from there on out. Only for 3D sounds.

* **coneInsideAngle [float]:** Specifies the angle of the inside cone in degrees. Valid values are from 0 to 360. Must be less than coneOutsideAngle. Default is 360. Only for 3D sounds.

* **coneOutsideAngle [float]:** Specifies the angle of the outside cone in degrees. Valid values are from 0 to 360. Default is 360. Only for 3D sounds.

* **coneOutsideVolume [float]:** Determines the volume scale factor applied to a source's base volume level outside of the outer cone. In the outer cone, starting from outside the inner cone, the scale factor smoothly interpolates from 1.0 (within the inner cone) to this value. At the moment, the allowed range is 0.0 (silence) to 1.0 (no attenuation) as amplification is only supported on XAudio2 but not on the other devices. Only for 3D sound.

* **channel [int]:** Volume channel that the sound will get assigned to. The base volume level of the sound will be scaled by the channel's volume level. Default is 0.

* **fadeInTime [float]:** Number of seconds to gradually fade in volume from zero when playback starts.

* **fadeOutTime [float]:** Number of seconds to gradually fade out volume to zero before playback stops.

* **streamPacketSize [int]:** Number of seconds of sample data to read per streaming packet. Only for streamed sounds and only when SFX's own streaming system is used.

* **streamReadAhead [int]:** Number of stream packets to keep buffered ahead of time. A number of packets (usually three) will generally be kept immediately on the SFX device for playback. This number controls how many more packets are read ahead of time in addition to this. Higher numbers allow to better cope with lagging stream sources but for good resource consumption, this should be kept reasonably low. Only for streamed sounds and only when SFX's own streaming system is used.


SFXProfile
-----------

Description
^^^^^^^^^^^
An SFXProfile combines a sound file with an SFXDescription that tells how to play back the sound. SFXProfiles are datablocks, so when you define server-side SFXProfiles use the **datablock** keyword. For client-side only profiles, use **new** or **singleton**.

For non-streamed sounds, the SFXProfile will keep a reference to the SFXBuffer on the device once the sound has been loaded. This will allow simultaneous playbacks of the same profile to share a single SFXBuffer. A profile's sound will automatically reload when its file on disk changes. This will also update all sources that are currently using the profile.

By default, the sound data contained in an SFXProfile will be loaded into the SFX device when the sound is first played. This will incur a short delay on the first use. To load the sound data ahead of time independent on the first use, set the "preload" property to true. This will cause sound data to be loaded when the profile object is added to the system.

Once loaded, the sound data will remain loaded on the device until either the device is destroyed or the SFXProfile is deleted. Be aware that only non-streamed sounds may be preloaded. Streamed sounds always incur a certain loading delay. To ready a streamed sound for playback, attach and ready an SFXSource before playing the sound. 

Properties
^^^^^^^^^^

* **filename [string]:** The name of the file to load. It is usually best to omit extensions with sound filenames. This allows you to easily switch formats without having to change scripts. The SFX system will scan through its list of supported file formats (including extended formats supported by specific devices) to find the full filename.

* **description [object]:** The SFXDescription to use when playing back the sound.

* **preload [bool]:** If true, the sound file will be loaded into the SFX system as soon as the profile object gets added to Torque's object graph. This helps ensure that sounds are immediately ready for playback when the profile is used. Be aware, though, that this will also result in immediate resource consumption on the SFXDevice. Preloading will not cause disruptions in the loading process as sound loading happens in the background. Only non-streamed sounds can be preloaded. This flag is ignored for streamed sounds. To load a streamed sound into ready state before playing, create an SFXSource for it.

Methods
^^^^^^^
**float getSoundDuration():** Return the duration (in seconds) of the sound referenced by the profile. 

SFXSource
-----------

Description
^^^^^^^^^^^
Central controller for sound playback. SFXSources control the playback of a particular SFXProfile or SFXStream. SFXSources can only be created through sfxCreateSource or the various sfxPlay functions.

SFXSources are explicitly created by the user through SFX functions and are valid until they are deleted. However, to reduce bookkeeping required for single-shot sounds, the system keeps a list of so called "play-once sources." An SFXSource that is created as a play-once source will only be valid for as long as it is playing. When it has finished playing, it will be automatically deleted during the next SFX update.

Note that while permanent references to play-once sources should not be stored in script, a reference will not become invalid in-midst of script execution.

Markers are used for notifications that are triggered when playback crosses over a certain playback position. Each marker has a name and an associated playback position expressed in seconds. When playback crosses over the position, the "onMarkerPassed( %source, %markerName )" callback will be called on the source.

This is useful for synchronizing logic to music and sound effects. Currently, using setPosition() on a source will not prevent markers being jumped over from triggering. Instead, these markers will immediately trigger on the next source update. 

Properties
^^^^^^^^^^^
* **statusCallback [string]:** Name of function to call when the status of the SFXSource changes. Must take two parameters "( object %source, string %newStatus )". Default is empty which deactivates the callback. If this field is set, the source's onStatusChange callback will not trigger.

Callbacks
^^^^^^^^^^
These methods may be defined on SFXSources by the user and are called by the system on specific events.

* **onMarkerPassed( object this, string name ):** Called when a notification marker has been passed by the playback cursor. "name" is the name of the marker.
* **onStatusChange( object this, string newStatus ):** Called when the playback status of the source changes. Set getStatus() for the possible values for "newStatus"

Methods
^^^^^^^

* **bool isReady():** Returns true when the source has successfully loaded all its sound data and is ready for playback.
* **bool isPaused():** Returns true when the source is currently in paused state.
* **bool isPlaying():** Return true when the source is currently playing. Even though a given SFXSource is in playing state, it will not emit sound data on the device if it is in blocked state (awaiting data from its SFXStream) or is in virtualized playback mode.
* **bool isStopped():** Returns true when the source is currently stopped. Sources will start out in stopped state and will transition back into stopped state when they have finished playing.
* **string getStatus():** Return the current playback status of the source. Possible values are:

	* "playing": source is currently playing
	* "stopped": source is not playing
	* "paused": source has been paused

* **int getChannel():** Return the volume channel this SFXSource is assigned to.
* **float getDuration():** Return the total playback time of the SFXSource's associated sound in seconds.
* **setTransform( vector pos, [ vector direction ] ):** Set the 3D position and optionally the direction of the SFXSource.
* **setCone( float innerAngle, float outerAngle, foat outsideVolume ):** Set the 3D sound cone of the SFXSource.
* **setVolume( float volume ):** Set the (unattenuated) volume of the SFXSource. Must be between 0 (min) and 1 (max).
* **setPitch( float pitch ):** The frequency shift factor. A pitch of 1 plays back at the default frequency. A pitch of 0.5 of half the default frequency. The default frequency is the frequency of the source SFXStream.
* **float getPosition():** Returns the current position of the play cursor in seconds.
* **setPosition( float pos ):** Set the position of the play cursor in seconds.
* **play( [ float fadeInTime ] ):** Start or resume playback. If "fadeInTime" is given and is greater than 0, then the source will do a volume fade to its assigned volume in "fadeInTime" seconds. "fadeInTime" overrides a setting given in the SFXSource's SFXDescription. If the sound referred to by the source is not yet fully loaded, there may be a delay before playback actually starts. If there are more active voices than supported by the current SFX device, one SFXSource (this or another one depending on which is deemed least important) will go into virtualized playback mode as a result of calling play().
* **stop( [ float fadeOutTime ] ):** Stop playback. If "fadeOutTime" is given and is  greater than 0, then the source will do a volume fade to zero in "fadeOutTime" seconds and then stop. "fadeOutTime" overrides a setting given in the SFXSource's SFXDescription.
* **pause( [ float fadeOutTime ] ):** Pause playback. If "fadeOutTime" is given and is greater than 0, then the source will do a volume fade to zero in "fadeOutTime" seconds and then pause. "fadeOutTime" overrides a setting given in the SFXSource's SFXDescription.
* **addMarker( string name, float pos ):** Add a marker called "name" at "pos" seconds into playback. If playback passes the given position, the "onMarkerPassed" callback will trigger.


SFXEmitter
------------

Description
^^^^^^^^^^^
An SFXEmitter is a 3D object that emits sound. It has no visible representation (except within the editor), but does have a true location and velocity in 3D world space. Even though an SFXEmitter is an object in 3D space, it need not necessarily emit a 3D sound. It can also emit non-positional 2D sounds.


This is useful for placing background music in a level. There are two ways to set up an SFXEmitter:

* through a predefined SFXProfile ("profile" property)
    * plays the sound specified by the profile
    * uses the profile's SFXDescription
    * some of the emitter's properties override the settings in the profile's SFXDescription (see documentation below)
* directly through a sound file ("fileName" property)
    * uses the properties on the emitter to set up a custom SFXDescription

Setting a "profile" will take precedence over setting a "fileName". Currently it is not possible to have an emitter go through a list of sounds (at least not without scripting). 

Properties
^^^^^^^^^^^

* **profile [SFXProfile]:** The sound profile to play on this emitter. Either use this or "fileName" to set the sound to play. This field will take precedence over "fileName".
* **fileName [FileName]:** The sound file to play on this emitter.
* **playOnAdd [bool]:** If true, playback will be immediately started when the emitter is added to the scene. Applies regardless of whether "profile" or "fileName" is used.
* **isLooping [bool]:** If true, the emitter's sound will loop infinitely. Only applies when using "fileName". For "profile", the profile SFXDescription's "isLooping" value is used.
* **isStreaming [bool]:** If true, the sound will use streamed playback. Only applies when using "fileName". For "profile", the profile SFXDescription's "isStreaming" value is used.
* **channel [int]:** The volume channel to play the sound in. Only applies when using "fileName". For "profile", the profile SFXDescription's "channel" value is used.
* **volume [float]:** The base (unattenuated) volume at which to play the sound. Applies to both "profile" and "fileName". Must be between 0 (min) and 1 (max).
* **pitch [float]:** The frequency shift factor at which to play back the sound. Must be greater than 0. Applies to both "profile" and "fileName".
* **fadeInTime [float]:** Time in seconds to fade volume from zero to full intensity when starting/resuming playback. Must be greater or equal to 0. Only applies when using "fileName". For "profile", the profile SFXDescription's "fadeInTime" value is used.
* **fadeOutTime [float]:** Time in seconds to fade volume out to zero before stopping/pausing playback. Must be greater or equal to 0. Only applies when using "fileName". For "profile", the profile SFXDescription's "fadeOutTime" value is used.
* **is3D [bool]:** If true, the sound will be positional. Only applies when using "fileName". For "profile", the profile SFXDescription's "is3D" value is used.
* **referenceDistance [float]:** The distance at which to start distance-based volume attenuation. Only applies to 3D sounds. Applies to both "profile" and "fileName".
* **maxDistance [float]:** The distance at which to stop distance-based volume attenuation. Only applies to 3D sounds. Applies to both "profile" and "fileName".
* **coneInsideAngle [int]:** Inside 3D cone angle in degrees. Must be between 0 (min) and 360 (max). Only applies to 3D sounds. Applies to both "profile" and "fileName".
* **coneOutsideAngle [int]:** Outside 3D cone angle in degrees. Must be between 0 (min) and 360 (max). Only applies to 3D sounds. Applies to both "profile" and "fileName".
* **coneOutsideVolume [float]:** Volume scale factor outside 3D cone. Must be between (0) (min) and 1 (max). Only applies to 3D sounds. Applies to both "profile" and "fileName".

Methods
^^^^^^^^

* **play():** Sends network event to start playback of the emitter (if not already playing). If called on the client (the ghost), will immediately trigger playback.
* **stop():** Sends network event to stop playback of the emitter (if not already stopped). If called on the client (the ghost), will immediately stop playback.
* **string getPlaybackStatus():** Returns the playback status of the emitter. See SFXSource.getStatus(). If called on a server-side SFXEmitter, the emitter's client-side object (ghost) object on the local client connection will be queried.
* **bool isInRange():** Returns true if the SFX listener (local connection's control object) is currently within the max range of the emitter.


Script Functions
===================

Device Management
------------------
Before sound playback functions can be used, a valid sound device must be created through one of the given sound providers. When using the standard game/core/ scripts, this is automatically taken care of during engine startup.

* **vector sfxGetAvailableDevices():** Returns a vector that describes each of the available devices. Individual devices are separated by newlines and individual properties of devices are separated by tabs.
* **bool sfxCreateDevice( string provider, string device, bool useHardware, int maxBuffers ):** Try to create a new sound device using the given properties. This function must be called before any of the sound playback functions can be used. If there currently is an active device, it will be deleted automatically. Returns true if the operation succeeded and the device has been created.

Each device entry has the following properties (in the order they appear in the vector):

* **providerName [string]:** The name of the sound provider (e.g. "FMOD")
* **deviceName [string]:** The name of the device made available by the provider.
* **hasHardware [bool]:** If true, the device has support for mixing in hardware.
* **maxBuffers [int]:** Maximum number of concurrent buffers supported by the device, i.e. the maximum number of concurrently audible voices. If this is exceeded, playback virtualization will kick in and distribute the available voices across the playing sounds.

In the **game/core** scripts, sound is automatically set up during startup in the sfxStartup() function. Sounds that are playing while the sound device is being changed will be temporarily transitioned to virtualized playback and then resume normal playback once the new device has been created. 

* **sfxDeleteDevice():** Delete the currently active sound device and release all its resources. In the core scripts, this is done automatically for you during shutdown in the sfxShutdown() function. SFXSources that are still playing will be transitioned to virtualized playback mode. When creating a new device, they will automatically transition back to normal playback.
* **vector sfxGetDeviceInfo():** Return information about the currently active sound device. The return value is a tab-delimited string containing the following properties (in the order they appear in the vector):
* **providerName [string]:** Name of the sound provider that supplies the device (e.g. "FMOD").
* **deviceName [string]:** Name of the device on the provider.
* **usesHardware [bool]:** If true, device is set up to use hardware mixing.
* **maxBuffers [int]:** Maximum number of concurrent voices the device is configured to use.

Configuration
--------------

* **float sfxGetMasterVolume():** Return the system master volume. This volume level scales the volume of all independent volume channels simultaneously. Default is 1.
* **sfxSetMasterVolume( float volume ):** Set the system master volume. Must be between 0 (min) and 1 (max). This will affect all currently active sounds.
* **float sfxGetChannelVolume( int channel ):** Return the volume level of the given channel. Will be between 0 and 1. Default is 1.
* **sfxSetChannelVolume( int channel, float volume ):** Set the volume level of the given channel. Must be between 0 (min) and 1 (max). This will affect all sounds currently playing on that channel.
* **string sfxGetDistanceModel():** Return the name of the distance model currently used for distance attenuation of 3D sounds. Currently, this is either "linear" or "logarithmic". Default is set by "$pref::SFX::distanceModel". If unset, the linear distance model is used.
* **sfxSetDistanceModel( string model ):** Set the distance model to use for distance attenuation of 3D sounds. Must be either "linear" or "logarithmic". This will affect the volume attenuation of all currently active 3D sounds.
* **float sfxGetDopplerFactor():** Return the factor applied to doppler effects on 3D sounds. Default is set by "$pref::SFX::dopplerFactor". If unset, default is 0.5.
* **sfxSetDopplerFactor( float factor ):** Set the factor to apply to doppler effects on 3D sounds. Set to zero to turn off pitch shifting caused by the Doppler Effect. The higher the value, the more pronounced the Doppler Effect will be.
* **float sfxGetRolloffFactor():** Get the scale factor applied to distance attenuation curves of 3D sounds in the logarithmic distance model. Default is taken from "$pref::SFX::rolloffFactor". If unset, default is 1.0, i.e. no scaling.
* **sfxSetRolloffFactor( float factor ):** Set the scale factor to apply to distance attenuation curves of 3D sounds in the logarithmic distance model. Values greater than 1 cause volume to decrease faster with distance where as values less than 1 cause volume to decrease slower. A value of 0 will disable distance attenuation. Factor must be greater or equal to 0.


Playback
----------

* **SFXSource sfxCreateSource( SFXProfile profile [, float x, float y, float z ] ):** Create a new SFXSource that plays the given profile. If coordinates are given, the source will be placed at the given position (though only if the given profile contains a 3D sound). The source will initially be in "stopped" state. If the sound contained in the profile has not yet been loaded, this will be initiated in the process.
* **SFXSource sfxCreateSource( SFXDescription description, string filename [, float x, float y, float z ] ):** Create a temporary SFXProfile using the given description and filename and then create a new SFXSource that plays the profile. If coordinates are given, the source will be placed at the given position (though only if the description has is3D set to true). The source will initially be in "stopped" state. Loading of the given file will be initiated in the process.
* **SFXSource sfxPlay( SFXSource source ):** Start playing the given SFXSource. This is the same as calling the play() method on the SFXSource directly. Returns source or null on failure.
* **SFXSource sfxPlay( SFXProfile profile [, float x, float y, float z ] ):** This is the same as calling sfxPlayOnce() with the given parameters.
* **SFXSource sfxPlayOnce(SFXProfile profile [, float x, float y, float z ] ):** Create a play-once SFXSource using the given profile and start playing it. The SFXSource will only be valid for as long as playback is running. If coordinates are given, the SFXSource will be placed at the specified position (only if the profile contains a 3D sound). The SFXSource will return in "playing" state. Returns a handle for the temporary SFXSource or null on failure.
* **SFXSource sfxPlayOnce( SFXDescription description, string filename [, float x, float y, float z ] ):** Creates a temporary SFXProfile with the given description and filename and then instantiates a new play-once SFXSource playing the profile. The SFXSource will be valid only for as long as playback is running. If coordinates are given, the SFXSource will be placed at the specified position (only if the given SFXDescription has is3D set to true). The SFXSource will return in "playing" state. Returns a handle for the temporary SFXSource or null on failure.
* **sfxStop( SFXSource source ):** Stop playing the given SFXSource. This is the same as calling the stop() method directly on the SFXSource.
* **sfxStopAll():** Call stop() on all SFXSources that are currently playing.


Misc
-----
* **sfxDumpSources():** Print a detailed rundown on all currently instantiated SFXSources to the console.

Conclusion
============
This interface guide covers everything you will need to know about using Torque 3D's stock sound effect system (SFX).