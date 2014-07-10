SFXDescription
==============

A description for how a sound should be played.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

SFXDescriptions are used by the sound system to collect all parameters needed to set up a given sound for playback. This includes information like its volume level, its pitch shift, etc. as well as more complex information like its fade behavior, 3D properties, and per-sound reverb properties.

Any sound playback will require a valid SFXDescription.

As datablocks, SFXDescriptions can be set up as either networked datablocks or non-networked datablocks, though it generally makes sense to keep all descriptions non-networked since they will be used exclusively by clients.

Example::

	// A description for a 3D sound with a reasonable default range setting.
	// The description is set up to assign sounds to the AudioChannelEffects source group
	// (defined in the core scripts).  An alternative means to achieve this is to use the
	// AudioEffects description as a copy source (": AudioEffects").
	
	singleton SFXDescription( Audio3DSound )
	{
	  sourceGroup       = AudioChannelEffects;
	  is3D              = true;
	  referenceDistance = 20.0;
	  maxDistance       = 100.0;
	};

Fields
------

.. cpp:member:: int  SFXDescription::coneInsideAngle

	Inner sound cone angle in degrees. This value determines the angle of the inner volume cone that protrudes out in the direction of a sound. Within this cone, the sound source retains full volume that is unaffected by sound cone settings (though still affected by distance attenuation.) Valid values are from 0 to 360. Must be less than coneOutsideAngle. Default is 360. Only for 3D sounds. Sound Cones

.. cpp:member:: int  SFXDescription::coneOutsideAngle

	Outer sound cone angle in degrees. This value determines the angle of the outer volume cone that protrudes out in the direction of a sound and surrounds the inner volume cone. Within this cone, volume will linearly interpolate from the outer cone hull inwards to the inner coner hull starting with the base volume scaled by coneOutsideVolume and ramping up/down to the full base volume. Valid values are from 0 to 360. Must be gt = coneInsideAngle. Default is 360. Only for 3D sounds. Sound Cones

.. cpp:member:: float  SFXDescription::coneOutsideVolume

	Determines the volume scale factor applied the a source's base volume level outside of the outer cone. In the outer cone, starting from outside the inner cone, the scale factor smoothly interpolates from 1.0 (within the inner cone) to this value. At the moment, the allowed range is 0.0 (silence) to 1.0 (no attenuation) as amplification is only supported on XAudio2 but not on the other devices. Only for 3D sound. Sound Cones

.. cpp:member:: EaseF  SFXDescription::fadeInEase

	Easing curve for fade-in transition. Volume fade-ins will interpolate volume along this curve. Volume Fades

.. cpp:member:: float  SFXDescription::fadeInTime

	Number of seconds to gradually fade in volume from zero when playback starts. Must be gt = 0. Volume Fades

.. cpp:member:: bool  SFXDescription::fadeLoops

	Fade each cycle of a loop in and/or out; otherwise only fade-in first cycle. By default, volume fading is applied to the beginning and end of the playback range, i.e. a fade-in segment is placed at the beginning of the sound and a fade-out segment is paced at the end of a sound. However, when looping playback, this may be undesirable as each iteration of the sound will then have a fade-in and fade-out effect. To set up looping sounds such that a fade-in is applied only when the sound is first started (or playback resumed) and a fade-out is only applied when the sound is explicitly paused or stopped, set this field to true. Default is false. Volume Fades

.. cpp:member:: EaseF  SFXDescription::fadeOutEase

	Easing curve for fade-out transition. Volume fade-outs will interpolate volume along this curve. Volume Fades

.. cpp:member:: float  SFXDescription::fadeOutTime

	Number of seconds to gradually fade out volume down to zero when playback is stopped or paused. Must be gt =0. Volume Fades

.. cpp:member:: bool  SFXDescription::is3D

	If true, sounds played with this description will have a position and orientation in space. Unlike a non-positional sound, a 3D sound will have its volume attenuated depending on the distance to the listener in space. The farther the sound moves away from the listener, the less audible it will be. Non-positional sounds, in contrast, will remain at their original volume regardless of where the listener is. 3D Audio Volume Attenuation

.. cpp:member:: bool  SFXDescription::isLooping

	If true, the sound will be played in an endless loop. Default is false.

.. cpp:member:: bool  SFXDescription::isStreaming

	If true, incrementally stream sounds; otherwise sounds are loaded in full. Streaming vs. Buffered Audio

.. cpp:member:: float  SFXDescription::maxDistance

	The distance at which attenuation stops. In the linear distance model, the attenuated volume will be zero at this distance. In the logarithmic model, attenuation will simply stop at this distance and the sound will keep its attenuated volume from there on out. As such, it primarily functions as a cutoff factor to exponential distance attentuation to limit the number of voices relevant to updates. Only applies to 3D sounds. 3D Audio Volume Attenuation

.. cpp:member:: string  SFXDescription::parameters [8]

	Names of the parameters to which sources using this description will automatically be linked. Individual parameters are identified by their internalName . Interactive Audio

.. cpp:member:: float  SFXDescription::pitch

	Pitch shift to apply to playback. The pitch assigned to a sound determines the speed at which it is played back. A pitch shift of 1 plays the sound at its default speed. A greater shift factor speeds up playback and a smaller shift factor slows it down. Must be gt 0. Default is 1.

.. cpp:member:: float  SFXDescription::priority

	Priority level for virtualization of sounds (1 = base level). When there are more concurrently active sounds than supported by the audio mixer, some of the sounds need to be culled. Which sounds are culled first depends primarily on total audibility of individual sounds. However, the priority of invidual sounds may be decreased or decreased through this field. Sounds and Voices

.. cpp:member:: float  SFXDescription::referenceDistance

	Distance at which volume attenuation begins. Up to this distance, the sound retains its base volume. In the linear distance model, the volume will linearly from this distance onwards up to maxDistance where it reaches zero. In the logarithmic distance model, the reference distance determine how fast the sound volume decreases with distance. Each referenceDistance steps (scaled by the rolloff factor), the volume halves. A rule of thumb is that for sounds that require you to be close to hear them in the real world, set the reference distance to small values whereas for sounds that are widely audible set it to larger values. Only applies to 3D sounds. 3D Audio Volume Attenuation

.. cpp:member:: const int  SFXDescription::REVERB_DIRECTHFAUTO  [static]

	Automatic setting of SFXDescription::reverbDirect due to distance to listener.

.. cpp:member:: const int  SFXDescription::REVERB_INSTANCE0  [static]

	EAX4/SFX/GameCube/Wii: Specify channel to target reverb instance 0. Default target.

.. cpp:member:: const int  SFXDescription::REVERB_INSTANCE1  [static]

	EAX4/SFX/GameCube/Wii: Specify channel to target reverb instance 1.

.. cpp:member:: const int  SFXDescription::REVERB_INSTANCE2  [static]

	EAX4/SFX/GameCube/Wii: Specify channel to target reverb instance 2.

.. cpp:member:: const int  SFXDescription::REVERB_INSTANCE3  [static]

	EAX4/SFX/GameCube/Wii: Specify channel to target reverb instance 3.

.. cpp:member:: const int  SFXDescription::REVERB_ROOMAUTO  [static]

	Automatic setting of SFXDescription::reverbRoom due to distance to listener.

.. cpp:member:: const int  SFXDescription::REVERB_ROOMHFAUTO  [static]

	Automatic setting of SFXDescription::reverbRoomHF due to distance to listener.

.. cpp:member:: float  SFXDescription::reverbAirAbsorptionFactor

	Multiplies SFXEnvironment::airAbsorptionHR.

.. cpp:member:: int  SFXDescription::reverbDirect

	Direct path level (at low and mid frequencies).

.. cpp:member:: int  SFXDescription::reverbDirectHF

	Relative direct path level at high frequencies.

.. cpp:member:: float  SFXDescription::reverbDopplerFactor

	Per-source doppler factor.

.. cpp:member:: int  SFXDescription::reverbExclusion

	Main exclusion control (attenuation at high frequencies).

.. cpp:member:: float  SFXDescription::reverbExclusionLFRatio

	Exclusion low-frequency level re. main control.

.. cpp:member:: int  SFXDescription::reverbFlags

	Bitfield combination of per-sound reverb flags.

.. cpp:member:: int  SFXDescription::reverbObstruction

	Main obstruction control (attenuation at high frequencies).

.. cpp:member:: float  SFXDescription::reverbObstructionLFRatio

	Obstruction low-frequency level re. main control.

.. cpp:member:: int  SFXDescription::reverbOcclusion

	Main occlusion control (attenuation at high frequencies).

.. cpp:member:: float  SFXDescription::reverbOcclusionDirectRatio

	Relative occlusion control for direct path.

.. cpp:member:: float  SFXDescription::reverbOcclusionLFRatio

	Occlusion low-frequency level re. main control.

.. cpp:member:: float  SFXDescription::reverbOcclusionRoomRatio

	Relative occlusion control for room effect.

.. cpp:member:: int  SFXDescription::reverbOutsideVolumeHF

	Outside sound cone level at high frequencies.

.. cpp:member:: float  SFXDescription::reverbReverbRolloffFactor

	Per-source logarithmic falloff factor.

.. cpp:member:: int  SFXDescription::reverbRoom

	Room effect level (at low and mid frequencies).

.. cpp:member:: int  SFXDescription::reverbRoomHF

	Relative room effect level at high frequencies.

.. cpp:member:: float  SFXDescription::reverbRoomRolloffFactor

	Room effect falloff factor.

.. cpp:member:: float  SFXDescription::rolloffFactor

	Scale factor to apply to logarithmic distance attenuation curve. If -1, the global rolloff setting is used.

.. cpp:member:: Point3F  SFXDescription::scatterDistance

	Bounds on random displacement of 3D sound positions. When a 3D sound is created and given its initial position in space, this field is used to determine the amount of randomization applied to the actual position given to the sound system. The randomization uses the following scheme:

.. cpp:member:: SFXSource SFXDescription::sourceGroup

	Group that sources playing with this description should be put into. When a sound source is allocated, it will be made a child of the source group that is listed in its description. This group will then modulate several properties of the sound as it is played. For example, one use of groups is to segregate sounds so that volume levels of different sound groups such as interface audio and game audio can be controlled independently. Source Hierarchies

.. cpp:member:: int  SFXDescription::streamPacketSize

	Number of seconds of sample data per single streaming packet. This field allows to fine-tune streaming for individual sounds. The streaming system processes streamed sounds in batches called packets. Each packet will contain a set amount of sample data determined by this field. The greater its value, the more sample data each packet contains, the more work is done per packet. Streaming vs. Buffered Audio

.. cpp:member:: int  SFXDescription::streamReadAhead

	Number of sample packets to read and buffer in advance. This field determines the number of packets that the streaming system will try to keep buffered in advance. As such it determines the number of packets that can be consumed by the sound device before the playback queue is running dry. Greater values thus allow for more lag in the streaming pipeline. Streaming vs. Buffered Audio

.. cpp:member:: bool  SFXDescription::useCustomReverb

	If true, use the reverb properties defined here on sounds. By default, sounds will be assigned a generic reverb profile. By setting this flag to true, a custom reverb setup can be defined using the "Reverb" properties that will then be assigned to sounds playing with the description. Audio Reverb

.. cpp:member:: bool  SFXDescription::useHardware

	Whether the sound is allowed to be mixed in hardware. If true, the sound system will try to allocate the voice for the sound directly on the sound hardware for mixing by the hardware mixer. Be aware that a hardware mixer may not provide all features available to sounds mixed in software.

.. cpp:member:: float  SFXDescription::volume

	Base volume level for the sound. This will be the starting point for volume attenuation on the sound. The final effective volume of a sound will be dependent on a number of parameters. Must be between 0 (mute) and 1 (full volume). Default is 1. Volume Attenuation
