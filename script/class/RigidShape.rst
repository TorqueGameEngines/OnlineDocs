RigidShape
==========

Implements rigid-body physics for DTS objects in the world.

Inherit:
	:doc:`ShapeBase`

Description
-----------

The RigidShape class implements rigid-body physics for DTS objects in the world.

"Rigid body physics" refers to a system whereby objects are assumed to have a finite size, equally distributed masses, and where deformations of the objects themselves are not accounted for. Uses the RigidShape class to control its physics.

Example::

   datablock RigidShapeData( BouncingBoulder )
   {
      category = "RigidShape";

      shapeFile = "~/data/shapes/boulder/boulder.dts";
      emap = true;

      // Rigid Body
      mass = 500;
      massCenter = "0 0 0";    // Center of mass for rigid body
      massBox = "0 0 0";         // Size of box used for moment of inertia,
                          // if zero it defaults to object bounding box
      drag = 0.2;                // Drag coefficient
      bodyFriction = 0.2;
      bodyRestitution = 0.1;
      minImpactSpeed = 5;        // Impacts over this invoke the script callback
      softImpactSpeed = 5;       // Play SoftImpact Sound
      hardImpactSpeed = 15;      // Play HardImpact Sound
      integration = 4;           // Physics integration: TickSec/Rate
      collisionTol = 0.1;        // Collision distance tolerance
      contactTol = 0.1;          // Contact velocity tolerance

      minRollSpeed = 10;

      maxDrag = 0.5;
      minDrag = 0.01;

      dustHeight = 10;

      dragForce = 0.05;
      vertFactor = 0.05;
   };

 	new RigidShape()
   {
      dataBlock = "BouncingBoulder";
      parentGroup = EWCreatorWindow.objectGroup;
   };

Methods
-------

.. cpp:function:: void RigidShape::forceClientTransform()

	Forces the client to jump to the RigidShape's transform rather then warp to it.

.. cpp:function:: void RigidShape::freezeSim(bool isFrozen)

	Enables or disables the physics simulation on the RigidShape object.

	:param isFrozen: Boolean frozen state to set the object.

	Example::

		// Define the frozen state.
		%isFrozen = "true";
		
		// Inform the object of the defined frozen state
		%thisRigidShape.freezeSim(%isFrozen);

.. cpp:function:: void RigidShape::onEnterLiquid(string objId, string waterCoverage, string liquidType)

	Called whenever this RigidShape object enters liquid.

	:param objId: The ID of the rigidShape object.
	:param waterCoverage: Amount of water coverage the RigidShape has.
	:param liquidType: Type of liquid that was entered.

	Example::

		// The RigidShape object falls in a body of liquid, causing the callback to occur.
		RigidShape::onEnterLiquid(%this,%objId,%waterCoverage,%liquidType)
		{
			// Code to run whenever this callback occurs.
		}

.. cpp:function:: void RigidShape::onLeaveLiquid(string objId, string liquidType)

	Called whenever the RigidShape object exits liquid.

	:param objId: The ID of the RigidShape object.
	:param liquidType: Type if liquid that was exited.

	Example::

		// The RigidShape object exits in a body of liquid, causing the callback to occur.
		RigidShape::onLeaveLiquid(%this,%objId,%liquidType)
		{
		  // Code to run whenever this callback occurs.
		}

.. cpp:function:: void RigidShape::reset()

	Clears physic forces from the shape and sets it at rest.

	Example::

		// Inform the RigidShape object to reset.
		%thisRigidShape.reset();
