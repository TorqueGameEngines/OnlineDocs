GuiTheoraCtrl
=============

A control to playing Theora videos.

Inherit:
	:doc:`GuiControl`

Description
-----------

This control can be used to play videos in the Theora video format. The videos may include audio in Vorbis format. The codecs for both formats are integrated with the engine and no codecs must be present on the user's machine.

Example::

	%video = newGuiTheoraCtrl()
	{
	   theoraFile = "videos/intro.ogv";
	   playOnWake = false;
	   stopOnSleep = true;
	}
	
	Canvas.setContent( %video );
	%video.play();

Methods
-------

.. cpp:function:: float GuiTheoraCtrl::getCurrentTime()

	Get the current playback time.

	:return: The elapsed playback time in seconds. 

.. cpp:function:: bool GuiTheoraCtrl::isPlaybackDone()

	Test whether the video has finished playing.

	:return: True if the video has finished playing, false otherwise. 

.. cpp:function:: void GuiTheoraCtrl::pause()

	Pause playback of the video. If the video is not currently playing, the call is ignored. While stopped, the control displays the last frame.

.. cpp:function:: void GuiTheoraCtrl::play()

	Start playing the video. If the video is already playing, the call is ignored.

.. cpp:function:: void GuiTheoraCtrl::setFile(string filename)

	Set the video file to play. If a video is already playing, playback is stopped and the new video file is loaded.

	:param filename: The video file to load.

.. cpp:function:: void GuiTheoraCtrl::stop()

	Stop playback of the video. The next call to play() will then start playback from the beginning of the video. While stopped, the control renders empty with just the background color.

Fields
------

.. cpp:member:: ColorI  GuiTheoraCtrl::backgroundColor

	Fill color when video is not playing.

.. cpp:member:: bool  GuiTheoraCtrl::matchVideoSize

	Whether to automatically match control extents to the video size.

.. cpp:member:: bool  GuiTheoraCtrl::playOnWake

	Whether to start playing video when control is woken up.

.. cpp:member:: bool  GuiTheoraCtrl::renderDebugInfo

	If true, displays an overlay on top of the video with useful debugging information.

.. cpp:member:: bool  GuiTheoraCtrl::stopOnSleep

	Whether to stop video when control is set to sleep. If this is not set to true, the video will be paused when the control is put to sleep. This is because there is no support for seeking in the video stream in the player backend and letting the time source used to synchronize video (either audio or a raw timer) get far ahead of frame decoding will cause possibly very long delays when the control is woken up again.

.. cpp:member:: filename  GuiTheoraCtrl::theoraFile

	Theora video file to play.

.. cpp:member:: GuiTheoraTranscoder GuiTheoraCtrl::transcoder

	The routine to use for Y'CbCr to RGB conversion.
