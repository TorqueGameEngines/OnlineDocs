PxMultiActorData
================

Defines the properties of a type of PxMultiActor.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Usually it is prefered to use PhysicsShape rather than PxMultiActor because a PhysicsShape is not PhysX specific and can be much easier to setup.

For more information, refer to Nvidia's PhysX docs.

Fields
------

.. cpp:member:: float  PxMultiActorData::angularDrag

	Value used to help calculate rotational drag force while submerged in water.

.. cpp:member:: float  PxMultiActorData::breakForce

	Force required to break an actor. This value does not apply to joints. If an actor is associated with a joint it will break whenever the joint does. This allows an actor "not" associated with a joint to also be breakable.

.. cpp:member:: float  PxMultiActorData::buoyancyDensity

	The density used to calculate buoyant forces. The result of the calculated buoyancy is relative to the density of the WaterObject the PxMultiActor is within.

.. cpp:member:: bool  PxMultiActorData::clientOnly


.. cpp:member:: void  PxMultiActorData::dumpModel

	Dumps model hierarchy and details to a file. The file will be created as 'model.dump' in the game folder. If model.dump already exists, it will be overwritten.

.. cpp:member:: float  PxMultiActorData::linearDrag

	Value used to help calculate linear drag force while submerged in water.

.. cpp:member:: PxMaterial PxMultiActorData::Material

	An optional PxMaterial to be used for the PxMultiActor . Defines properties such as friction and restitution. Unrelated to the material used for rendering. The physXStream will contain defined materials that can be customized in 3DS Max. To override the material for all physics shapes in the physXStream, specify a material here.

.. cpp:member:: bool  PxMultiActorData::noCorrection


.. cpp:member:: filename  PxMultiActorData::physXStream

	.XML file containing data such as actors, shapes, and joints. These files can be created using a free PhysX plugin for 3DS Max.

.. cpp:member:: void  PxMultiActorData::reload

	Reloads all data used for the PxMultiActorData . If the reload sucessfully completes, all PxMultiActor's will be notified.

.. cpp:member:: filename  PxMultiActorData::shapeName

	Path to the .DAE or .DTS file to render.

.. cpp:member:: bool  PxMultiActorData::singlePlayerOnly


.. cpp:member:: string PxMultiActorData::string


.. cpp:member:: float  PxMultiActorData::waterDragScale

	Scale to apply to linear and angular dampening while submerged in water.
