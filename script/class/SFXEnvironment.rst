SFXEnvironment
==============

Description of a reverb environment.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

A reverb environment specifies how the audio mixer should render advanced environmental audio effects.

To use reverb environments in your level, set up one or more ambient audio spaces, assign reverb environments appropriately, and then attach the SFXAmbiences to your LevelInfo (taking effect globally) or Zone objects (taking effect locally).

To define your own custom reverb environments, it is usually easiest to adapt one of the pre-existing reverb definitions::

	singleton SFXEnvironment( AudioEnvCustomUnderwater : AudioEnvUnderwater )
	{
	   // Override select properties from AudioEnvUnderwater here.
	};

In the Datablock Editor, this can be done by selecting an existing environment to copy from when creating the SFXEnvironment datablock.

For a precise description of reverb audio and the properties of this class, please consult the EAX documentation.

All SFXEnvironment instances are automatically added to the global SFXEnvironmentSet.

Fields
------

.. cpp:member:: float  SFXEnvironment::airAbsorptionHF

	Change in level per meter at high frequencies.

.. cpp:member:: float  SFXEnvironment::decayHFRatio

	High-frequency to mid-frequency decay time ratio.

.. cpp:member:: float  SFXEnvironment::decayLFRatio

	Low-frequency to mid-frequency decay time ratio.

.. cpp:member:: float  SFXEnvironment::decayTime

	Reverberation decay time at mid frequencies.

.. cpp:member:: float  SFXEnvironment::density

	Value that controls the modal density in the late reverberation decay.

.. cpp:member:: float  SFXEnvironment::diffusion

	Value that controls the echo density in the late reverberation decay.

.. cpp:member:: float  SFXEnvironment::echoDepth

	Echo depth.

.. cpp:member:: float  SFXEnvironment::echoTime

	Echo time.

.. cpp:member:: float  SFXEnvironment::envDiffusion

	Environment diffusion.

.. cpp:member:: float  SFXEnvironment::envSize

	Environment size in meters.

.. cpp:member:: int  SFXEnvironment::flags

	A bitfield of reverb flags.

.. cpp:member:: float  SFXEnvironment::HFReference

	Reference high frequency in Hertz.

.. cpp:member:: float  SFXEnvironment::LFReference

	Reference low frequency in Hertz.

.. cpp:member:: float  SFXEnvironment::modulationDepth

	Modulation depth.

.. cpp:member:: float  SFXEnvironment::modulationTime

	Modulation time.

.. cpp:member:: int  SFXEnvironment::reflections

	Early reflections level relative to room effect.

.. cpp:member:: float  SFXEnvironment::reflectionsDelay

	Initial reflection delay time.

.. cpp:member:: float  SFXEnvironment::reflectionsPan [3]

	Early reflections panning vector.

.. cpp:member:: int  SFXEnvironment::reverb

	Late reverberation level relative to room effect.

.. cpp:member:: const int  SFXEnvironment::REVERB_CORE0  [static]

	PS2 Only - Reverb is applied to CORE0 (hw voices 0-23).

.. cpp:member:: const int  SFXEnvironment::REVERB_CORE1  [static]

	PS2 Only - Reverb is applied to CORE1 (hw voices 24-47).

.. cpp:member:: const int  SFXEnvironment::REVERB_DECAYHFLIMIT  [static]

	SFXEnvironment::airAbsorptionHF affects SFXEnvironment::decayHFRatio .

.. cpp:member:: const int  SFXEnvironment::REVERB_DECAYTIMESCALE  [static]

	SFXEnvironment::envSize affects reverberation decay time.

.. cpp:member:: const int  SFXEnvironment::REVERB_ECHOTIMESCALE  [static]

	SFXEnvironment::envSize affects echo time.

.. cpp:member:: const int  SFXEnvironment::REVERB_HIGHQUALITYDPL2REVERB  [static]

	GameCube/Wii Only - Use high-quality DPL2 reverb.

.. cpp:member:: const int  SFXEnvironment::REVERB_HIGHQUALITYREVERB  [static]

	GameCube/Wii Only - Use high-quality reverb.

.. cpp:member:: const int  SFXEnvironment::REVERB_MODULATIONTIMESCALE  [static]

	SFXEnvironment::envSize affects modulation time.

.. cpp:member:: const int  SFXEnvironment::REVERB_REFLECTIONSDELAYSCALE  [static]

	SFXEnvironment::envSize affects initial reflection delay time.

.. cpp:member:: const int  SFXEnvironment::REVERB_REFLECTIONSSCALE  [static]

	SFXEnvironment::envSize affects reflection level.

.. cpp:member:: const int  SFXEnvironment::REVERB_REVERBDELAYSCALE  [static]

	SFXEnvironment::envSize affects late reverberation delay time.

.. cpp:member:: const int  SFXEnvironment::REVERB_REVERBSCALE  [static]

	SFXEnvironment::envSize affects reflections level.

.. cpp:member:: float  SFXEnvironment::reverbDelay

	Late reverberation delay time relative to initial reflection.

.. cpp:member:: float  SFXEnvironment::reverbPan [3]

	Late reverberation panning vector.

.. cpp:member:: int  SFXEnvironment::room

	Room effect level at mid-frequencies.

.. cpp:member:: int  SFXEnvironment::roomHF

	Relative room effect level at high frequencies.

.. cpp:member:: int  SFXEnvironment::roomLF

	Relative room effect level at low frequencies.

.. cpp:member:: float  SFXEnvironment::roomRolloffFactor

	Logarithmic distance attenuation rolloff scale factor for reverb room size effect.
