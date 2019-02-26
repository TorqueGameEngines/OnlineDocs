Projectiles
************

Introduction
=============

This article will discuss the technical aspect of creating custom projectiles for use with custom weapons in your games.

Projectiles
============

Projectiles are what we use in T3D for most bullets, rockets, grenades, and all objects of the like. Typically a projectile is created in the ``WeaponImage::OnFire`` call like so::

    // Create the projectile object
    %p = new (%this.projectileType)
    {
        dataBlock = %this.projectile;
        initialVelocity = %muzzleVelocity;
        initialPosition = %obj.getMuzzlePoint(%slot);
        sourceObject = %obj;
        sourceSlot = %slot;
        client = %obj.client;
    };
    MissionCleanup.add(%p); // MissionCleanup is a SimGroup.

Once created, a projectile will move from it's initialPosition in the direction of it's initial velocity. It will travel along this path until it comes in contact with a sceneObject. (This includes the terrain.) where it will either bounce, or explode depending on how the projectile's datablock has been setup. Before the projectile actually explodes, it uses it's onExplode callback in script before actualling the explode() code in C++. This gives scriptors a chance to affect the behavior of the projectile before the engine actually processes an explosion, or to do any last minute tricks, hacks, or checks before it explodes. It's important to keep in mind that the onExplode callback will only be done server side.

While there are many fields and properties to a Projectile's datablock, there are a couple to keep in mind, and have a firm understanding of. (Those closely related will be grouped together.)

======================================  ===================================================================================  
Important Projectile Datablock Fields
======================================  ===================================================================================  
projectileShapeName                     Path to the shape to be used for the projectile
explosion                               Explosion effect to play at the point of the explosion
decal                                   Decal to leave on walls/terrain/objects when it explodes
particleEmitter                         An effect for the trail as the projectile lies through the air
armingDelay                             amount of time (In milliseconds) before a projectile is allowed to explode
lifeTime                                amount of time (in milliseconds) before a projectile deletes itself from the scene
======================================  ===================================================================================

.. note:: One thing I've noticed is that somewhere down the line in projectiles, we've relied heavily on the use of dynamic fields to handle things in script that would be assumed to be taken care of by the engine. For example, directDamage is in our example datablock, but really is only a dynamic field used later for players hit directly with a rocket.

Most of the processing of a projectile is done from the script side of things. The engine side of things really only updates it's position, calls it's callbacks, networking, exploding when the time is right, etc. Things like damage and pushback must be handled from various callbacks in script.

From a script side of things, when a projectile has been created, the next thing you'll have to do is deal with it's script callback. Depending on the behavior of the projectile, you will be looking to work with onCollision (For ballistic-type weapons), or onExplode (For grenade-type weapons).

At the very least, we want to call some kind of damage() function that will decrement the player's health and update their GUI. In the event of a grenade or rocket, we want to damage the player it hit and likely anything around it. The easiest way to do this is by using a ContainerRadiusSearch, passing in the position of the explosion, the radius of the explosion (usually set as a dynamic field on the projectile's datablock), and $TypeMasks::ShapeBaseObjectType or $TypeMasks::PlayerObjectType. We can do some math on every object the container search returns to determine if we should just outright damage the player, or scale the damage and impulse effects based on their distance from the center of the explosion. (It doesn't make much sense to take full damage when you are on the very edge of an explosion, does it?). You should also make use of calcExplosionCoverage during the container call to make sure that objects aren't damaged if they are covered by walls, or other objects. Distance scale can be calculated as::

    scale = (distanceFromExplosion < explosionRadius / 2)? 1.0 : 1.0 
        - ((distanceFromExplosion � explosionRadius / 2) / explosionRadius / 2);

Conclusion
=============
Having Torque 3D's camera system exposed to script gives you a great deal of power and flexibility in your game. When you have tested the various modes, you can begin to see how this will affect game play