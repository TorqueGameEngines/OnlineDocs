Overview
**********

Introduction
===============

SFX is the new 2D and 3D audio system for Torque 3D. It was designed to provide the basic features for sound playback across multiple platforms, sound devices, and audio libraries. This guide is a high level overview of the SFX module and what systems it supports.

**Recommendation:** For the best cross-platform support as well as for the best compatibility with future additions to SFX, it is recommended to either use OpenAL or FMOD with SFX. A number of future additions will likely not be supported with other sound APIs.

Two Playback Types
===================

Each individual sound can be played back in two ways. The type of playback used by the sound system for a particular sound is determined by the "isStreaming"property of its SFXDescription (SFXInterface.html#SFXDescription)

Note: *With either form of playback, sound data is stored in uncompressed form on the device. For compressed formats, decompression occurs during sound loading. For streamed sounds, this is a continuous process. All sound loading happens on worker threads regardless of how it is played back so it does not tax the main thread.*

Buffered
---------

DEFINITION: Sample data completely offloaded to a sound device in one contiguous chunk. Ideal for small sounds, such as "place once" effects (e.g. gun fire, collision audio, etc).

**Advantages**

#. Fast seeking
#. No overhead after loading
#. Sound data can be shared between simultaneous playbacks

**Disadvantages**

#. May consume a lot of memory on the device (depending on sample data size)
#. May take longer to load (depending on sample data size)
#. May fail to load entirely depending on device (depending on sample data size)
#. Needs entire sound stream to be available before playback can start

Streamed
---------

DEFINITION: Small buffer allocated on a sound device and data is progressively loaded in the background as playback progresses. Ideal for large sounds (e.g. music) and continuous streams (e.g. voice chat). This feature is fully threaded; playback will continue normally even if Torque 3D is, for example, busy loading a level.


**Advantages**

#. Small footprint on sound device
#. Loads quickly
#. Can play sound streams for which only part of the data is available

**Disadvantages**

#. Incurs a certain continuous overhead
#. Data for a sound cannot be shared between playbacks
#. Seeking needs to reset stream feed and will generally incur a delay
#. End-of-stream notifications may be imprecise (depends on actual sound device used)

3D Sound
=========

Sounds can be positional (3D) or non-positional (2D). Positional sounds are located in Torque's three-dimensional world. Whether a sound is 2D or 3D is determined by the "is3D" property of its SFXDescription. (SFXInterface.html#SFXDescription)

3D sounds will be mixed at varying volumes and distributed dynamically to the sound card's output channels depending on the player's position and velocity in relation to the sound's own position and velocity. This is computed independently for each playing 3D sound.

Each 3D sound has a position, an orientation, and a velocity. To represent 3D sounds by real objects in Torque 3D, use SFXEmitters. (SFXInterface.html#SFXEmitter)

**!! Important !!:** 3D sounds must be single channel (mono). This is a requirement coming from the sound APIs. Currently, 3D sound is completely agnostic to the environment. This means that to the SFX system the entire world is one single empty space and sound will propagate uniformly and unencumbered in all directions. 

Distance Attenuation
---------------------

Just like sound in the real world, 3D sounds become less audible the farther away you are from their source. Distance attenuation then refers to the process of computing the level of volume that a given 3D sound has at a certain distance away from its origin.

The process of setting up distance attenuation is described in more detail in Configuring 3D Playback. (SFXInterface.html#Configuring_3D_Playback)

**Sound Cones**

Distance attenuation works uniformly in all direction regardless of the actual direction of the sound. Sound cones allow you to add directional volume attenuation to distance attenuation.

There are two cones defined on each 3D sound that affect volume attenuation. Both have a their upwards axis aligned with the sound's direction and their tips at the sound's origin. The width of each cone is defined by an angle. By default this angle is 360 degrees meaning that the sound spreads in all directions.

By narrowing the angle, the cone will get smaller and the sound will spread only across a certain range in its direction. Of the two cones, one is the inner cone and one is the outer cone.

Within the inner cone, the 3D sound will retain full volume as specified in its SFXDescription (attenuated only by the sound channel it is assigned to and, of course, the master volume of the system).

Outside of the outer cone, the 3D sound's volume will be attenuated by the scale factor set by **"coneOutsideVolume"** property of its SFXDescription. Then, within the transitioning zone between the inner code to outside the outer cone, the volume will gradually shift from an attenuation of 1.0 (inside inner cone) to an attenuation of "coneOutsideVolume".

Note: Cone settings from SFXDescriptions can be overridden for individual SFXSources using the setCone() method. (SFXInterface.html#SFXSource)

To gain a better understanding of how sound cones work, read through this MSDN article on sound cones. (https://msdn.microsoft.com/en-us/library/ee418803(v=VS.85).aspx)

Doppler Effect Also known as Doppler Shift, this effect is the change in frequency of a wave for an observer moving relative to the source of the waves, similar to how you perceive a loud motorcycle approaching and passing you. The following articles contain a more in depth description: 

* Wikipedia Entry (https://en.wikipedia.org/wiki/Doppler_effect)
* Kettering Article (http://www.acs.psu.edu/drussell/Demos/doppler/doppler.html)

Playback Virtualization
=========================

In any given situation, a game may have more sounds playing concurrently than are actually supported by the underlying device. To cope with this, the SFX system uses what is called playback virtualization.

During SFX's update routine, the system will compute effective volumes for all playing sounds. If there are more sounds playing than are supported by the underlying SFX device, the system will reassign voices from the least audible (usually the sounds farthest from the player) sounds to more audible sounds.

A sound source that is playing but loses its voice on the device will transition into virtualized playback mode. In this mode, the sound will continue to have its play cursor advance in real-time but there will not be actual audio output on the device.

Voice distribution is re-evaluated on each SFX update so a given sound that has been transitioned to virtualized playback mode may later regain a voice and transition back to normal playback.

Supported Audio Formats
=========================

SFX supports WAV and Vorbis across all devices. In addition, devices may implement their own file loading which will take precedence over the built-in loading code. See Supported APIs for more information.

Live Asset Updating is supported by SFX meaning that if a sound file changes on disk, it will automatically be reloaded by the SFX system. All sources playing the sound will temporarily transition to virtualized playback and then transition to normal playback when the file has been reloaded. 

WAV
----

* **Premise:** Uncompressed format that is most useful for sound production
* **Pro:** Uncompromising sound quality
* **Con:** Consumes lots of disk space

Note: At the moment, none of the enhanced features of WAVs (loops, markers, etc.) are supported.

Ogg/Vorbis
-----------

* **Premise:** High-quality compressed format (usually outperforms rival lossy sound compression formats such as MP3 or WMA)
* **Pro:** Very good quality/size ratio
* **Con:** Compression is lossy (with proper settings, this should not be noticeable in most all game settings)

Supported Sound APIs
======================

The SFX system supports several different sound APIs.

*Note: Switching sound devices at runtime will preserve all SFXProfile and SFXSource states. SFXSources that are currently playing will temporarily transition to virtualized playback.*

DirectSound
------------

Platform: Windows Description: Standard DirectX audio API.

FMOD
-----

**Platforms:** Windows, Mac, XBox, PS3 **Description:** High-quality, highly cross-platform sound API. Must be installed separately. For commercial releases, a license must be obtained.

With FMOD selected, all file loading and streaming will be taken over by the device. If for some reason you want to disabled this feature, set the following global variable in TorqueScript::

	$pref::SFX::FMOD::noCustomFileLoading = 1)
	
The following formats are supported:

* .aiff
* .asf
* .asx
* .dls
* .flac
* .fsb
* .it
* .m3u
* .mid
* .mod
* .mp2
* .mp3
* .ogg
* .pls
* .s3m
* .vag
* .wav
* .wax
* .wma
* .xm
* .xma (on Xbox only)

*Notes:*

* To download FMOD, visit the FMOD homepage http://www.fmod.org/
* To purchase a very friendly priced indie license of FMOD for your game, visit the GarageGames store. http://www.garagegames.com/products/fmod
* At the moment, Live Asset Updating is not available with sounds that have been loaded directly through FMOD.
* Currently, using play list files with FMOD is the only way to use play lists with SFX.

OpenAL
-------
**Platforms:** Windows, Mac **Description:** A cross-platform 3D audio API appropriate for use with gaming applications and many other types of audio applications.

*Note: On Windows, OpenAL must be installed separately. Visit the OpenAL website for more details* 

* http://connect.creativelabs.com/openal/default.aspx

XAudio
-------
**Platforms:** Windows, XBox **Description:** InterTrust's fast and robust, multi-platform solution for digital playback. Targets MPEG Audio (MP1, MP2, and MP3) decoding. It is offered in the form of a developer's kit (SDK), which includes the Xaudio decoding engine.

Null
-----
**Platforms:** Windows, Mac **Description:** Stub device for dedicated servers. Simulates playback. No actual audio output.

Conclusion
===========
This document is intended to provide you with the base knowledge of SFX's capabilities.
