ParticleEmitterNode
===================

A particle emitter object that can be positioned in the world and dynamically enabled or disabled.

Inherit:
	:doc:`GameBase`

Description
-----------

A particle emitter object that can be positioned in the world and dynamically enabled or disabled.

Example::

	datablock ParticleEmitterNodeData( SimpleEmitterNodeData )
	{
	   timeMultiple = 1.0;
	};
	
	%emitter = newParticleEmitterNode()
	{
	   datablock = SimpleEmitterNodeData;
	   active = true;
	   emitter = FireEmitterData;
	   velocity = 3.5;
	};
	
	// Dynamically change emitter datablock
	%emitter.setEmitterDataBlock( DustEmitterData );


Methods
-------


.. cpp:function:: void ParticleEmitterNode::setActive(bool active)

	Turns the emitter on or off.

	:param active: New emitter state

.. cpp:function:: void ParticleEmitterNode::setEmitterDataBlock(ParticleEmitterData emitterDatablock)

	Assigns the datablock for this emitter node.

	:param emitterDatablock: ParticleEmitterData datablock to assign

	Example::

		// Assign a new emitter datablock
		%emitter.setEmitterDatablock( %emitterDatablock );

Fields
------


.. cpp:member:: bool  ParticleEmitterNode::active

	Controls whether particles are emitted from this node.

.. cpp:member:: ParticleEmitterData ParticleEmitterNode::emitter

	Datablock to use when emitting particles.

.. cpp:member:: float  ParticleEmitterNode::velocity

	Velocity to use when emitting particles (in the direction of the ParticleEmitterNode object's up (Z) axis).
