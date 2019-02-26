Internals
**********

SFXBuffer
===========
Objects of this class hold sound data on the sound device. Buffers will be deleted when no longer used but will also be freed when the device is destroyed. Use StrongWeakRefPtrs to permanently refer to SFXBuffers so that references will null out when the buffer goes away.

Loading and updating of sound buffers happens on dedicated SFX update threads created by the individual devices. For devices that do not create such a thread, updating will happen on the main thread; this, however, is currently only used by the Null device.

Buffers hold raw, uncompressed PCM sample data loaded from SFXStreams. SFXBuffers for normal, buffered playback will be loaded once in entirety and may then be used by an arbitrary number of SFXVoices for concurrent playback.

SFXBuffers for streamed playback will be loaded progressively in the background and are tied to a single unique SFXVoice.

**Important:** Do not use delete directly on an SFXBuffer. Instead call **destroySelf()** on the buffer to delete it. Buffers may have pending asynchronous operations that need to flush out first before the buffer can actually be deleted. 

SFXVoice
==========
This is an abstract base class for objects on the sound device that the control playback of a particular SFXBuffer. Usually, a device will limit the number of concurrent sound playbacks it supports. SFXVoices follow the same lifecycle as SFXBuffers. An SFXVoice should never be directly deleted by clients. Leave lifetime management to reference-counting.

An SFXVoice promoted to playing state when its attached SFXBuffer has not yet fully loaded will temporarily transition into SFXStatusBlocked to indicate that playback can't progress. This will also happen for streamed sounds when the playback cursor is outrunning the stream feed. 

SFXStream
==========
Abstract base class for reading raw PCM sample streams. Instances of subclasses will be used for all sound loading that goes through SFX's own loading system (in contrast to sound loading happening directly through the sound API in use). Both buffered and streamed sounds are loaded through SFXStreams.

SFXStreams are used concurrently from multiple threads and are concurrently reference-counted to ensure proper and safe reclamation. For an SFXStream to support seeking in combination with streamed playback, it must implement cloning through the clone() method.

Streamed playback that also loops will require the attached SFXStream to properly reset().

SFXFileStream
===============
This is the abstract base class for specific file format loaders.

SFXResource
============
Thin wrapper that represents as sound file on disk. Performs a header read on the file to detect SFXFormat characteristics. Does not keep actual sound data. 

SFXDevice
==========
Abstract base class for SFX implementations against particular sound APIs. Manages SFXVoices and SFXBuffers as the primary sound device resources. The lifetimes of all sound resources are bound to their respective SFXDevice. Only one SFXDevice will ever be instanced at any one point.

SFXProvider
=============
Abstract base class for objects that manage device creation on particular sound APIs. There is one SFXProvider per supported sound API. SFXProviders have no responsibilities besides enumerating, querying, and creating SFXDevices

SFXSystem
===========
Singleton class that defines the central hub for the sound system. Exposes the high-level interface of the system. Manages SFXSources and the current SFXDevice instance. Exposes global SFX parameters.

SFXSystem::_update() is called from the main game loop to periodically update the SFXSources in the system. Play-once source that have stopped playing will purged in the process. Sound loading, however, is usually handled on a dedicated thread rather than on the main thread. 

Conclusion
===========
You typically will not be working directly with the SFX internals, unless you are heavily extending the SFX system. This guide was meant to show you the major internal classes that drive the SFX system. Continue reading to learn about common tips, troubleshooting, and the conclusion of the SFX system documentation.
