Conclusion
************

How Do I...
===============

... convert to/from OGG?
--------------------------
For Windows, a neat little tool is oggdropXPd. It converts to and from OGG using various formats and has an interface as straightforward as it gets.

* http://www.rarewares.org/ogg-oggdropxpd.php
  
... see how the system is used. Is there an example I can look at?
--------------------------------------------------------------------
A simple example of how to use the system can be found in the form of the GuiMusicPlayer control found in **core/scripts/gui/guiMusicPlayer.cs**. 

... create 5.1 or 7.1 surround sound?
---------------------------------------
This is done by the mixer of the sound device you are using. This mixer will take all the active sound voice (2D and 3D) and mix their audio signals down into a number of output channels. In plain stereo playback, this will be two channels: a left one and a right one.

With surround systems, a corresponding number of output channels are fed by the mixer. Note, however, that in order to get surround effects in your game, you need to properly set up 3D sounds. 

... play background music?
----------------------------
One way is to place an SFXEmitter in your level and let it stream a 2D looping music track.Another way is to manually trigger playback directly from script. 

... tune stream buffering?
---------------------------
If you experience lag and interruptions with stream sources, set the streamPacketSize and streamReadAhead properties in SFXDescriptions such that more data is buffered in advanced. Be careful with streamPacketSize as it directly affects buffer metrics on the device as well as the time spend on each individual I/O operation.

To directly modify queue length on devices, adjust the following in the engine code::

	SFXInternal::SFXAsyncQueue::DEFAULT_STREAM_QUEUE_LENGTH

This will not affect streaming happening directly on the device (FMOD currently). 

... stream custom audio data?
-------------------------------
One way is to derive a class from SFXStream to use it to write the sample data to the audio buffers. SFXSystem::createSourceFromStream() can be used here to create an SFXSource from just a plain SFXStream and an SFXDescription.

Another way is to create and feed an SFXPacketStream which consumes raw, uncompressed sample data in discrete packets and writes them to the consumer audio buffer as needed. Use the same SFXSystem::createSourceFromStream() method to create an SFXSource to control playback. 

... add support for a new audio format?
-----------------------------------------
Derive a class from SFXFileStream and register your extension(s) through SFXFileStream::registerExtension() in SFXSystem::init(). Look at SFXWavStream and SFXOggStream for examples. 

... monitor the status of the SFX system?
-------------------------------------------
se the "sfx" metrics, for example, by typing 'metrics( "sfx" );' in the console. This display various live statistics for the SFX system. To see a detailed listing of all current SFXSources, use "sfxDumpSources". 

... play multiple sounds in random/sequential order on an SFXEmitter?
----------------------------------------------------------------------
Currently, this is not possible without custom scripting. The next revision of SFX will, however, include playlist support across all devices. 
  
Troubleshooting
=================
**I am hearing 3D sounds outside of their set maximum range. How can I fix this?**

You are probably using the logarithmic distance model. This is where sounds are not cut off at their maximum distance, but rather retain the attenuated volume that is greater than the specified max distance. To make sounds fade out in time, use proper settings for the min and max distance. Also, to speed up or slow down overall volume falloff with distance, increase or decrease the 3D rolloff factor.

**My sounds start with a delay. What is wrong?**

The delay is due to the sound taking a certain time to load. Generally, make sure that either sound data is available before starting playback or that a short delay is not relevant for a given sound.

**I'm seeing an error in the console.log that says "SFXFMODProvider - Could not locate the <fmod.dll>". What is wrong?**

This only means that the FMOD sound provider cannot find the FMOD DLL. If you do not want to use FMOD, then simply ignore this message. Otherwise, make sure to copy the FMOD DLL (fmodex.dll on Windows; fmodex.dylib on Mac) to the same folder as your game executable. This message should then disappear the next time you start Torque. 

To download FMOD, visit the FMOD homepage. To purchase a very friendly priced indie license of FMOD for your game, visit the Torque store.

#. http://www.fmod.org/
#. http://www.garagegames.com/products/fmod

**I'm seeing crashes with XAudio. What can I do?**
Head over to Torque 3D Private forum and post a bug report. Our SFX developer will be around to look into the issue.

#. http://www.garagegames.com/community/forums/63

Best Practices
================
**Preload or not?**

Anything that is used often should be preloaded. Rarely used sounds for which it is okay to start with a short delay need not be preloaded. Streamed sounds cannot be preloaded (create an SFXSource if you want to ready them before playing). 

**Lifetimes of SFXProfiles**

Scope the lifetimes of SFXProfiles to where they are actually used. Generally, don't put all of the sounds of your game together as one batch of SFXProfiles. Once its sound data has been loaded, an SFXProfile for non-streamed sounds will consume resources on the SFX device.

Ambient sounds, for example, that are not used in a particular level need not have their SFXProfiles loaded. However, sounds that are used in any level in the game are better loaded once at startup. For server-side profiles, use the datablock keyword whereas for client-side profiles, use new or singleton.

**Stream or not?**

Stream music/ambient sounds, don't stream effects. Generally WAVs over ~700kb and OGGs over 200k should be streamed.

Conclusion
============
This concludes the SFX documentation for Torque 3D. If you wish to learn more about the system, this is a good time to browse the demos provided with Torque 3D and see how they are used. Additionally, the system is very well commented in the engine code and will contain more detailed information on a per-line basis. 
