Special Effects
===============

Classes responsible for special effect objects, such as Explosion, Debris, Particles, etc. 

Classes
-------

.. toctree::
	:maxdepth: 1
	
	class/Debris
	class/DebrisData
	class/DecalData
	class/DecalManager
	class/Explosion
	class/ExplosionData
	class/ForestWindEmitter
	class/LightAnimData
	class/Lightning
	class/LightningData
	class/LightningStrikeEvent
	class/ParticleData
	class/ParticleEmitter
	class/ParticleEmitterData
	class/ParticleEmitterNode
	class/ParticleEmitterNodeData
	class/Precipitation
	class/PrecipitationData
	class/Splash
	class/SplashData

Enumeration
-----------

.. cpp:member:: enum  ParticleBlendStyle

	The type of visual blending style to apply to the particles.

	:param NORMAL: No blending style.
	:param ADDITIVE: Adds the color of the pixel to the frame buffer with full alpha for each pixel.
	:param SUBTRACTIVE: Subtractive Blending. Reverses the color model, causing dark colors to have a stronger visual effect.
	:param PREMULTALPHA: Color blends with the colors of the imagemap rather than the alpha.

Functions
---------

.. cpp:function:: float calcExplosionCoverage(Point3F pos, int id, int covMask)

	Calculates how much an explosion effects a specific object. Use this to determine how much damage to apply to objects based on their distance from the explosion's center point, and whether the explosion is blocked by other objects.

	:param pos: Center position of the explosion.
	:param id: Id of the object of which to check coverage.
	:param covMask: Mask of object types that may block the explosion.

	:return: Coverage value from 0 (not affected by the explosion) to 1 (fully affected)

	Example::

		// Get the position of the explosion.
		%position = %explosion.getPosition();
		
		// Set a list of TypeMasks (defined in gameFunctioncs.cpp), seperated by the | character.
		%TypeMasks = $TypeMasks::StaticObjectType | $TypeMasks::ItemObjectType
		
		// Acquire the damage value from 0.0f - 1.0f.
		%coverage = calcExplosionCoverage( %position, %sceneObject, %TypeMasks );
		
		// Apply damage to object
		%sceneObject.applyDamage( %coverage * 20 );
