ProjectileData
==============

Stores properties for an individual projectile type.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Stores properties for an individual projectile type.

Example::

	datablock ProjectileData(GrenadeLauncherProjectile)
	{
	 projectileShapeName = "art/shapes/weapons/SwarmGun/rocket.dts";
	directDamage = 30;
	radiusDamage = 30;
	damageRadius = 5;
	areaImpulse = 2000;
	explosion = GrenadeLauncherExplosion;
	waterExplosion = GrenadeLauncherWaterExplosion;
	decal = ScorchRXDecal;
	splash = GrenadeSplash;
	particleEmitter = GrenadeProjSmokeTrailEmitter;
	particleWaterEmitter = GrenadeTrailWaterEmitter;
	muzzleVelocity = 30;
	velInheritFactor = 0.3;
	armingDelay = 2000;
	lifetime = 10000;
	fadeDelay = 4500;
	bounceElasticity = 0.4;
	bounceFriction = 0.3;
	isBallistic = true;
	gravityMod = 0.9;
	lightDesc = GrenadeLauncherLightDesc;
	damageType = "GrenadeDamage";
	};


Methods
-------


.. cpp:function:: void ProjectileData::onCollision(Projectile proj, SceneObject col, float fade, Point3F pos, Point3F normal)

	Called when a projectile collides with another object. This function is only called on server objects.

	:param proj: The projectile colliding with SceneObject col.
	:param col: The SceneObject hit by the projectile.
	:param fade: The current fadeValue of the projectile, affects its visibility.
	:param pos: The position of the collision.
	:param normal: The normal of the collision.

.. cpp:function:: void ProjectileData::onExplode(Projectile proj, Point3F pos, float fade)

	Called when a projectile explodes. This function is only called on server objects.

	:param proj: The exploding projectile.
	:param pos: The position of the explosion.
	:param fade: The current fadeValue of the projectile, affects its visibility.

Fields
------


.. cpp:member:: int  ProjectileData::armingDelay

	Amount of time, in milliseconds, before the projectile will cause damage or explode on impact. This value must be equal to or less than the projectile's lifetime.

.. cpp:member:: float  ProjectileData::bounceElasticity

	Influences post-bounce velocity of a projectile that does not explode on contact. Scales the velocity from a bounce after friction is taken into account. A value of 1.0 will leave it's velocity unchanged while values greater than 1.0 will increase it.

.. cpp:member:: float  ProjectileData::bounceFriction

	Factor to reduce post-bounce velocity of a projectile that does not explode on contact. Reduces bounce velocity by this factor and a multiple of the tangent to impact. Used to simulate surface friction.

.. cpp:member:: DecalData ProjectileData::decal

	Decal datablock used for decals placed at projectile explosion points.

.. cpp:member:: ExplosionData ProjectileData::Explosion

	Explosion datablock used when the projectile explodes outside of water.

.. cpp:member:: int  ProjectileData::fadeDelay

	Amount of time, in milliseconds, before the projectile begins to fade out. This value must be smaller than the projectile's lifetime to have an affect.

.. cpp:member:: float  ProjectileData::gravityMod

	Scales the influence of gravity on the projectile. The larger this value is, the more that gravity will affect the projectile. A value of 1.0 will assume "normal" influence upon it. The magnitude of gravity is assumed to be 9.81 m/s/s

.. cpp:member:: float  ProjectileData::impactForce


.. cpp:member:: bool  ProjectileData::isBallistic

	Detetmines if the projectile should be affected by gravity and whether or not it bounces before exploding.

.. cpp:member:: int  ProjectileData::lifetime

	Amount of time, in milliseconds, before the projectile is removed from the simulation. Used with fadeDelay to determine the transparency of the projectile at a given time. A projectile may exist up to a maximum of 131040ms (or 4095 ticks) as defined by Projectile::MaxLivingTicks in the source code.

.. cpp:member:: LightDescription ProjectileData::lightDesc

	LightDescription datablock used for lights attached to the projectile.

.. cpp:member:: float  ProjectileData::muzzleVelocity

	Amount of velocity the projectile recieves from the "muzzle" of the gun. Used with velInheritFactor to determine the initial velocity of the projectile. This value is never modified by the engine.

.. cpp:member:: ParticleEmitterData ProjectileData::ParticleEmitter

	Particle emitter datablock used to generate particles while the projectile is outside of water.

.. cpp:member:: ParticleEmitterData ProjectileData::particleWaterEmitter

	Particle emitter datablock used to generate particles while the projectile is submerged in water.

.. cpp:member:: filename  ProjectileData::projectileShapeName

	File path to the model of the projectile.

.. cpp:member:: Point3F  ProjectileData::scale

	Scale to apply to the projectile's size.

.. cpp:member:: SFXTrack ProjectileData::sound

	SFXTrack datablock used to play sounds while in flight.

.. cpp:member:: SplashData ProjectileData::Splash

	Splash datablock used to create splash effects as the projectile enters or leaves water.

.. cpp:member:: float  ProjectileData::velInheritFactor

	Amount of velocity the projectile recieves from the source that created it. Use an amount between 0 and 1 for the best effect. This value is never modified by the engine.

.. cpp:member:: ExplosionData ProjectileData::waterExplosion

	Explosion datablock used when the projectile explodes underwater.
