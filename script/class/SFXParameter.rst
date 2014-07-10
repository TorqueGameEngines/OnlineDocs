SFXParameter
============

A sound channel value that can be bound to multiple sound sources.

Inherit:
	:doc:`SimObject`

Description
-----------

Parameters are special objects that isolate a specific property that sound sources can have and allows to bind this isolated instance to multiple sound sources such that when the value of the parameter changes, all sources bound to the parameter will have their respective property changed.

Parameters are identified and referenced by their internalName. This means that the SFXDescription::parameters and SFXTrack::parameters fields should contain the internalNames of the SFXParameter objects which should be attached to the SFXSources when they are created. No two SFXParameters should have the same internalName.

All SFXParameter instances are automatically made children of the SFXParameterGroup.

Parameter Updates
~~~~~~~~~~~~~~~~~

Parameters are periodically allowed to update their own values. This makes it possible to attach custom logic to a parameter and have individual parameters synchronize their values autonomously. Use the onUpdate() callback to attach script code to a parameter update.

Example::

	newSFXParameter( EngineRPMLevel )
	{
	   // Set the name by which this parameter is identified.
	   internalName = "EngineRPMLevel";
	
	   // Let this parameter control the pitch of attached sources to simulate engine RPM ramping up and down.
	   channel = "Pitch";
	
	   // Start out with unmodified pitch.
	   defaultValue = 1;
	
	   // Add a texture description of what this parameter does.
	   description = "Engine RPM Level";
	};
	
	// Create a description that automatically attaches the engine RPM parameter.
	singleton SFXDescription( EngineRPMSound : AudioLoop2D )
	{
	   parameters[ 0 ] = "EngineRPMLevel";
	};
	
	// Create sound sources for the engine.
	sfxCreateSource( EngineRPMSound, "art/sound/engine/enginePrimary" );
	sfxCreateSource( EngineRPMSound, "art/sound/engine/engineSecondary" );
	
	// Setting the parameter value will now affect the pitch level of both sound sources.
	EngineRPMLevel.value = 0.5;
	EngineRPMLevel.value = 1.5;


Methods
-------

.. cpp:function:: String SFXParameter::getParameterName()

	Get the name of the parameter.

	:return: The paramete name. 

.. cpp:function:: void SFXParameter::onUpdate()

	Called when the sound system triggers an update on the parameter. This occurs periodically during system operation.

.. cpp:function:: void SFXParameter::reset()

	Reset the parameter's value to its default.

Fields
------

.. cpp:member:: SFXChannel SFXParameter::channel

	Channel that the parameter controls. This controls which property of the sources it is attached to the parameter controls.

.. cpp:member:: float  SFXParameter::defaultValue

	Value to which the parameter is initially set. When the parameter is first added to the system, value will be set to defaultValue .

.. cpp:member:: string  SFXParameter::description

	Textual description of the parameter. Primarily for use in the Audio Parameters dialog of the editor to allow for easier identification of parameters.

.. cpp:member:: Point2F  SFXParameter::range

	Permitted range for value . Minimum and maximum allowed value for the parameter. Both inclusive. For all but the User0-3 channels, this property is automatically set up by SFXParameter .

.. cpp:member:: float  SFXParameter::value

	Current value of the audio parameter. All attached sources are notified when this value changes.
