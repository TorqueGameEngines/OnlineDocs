ParticleEmitter
===============

This object is responsible for spawning particles.

Inherit:
	:doc:`GameBase`

Description
-----------

This object is responsible for spawning particles.

This class is the main interface for creating particles - though it is usually only accessed from within another object like ParticleEmitterNode or WheeledVehicle. If using this object class (via C++) directly, be aware that it does not track changes in source axis or velocity over the course of a single update, so emitParticles should be called at a fairly fine grain. The emitter will potentially track the last particle to be created into the next call to this function in order to create a uniformly random time distribution of the particles.

If the object to which the emitter is attached is in motion, it should try to ensure that for call (n+1) to this function, start is equal to the end from call (n). This will ensure a uniform spatial distribution.

