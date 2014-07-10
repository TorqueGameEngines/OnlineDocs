SFXController
=============

A sound source that drives multi-source playback.

Inherit:
	:doc:`SFXSource`

Description
-----------

This class acts as an interpreter for SFXPlayLists. It goes through the slots of the playlist it is attached to and performs the actions described by each of the slots in turn. As SFXControllers are created implicitly by the SFX system when instantiating a source for a play list it is in most cases not necessary to directly deal with the class. The following example demonstrates how a controller would commonly be created.

Example::

	// Create a play list from two SFXProfiles.
	%playList = newSFXPlayList()
	{
	   // Use a looped description so the list playback will loop.description = AudioMusicLoop2D;
	
	   track[ 0 ] = Profile1;
	   track[ 1 ] = Profile2;
	};
	
	// Play the list.  This will implicitly create a controller.sfxPlayOnce( %playList );

Methods
-------

.. cpp:function:: int SFXController::getCurrentSlot()

	Get the index of the playlist slot currently processed by the controller.

	:return: The slot index currently being played. 

.. cpp:function:: void SFXController::setCurrentSlot(int index)

	Set the index of the playlist slot to play by the controller. This can be used to seek in the playlist.

	:param index: Index of the playlist slot.

Fields
------

.. cpp:member:: bool  SFXController::trace

	If true, the controller logs its operation to the console. This is a non-networked field that will work locally only.
