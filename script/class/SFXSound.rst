SFXSound
========

A sound controller that directly plays a single sound file.

Inherit:
	:doc:`SFXSource`

Description
-----------

When playing individual audio files, SFXSounds are implicitly created by the sound system.

Each sound source has an associated play cursor that can be queried and explicitly positioned by the user. The cursor is a floating-point value measured in seconds.

For streamed sources, playback may not be continuous in case the streaming queue is interrupted.

Sounds and Voices
~~~~~~~~~~~~~~~~~

To actually emit an audible signal, a sound must allocate a resource on the sound device through which the sound data is being played back. This resource is called 'voice'.

As with other types of resources, the availability of these resources may be restricted, i.e. a given sound device will usually only support a fixed number of voices that are playing at the same time. Since, however, there may be arbitrary many SFXSounds instantiated and playing at the same time, this needs to be solved.

Methods
-------

.. cpp:function:: float SFXSound::getDuration()

	Get the total play time (in seconds) of the sound data attached to the sound.

	:return: Returns:

.. cpp:function:: float SFXSound::getPosition()

	Get the current playback position in seconds.

	:return: The current play cursor offset. 

.. cpp:function:: bool SFXSound::isReady()

	Test whether the sound data associated with the sound has been fully loaded and is ready for playback. For streamed sounds, this will be false during playback when the stream queue for the sound is starved and waiting for data. For buffered sounds, only an initial loading phase will potentially cause isReady to return false.

	:return: True if the sound is ready for playback. 

.. cpp:function:: void SFXSound::setPosition(float position)

	Set the current playback position in seconds. If the source is currently playing, playback will jump to the new position. If playback is stopped or paused, playback will resume at the given position when play() is called.

	:param position: The new position of the play cursor (in seconds).
