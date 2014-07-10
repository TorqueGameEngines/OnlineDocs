TheoraTextureObject
===================

Definition of a named texture target playing a Theora video.

Inherit:
	:doc:`SimObject`

Description
-----------

TheoraTextureObject defines a named texture target that may play back a Theora video. This texture target can, for example, be used by materials to texture objects with videos.

Example::

	// The object that provides the video texture and controls its playback.
	singleton TheoraTextureObject( TheVideo )
	{
	   // Unique name for the texture target for referencing in materials.
	   texTargetName = "video";
	
	   // Path to the video file.
	   theoraFile = "./MyVideo.ogv";
	};
	
	// Material that uses the video texture.
	singleton Material( TheVideoMaterial )
	{
	   // This has to reference the named texture target defined by the
	   // TheoraTextureObjects texTargetName property.  Prefix with # to
	   // identify as texture target reference.
	   diffuseMap[ 0 ] = "#video";
	};

Methods
-------

.. cpp:function:: void TheoraTextureObject::pause()

	Pause playback of the video.

.. cpp:function:: void TheoraTextureObject::play()

	Start playback of the video.

.. cpp:function:: void TheoraTextureObject::stop()

	Stop playback of the video.

Fields
------

.. cpp:member:: bool  TheoraTextureObject::loop

	Should the video loop.

.. cpp:member:: SFXDescription TheoraTextureObject::SFXDescription

	Sound description to use for the video's audio channel. If not set, will use a default one.

.. cpp:member:: string  TheoraTextureObject::texTargetName

	Name of the texture target by which the texture can be referenced in materials.

.. cpp:member:: filename  TheoraTextureObject::theoraFile

	Theora video file to play.
