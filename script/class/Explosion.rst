Explosion
=========

object.

Inherit:
	:doc:`GameBase`

Description
-----------

The emitter for an explosion effect, with properties defined by a ExplosionData object.

The object will initiate the explosion effects automatically after being added to the simulation.

Example::

	datablock ExplosionData( GrenadeSubExplosion )
	{
	   offset = 0.25;
	   emitter[0] = GrenadeExpSparkEmitter;
	
	   lightStartRadius = 4.0;
	   lightEndRadius = 0.0;
	   lightStartColor = "0.9 0.7 0.7";
	   lightEndColor = "0.9 0.7 0.7";
	   lightStartBrightness = 2.0;
	   lightEndBrightness = 0.0;
	};
	
	datablock ExplosionData( GrenadeLauncherExplosion )
	{
	   soundProfile = GrenadeLauncherExplosionSound;
	   lifeTimeMS = 400; // Quick flash, short burn, and moderate dispersal// Volume particles
	   particleEmitter = GrenadeExpFireEmitter;
	   particleDensity = 75;
	   particleRadius = 2.25;
	
	   // Point emission
	   emitter[0] = GrenadeExpDustEmitter;
	   emitter[1] = GrenadeExpSparksEmitter;
	   emitter[2] = GrenadeExpSmokeEmitter;
	
	   // Sub explosion objects
	   subExplosion[0] = GrenadeSubExplosion;
	
	   // Camera Shaking
	   shakeCamera = true;
	   camShakeFreq = "10.0 11.0 9.0";
	   camShakeAmp = "15.0 15.0 15.0";
	   camShakeDuration = 1.5;
	   camShakeRadius = 20;
	
	   // Exploding debris
	   debris = GrenadeDebris;
	   debrisThetaMin = 10;
	   debrisThetaMax = 60;
	   debrisNum = 4;
	   debrisNumVariance = 2;
	   debrisVelocity = 25;
	   debrisVelocityVariance = 5;
	
	   lightStartRadius = 4.0;
	   lightEndRadius = 0.0;
	   lightStartColor = "1.0 1.0 1.0";
	   lightEndColor = "1.0 1.0 1.0";
	   lightStartBrightness = 4.0;
	   lightEndBrightness = 0.0;
	   lightNormalOffset = 2.0;
	};
	
	function createExplosion()
	{
	   // Create a new explosion - it will explode automatically
	   %pos = "0 0 100";
	   %obj = newExplosion()
	   {
	      position = %pos;
	      dataBlock = GrenadeLauncherExplosion;
	   };
	}
	
	// schedule an explosionschedule(1000, 0, createExplosion);

