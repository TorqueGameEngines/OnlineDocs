Item
====

datablock for common properties.

Inherit:
	:doc:`ShapeBase`

Description
-----------

Base Item class. Uses the ItemData datablock for common properties.

Items represent an object in the world, usually one that the player will interact with. One example is a health kit on the group that is automatically picked up when the player comes into contact with it.

Example::

	// This is the "health patch" dropped by a dying player.
	datablock ItemData(HealthKitPatch)
	{
	   // Mission editor category, this datablock will show up in the// specified category under the "shapes" root category.
	   category = "Health";
	
	   className = "HealthPatch";
	
	   // Basic Item properties
	   shapeFile = "art/shapes/items/patch/healthpatch.dts";
	   mass = 2;
	   friction = 1;
	   elasticity = 0.3;
	   emap = true;
	
	   // Dynamic properties used by the scripts
	   pickupName = "a health patch";
	   repairAmount = 50;
	};
	
	%obj = newItem()
	{
	   dataBlock = HealthKitSmall;
	   parentGroup = EWCreatorWindow.objectGroup;
	   static = true;
	   rotate = true;
	};


Methods
-------


.. cpp:function:: string Item::getLastStickyNormal()

	Get the normal of the surface on which the object is stuck.

	:return:  is stuck. 

	Example::

		// Acquire the position where this Item is currently stuck
		%stuckPosition = %item.getLastStickPos();

.. cpp:function:: string Item::getLastStickyPos()

	Get the position on the surface on which this Item is stuck.

	:return:  is stuck. 

	Example::

		// Acquire the position where this Item is currently stuck
		%stuckPosition = %item.getLastStickPos();

.. cpp:function:: bool Item::isAtRest()

	Is the object at rest (ie, no longer moving)?

	:return: True if the object is at rest, false if it is not. 

	Example::

		// Query the item on if it is or is not at rest.
		%isAtRest = %item.isAtRest();

.. cpp:function:: bool Item::isRotating()

	Is the object still rotating?

	:return: True if the object is still rotating, false if it is not. 

	Example::

		// Query the item on if it is or is not rotating.
		%isRotating = %itemData.isRotating();

.. cpp:function:: bool Item::isStatic()

	Is the object static (ie, non-movable)?

	:return: True if the object is static, false if it is not. 

	Example::

		// Query the item on if it is or is not static.
		%isStatic = %itemData.isStatic();

.. cpp:function:: void Item::onEnterLiquid(string objID, string waterCoverage, string liquidType)

	Informs an Item object that it has entered liquid, along with information about the liquid type.

	:param objID: Object ID for this Item object.
	:param waterCoverage: How much coverage of water this Item object has.
	:param liquidType: The type of liquid that this Item object has entered.

.. cpp:function:: void Item::onLeaveLiquid(string objID, string liquidType)

	Informs an Item object that it has left a liquid, along with information about the liquid type.

	:param objID: Object ID for this Item object.
	:param liquidType: The type of liquid that this Item object has left.

.. cpp:function:: void Item::onStickyCollision(string objID)

	Informs the Item object that it is now sticking to another object. This callback is only called if the ItemData::sticky property for this Item is true.

	:param objID: Object ID this Item object.

.. cpp:function:: bool Item::setCollisionTimeout(int ignoreColObj)

	Temporarily disable collisions against a specific ShapeBase object. This is useful to prevent a player from immediately picking up an Item they have just thrown. Only one object may be on the timeout list at a time. The timeout is defined as 15 ticks.

	:param objectID: ShapeBase object ID to disable collisions against.

	:return:  object requested could be found, false if it could not. 

	Example::

		// Set the ShapeBase Object ID to disable collisions against
		%ignoreColObj = %player.getID();
		
		// Inform this Item object to ignore collisions temproarily against the %ignoreColObj.
		%item.setCollisionTimeout(%ignoreColObj);

Fields
------


.. cpp:member:: int  Item::maxWarpTicks  [static]

	When a warp needs to occur due to the client being too far off from the server, this is the maximum number of ticks we'll allow the client to warp to catch up.

.. cpp:member:: float  Item::minWarpTicks  [static]

	Fraction of tick at which instant warp occures on the client.

.. cpp:member:: bool  Item::rotate

	If true, the object will automatically rotate around its Z axis.

.. cpp:member:: bool  Item::static

	If true, the object is not moving in the world.
