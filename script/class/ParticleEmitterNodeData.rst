ParticleEmitterNodeData
=======================

.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Contains additional data to be associated with a ParticleEmitterNode.


Fields
------


.. cpp:member:: float  ParticleEmitterNodeData::timeMultiple

	Time multiplier for particle emitter nodes. Increasing timeMultiple is like running the emitter at a faster rate - single-shot emitters will complete in a shorter time, and continuous emitters will generate particles more quickly. Valid range is 0.01 - 100.
