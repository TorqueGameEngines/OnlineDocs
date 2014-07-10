SFXSource
=========

Playback controller for a sound source.

Inherit:
	:doc:`SimGroup`

Description
-----------

All sound playback is driven by SFXSources. Each such source represents an independent playback controller that directly or indirectly affects sound output.

While this class itself is instantiable, such an instance will not by itself emit any sound. This is the responsibility of its subclasses. Note, however, that none of these subclasses must be instantiated directly but must instead be instantiated indirectly through the SFX interface.

Play-Once Sources
~~~~~~~~~~~~~~~~~

Often, a sound source need only exist for the duration of the sound it is playing. In this case so-called "play-once" sources simplify the bookkeeping involved by leaving the deletion of sources that have expired their playtime to the sound system.

Play-once sources can be created in either of two ways:

* sfxPlayOnce(): Directly create a play-once source from a SFXTrack or file.
* sfxDeleteWhenStopped(): Retroactively turn any source into a play-once source that will automatically be deleted when moving into stopped state.

Source Hierarchies
~~~~~~~~~~~~~~~~~~

Source are arranged into playback hierarchies where a parent source will scale some of the properties of its children and also hand on any play(), pause(), and stop() commands to them. This allows to easily group sounds into logical units that can then be operated on as a whole.

An example of this is the segregation of sounds according to their use in the game. Volume levels of background music, in-game sound effects, and character voices will usually be controlled independently and putting their sounds into different hierarchies allows to achieve that easily.

The source properties that are scaled by parent values are:

* volume,
* pitch, and
* priority

This means that if a parent has a volume of 0.5, the child will play at half the effective volume it would otherwise have.

Additionally, parents affect the playback state of their children:

* A parent that is in stopped state will force all its direct and indirect children into stopped state.
* A parent that is in paused state will force all its direct and indirect children that are playing into paused state. However, children that are in stopped state will not be affected.
* A parent that is in playing state will not affect the playback state of its children.

Each source maintains a state that is wants to be in which may differ from the state that is enforced on it by its parent. If a parent changes its states in a way that allows a child to move into its desired state, the child will do so.

For logically grouping sources, instantiate the SFXSource class directly and make other sources children to it. A source thus instantiated will not effect any real sound output on its own but will influence the sound output of its direct and indirect children.

.. note::

	Be aware that the property values used to scale child property values are the effective values. For example, the value used to scale the volume of a child is the effective volume of the parent, i.e. the volume after fades, distance attenuation, etc. has been applied.

Volume Attenuation
~~~~~~~~~~~~~~~~~~

During its lifetime, the volume of a source will be continually updated. This update process always progresses in a fixed set of steps to compute the final effective volume of the source based on the base volume level that was either assigned from the SFXDescription associated with the source (SFXDescription::volume) or manually set by the user. The process of finding a source's final effective volume is called "volume attenuation". The steps involved in attenuating a source's volume are (in order):

Fading
	If the source currently has a fade-effect applied, the volume is interpolated along the currently active fade curve.

Modulation
	If the source is part of a hierarchy, it's volume is scaled according to the effective volume of its parent.

Distance Attenuation
	If the source is a 3D sound source, then the volume is interpolated according to the distance model in effect and current listener position and orientation (see 3D Audio).

Volume Fades
~~~~~~~~~~~~

To ease-in and ease-out playback of a sound, fade effects may be applied to sources. A fade will either go from zero volume to full effective volume (fade-in) or from full effective volume to zero volume (fade-out).

Fading is coupled to the play(), pause(), and stop() methods as well as to loop iterations when SFXDescription::fadeLoops is true for the source. play() and the start of a loop iteration will trigger a fade-in whereas pause(), stop() and the end of loop iterations will trigger fade-outs.

For looping sources, if SFXDescription::fadeLoops is false, only the initial play() will trigger a fade-in and no further fading will be applied to loop iterations.

By default, the fade durations will be governed by the SFXDescription::fadeInTime and SFXDescription::fadeOutTime properties of the SFXDescription attached to the source. However, these may be overridden on a per-source basis by setting fade times explicitly with setFadeTimes(). Additionally, the set values may be overridden for individual play(), pause(), and stop() calls by supplying appropriate fadeInTime/fadeOutTime parameters.

By default, volume will interpolate linearly during fades. However, custom interpolation curves can be assigned through the SFXDescription::fadeInEase and SFXDescription::fadeOutTime properties.

Sound Cones
~~~~~~~~~~~~

Doppler Effect
~~~~~~~~~~~~~~

Playback Markers
~~~~~~~~~~~~~~~~

Playback markers allow to attach notification triggers to specific playback positions. Once the play cursor crosses a position for which a marker is defined, the onMarkerPassed callback will be triggered on the SFXSource thus allowing to couple script logic to .

Be aware that the precision with which marker callbacks are triggered are bound by global source update frequency. Thus there may be a delay between the play cursor actually passing a marker position and the callback being triggered.

Methods
-------

.. cpp:function:: void SFXSource::addMarker(String name, float pos)

	Add a notification marker called name at pos seconds of playback.

	:param name: Symbolic name for the marker that will be passed to the onMarkerPassed() callback.
	:param pos: Playback position in seconds when the notification should trigger. Note that this is a soft limit and there may be a delay between the play cursor actually passing the position and the callback being triggered.

	Example::

		// Create a new source.
		$source = sfxCreateSource( AudioMusicLoop2D, "art/sound/backgroundMusic" );
		
		// Assign a class to the source.
		$source.class = "BackgroundMusic";
		
		// Add a playback marker at one minute into playback.
		$source.addMarker( "first", 60 );
		
		// Define the callback function.  This function will be called when the playback position passes the one minute mark.
		function BackgroundMusic::onMarkerPassed( %this, %markerName )
		{
		   if( %markerName $= "first" )
		      echo( "Playback has passed the 60 seconds mark." );
		}
		
		// Play the sound.
		$source.play();

.. cpp:function:: void SFXSource::addParameter(SFXParameter parameter)

	Attach parameter to the source,. Once attached, the source will react to value changes of the given parameter . Attaching a parameter will also trigger an initial read-out of the parameter's current value.

	:param parameter: The parameter to attach to the source.

.. cpp:function:: float SFXSource::getAttenuatedVolume()

	Get the final effective volume level of the source. This method returns the volume level as it is after source group volume modulation, fades, and distance-based volume attenuation have been applied to the base volume level. Volume Attenuation

	:return: The effective volume of the source.

.. cpp:function:: float SFXSource::getFadeInTime()

	Get the fade-in time set on the source. This will initially be SFXDescription::fadeInTime . Volume Fades

	:return: The fade-in time set on the source in seconds.

.. cpp:function:: float SFXSource::getFadeOutTime()

	Get the fade-out time set on the source. This will initially be SFXDescription::fadeOutTime . Volume Fades

	:return: The fade-out time set on the source in seconds.

.. cpp:function:: SFXParameter  SFXSource::getParameter(int index)

	Get the parameter at the given index.

	:param index: Index of the parameter to fetch. Must be 0<=index<=getParameterCount().

	:return:  is out of range.

	Example::

		// Print the name ofo each parameter attached to %source.
		%numParams = %source.getParameterCount();
		for( %i = 0; %i < %numParams; %i ++ )
		   echo( %source.getParameter( %i ).getParameterName() );

.. cpp:function:: int SFXSource::getParameterCount()

	Get the number of SFXParameters that are attached to the source.

	:return: The number of parameters attached to the source.

	Example::

		// Print the name ofo each parameter attached to %source.
		%numParams = %source.getParameterCount();
		for( %i = 0; %i < %numParams; %i ++ )
		   echo( %source.getParameter( %i ).getParameterName() );

.. cpp:function:: float SFXSource::getPitch()

	Get the pitch scale of the source. Pitch determines the playback speed of the source (default: 1).

	:return: The current pitch scale factor of the source.

.. cpp:function:: SFXStatus  SFXSource::getStatus()

	Get the current playback status.

	:return: Te current playback status 

.. cpp:function:: float SFXSource::getVolume()

	Get the current base volume level of the source. This is not the final effective volume that the source is playing at but rather the starting volume level before source group modulation, fades, or distance-based volume attenuation are applied. Volume Attenuation

	:return: The current base volume level.

.. cpp:function:: bool SFXSource::isPaused()

	Test whether the source is currently paused.

	:return: True if the source is in paused state, false otherwise.

.. cpp:function:: bool SFXSource::isPlaying()

	Test whether the source is currently playing.

	:return: True if the source is in playing state, false otherwise.

.. cpp:function:: bool SFXSource::isStopped()

	Test whether the source is currently stopped.

	:return: True if the source is in stopped state, false otherwise.

.. cpp:function:: void SFXSource::onParameterValueChange(SFXParameter parameter)

	Called when a parameter attached to the source changes value. This callback will be triggered before the value change has actually been applied to the source.

	:param parameter: The parameter that has changed value.

.. cpp:function:: void SFXSource::onStatusChange(SFXStatus newStatus)

	Called when the playback status of the source changes.

	:param newStatus: The new playback status.

.. cpp:function:: void SFXSource::pause(float fadeOutTime)

	Pause playback of the source.

	:param fadeOutTime: Seconds for the sound to fade down to zero volume. If -1, the SFXDescription::fadeOutTime set in the source's associated description is used. Pass 0 to disable a fade-out effect that may be configured on the description. Be aware that if a fade-out effect is used, the source will not immediately to paused state but will rather remain in playing state until the fade-out time has expired..

.. cpp:function:: void SFXSource::removeParameter(SFXParameter parameter)

	Detach parameter from the source. Once detached, the source will no longer react to value changes of the given parameter . If the parameter is not attached to the source, the method will do nothing.

	:param parameter: The parameter to detach from the source.

.. cpp:function:: void SFXSource::setCone(float innerAngle, float outerAngle, float outsideVolume)

	Set up the 3D volume cone for the source.

	:param innerAngle: Angle of the inner sound cone in degrees (SFXDescription::coneInsideAngle). Must be 0<=innerAngle<=360.
	:param outerAngle: Angle of the outer sound cone in degrees (SFXDescription::coneOutsideAngle). Must be 0<=outerAngle<=360.
	:param outsideVolume: Volume scale factor outside of outer cone (SFXDescription::coneOutsideVolume). Must be 0<=outsideVolume<=1.

.. cpp:function:: void SFXSource::setFadeTimes(float fadeInTime, float fadeOutTime)

	Set the fade time parameters of the source. Volume Fades

	:param fadeInTime: The new fade-in time in seconds.
	:param fadeOutTime: The new fade-out time in seconds.

.. cpp:function:: void SFXSource::setPitch(float pitch)

	Set the pitch scale of the source. Pitch determines the playback speed of the source (default: 1).

	:param pitch: The new pitch scale factor.

.. cpp:function:: void SFXSource::setTransform(Point3F position, Point3F direction)

	Start playback of the source. Set the position and orientation of the source's 3D sound. Set the position of the source's 3D sound. If the sound data for the source has not yet been fully loaded, there will be a delay after calling play and playback will start after the data has become available.

	:param position: The new position in world space.
	:param direction: The forward vector.
	:param position: The new position in world space.
	:param fadeInTime: Seconds for the sound to reach full volume. If -1, the SFXDescription::fadeInTime set in the source's associated description is used. Pass 0 to disable a fade-in effect that may be configured on the description.

.. cpp:function:: void SFXSource::setVolume(float volume)

	Set the base volume level for the source. This volume will be the starting point for source group volume modulation, fades, and distance-based volume attenuation. Volume Attenuation

	:param volume: The new base volume level for the source. Must be 0>=volume<=1.

.. cpp:function:: void SFXSource::stop(float fadeOutTime)

	Stop playback of the source.

	:param fadeOutTime: Seconds for the sound to fade down to zero volume. If -1, the SFXDescription::fadeOutTime set in the source's associated description is used. Pass 0 to disable a fade-out effect that may be configured on the description. Be aware that if a fade-out effect is used, the source will not immediately transtion to stopped state but will rather remain in playing state until the fade-out time has expired.

Fields
------

.. cpp:member:: SFXDescription SFXSource::description

	The playback configuration that determines the initial sound properties and setup. Any SFXSource must have an associated SFXDescription .

.. cpp:member:: string  SFXSource::statusCallback

	Name of function to call when the status of the source changes. The source that had its status changed is passed as the first argument to the function and the new status of the source is passed as the second argument.
