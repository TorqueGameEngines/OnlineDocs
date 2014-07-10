ParticleData
============

Contains information for how specific particles should look and react including particle colors, particle imagemap, acceleration value for individual particles and spin information.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Contains information for how specific particles should look and react including particle colors, particle imagemap, acceleration value for individual particles and spin information.

Example::

	datablock ParticleData( GLWaterExpSmoke )
	{
	   textureName = "art/shapes/particles/smoke";
	   dragCoefficient = 0.4;
	   gravityCoefficient = -0.25;
	   inheritedVelFactor = 0.025;
	   constantAcceleration = -1.1;
	   lifetimeMS = 1250;
	   lifetimeVarianceMS = 0;
	   useInvAlpha = false;
	   spinSpeed = 1;
	   spinRandomMin = -200.0;
	   spinRandomMax = 200.0;
	
	   colors[0] = "0.1 0.1 1.0 1.0";
	   colors[1] = "0.4 0.4 1.0 1.0";
	   colors[2] = "0.4 0.4 1.0 0.0";
	
	   sizes[0] = 2.0;
	   sizes[1] = 6.0;
	   sizes[2] = 2.0;
	
	   times[0] = 0.0;
	   times[1] = 0.5;
	   times[2] = 1.0;
	};


Methods
-------


.. cpp:function:: void ParticleData::reload()

	Reloads this particle.

	Example::

		// Get the editors current particle
		%particle = PE_ParticleEditor.currParticle
		
		// Change a particle value
		%particle.setFieldValue( %propertyField, %value );
		
		// Reload it
		%particle.reload();

Fields
------


.. cpp:member:: bool  ParticleData::animateTexture

	If true, allow the particle texture to be an animated sprite.

.. cpp:member:: string  ParticleData::animTexFrames

	A list of frames and/or frame ranges to use for particle animation if animateTexture is true. Each frame token must be separated by whitespace. A frame token must be a positive integer frame number or a range of frame numbers separated with a '-'. The range separator, '-', cannot have any whitspace around it. Ranges can be specified to move through the frames in reverse as well as forward (eg. 19-14). Frame numbers exceeding the number of tiles will wrap.

	Example::

		animTexFrames = "0-16 20 19 18 17 31-21";

.. cpp:member:: string  ParticleData::animTexName

	Texture file to use for this particle if animateTexture is true. Deprecated. Use textureName instead.

.. cpp:member:: Point2I  ParticleData::animTexTiling

	The number of frames, in rows and columns stored in textureName (when animateTexture is true). A maximum of 256 frames can be stored in a single texture when using animTexTiling. Value should be "NumColumns NumRows", for example "4 4".

.. cpp:member:: ColorF  ParticleData::colors [4]

	Particle RGBA color keyframe values. The particle color will linearly interpolate between the color/time keys over the lifetime of the particle.

.. cpp:member:: float  ParticleData::constantAcceleration

	Constant acceleration to apply to this particle.

.. cpp:member:: float  ParticleData::dragCoefficient

	Particle physics drag amount.

.. cpp:member:: int  ParticleData::framesPerSec

	If animateTexture is true, this defines the frames per second of the sprite animation.

.. cpp:member:: float  ParticleData::gravityCoefficient

	Strength of gravity on the particles.

.. cpp:member:: float  ParticleData::inheritedVelFactor

	Amount of emitter velocity to add to particle initial velocity.

.. cpp:member:: int  ParticleData::lifetimeMS

	Time in milliseconds before this particle is destroyed.

.. cpp:member:: int  ParticleData::lifetimeVarianceMS

	Variance in lifetime of particle, from 0 - lifetimeMS.

.. cpp:member:: float  ParticleData::sizes [4]

	Particle size keyframe values. The particle size will linearly interpolate between the size/time keys over the lifetime of the particle.

.. cpp:member:: float  ParticleData::spinRandomMax

	Maximum allowed spin speed of this particle, between spinRandomMin and 1000.

.. cpp:member:: float  ParticleData::spinRandomMin

	Minimum allowed spin speed of this particle, between -1000 and spinRandomMax.

.. cpp:member:: float  ParticleData::spinSpeed

	Speed at which to spin the particle.

.. cpp:member:: Point2F  ParticleData::textureCoords [4]

	4 element array defining the UV coords into textureName to use for this particle. Coords should be set for the first tile only when using animTexTiling; coordinates for other tiles will be calculated automatically. "0 0" is top left and "1 1" is bottom right.

.. cpp:member:: string  ParticleData::textureName

	Texture file to use for this particle.

.. cpp:member:: float  ParticleData::times [4]

	Time keys used with the colors and sizes keyframes. Values are from 0.0 (particle creation) to 1.0 (end of lifespace).

.. cpp:member:: bool  ParticleData::useInvAlpha

	Controls how particles blend with the scene. If true, particles blend like ParticleBlendStyle NORMAL, if false, blend like ParticleBlendStyle ADDITIVE.

.. cpp:member:: float  ParticleData::windCoefficient

	Strength of wind on the particles.
