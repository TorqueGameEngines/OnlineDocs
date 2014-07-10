PxMultiActor
============

Represents a destructible physical object simulated using PhysX.

Inherit:
	:doc:`GameBase`

Description
-----------

Usually it is prefered to use PhysicsShape and not PxMultiActor because it is not PhysX specific and much easier to setup.

Methods
-------

.. cpp:function:: void PxMultiActor::listMeshes(enum Hidden, enum Shown, enum All)

	Lists all meshes of the provided type in the console window.

	:param All: Lists all of the PxMultiActor's meshes.
	:param Hidden: Lists all of the PxMultiActor's hidden meshes.
	:param Shown: Lists all of the PxMultiActor's visible meshes.

.. cpp:function:: void PxMultiActor::setAllHidden()

	Hides or unhides all meshes contained in the PxMultiActor . Hidden meshes will not be rendered.

.. cpp:function:: void PxMultiActor::setBroken()

	Sets the PxMultiActor to a broken or unbroken state.

.. cpp:function:: void PxMultiActor::setMeshHidden(string meshName, bool isHidden)

	Prevents the provided mesh from being rendered.

Fields
------

.. cpp:member:: bool  PxMultiActor::broken


.. cpp:member:: bool  PxMultiActor::debugRender

