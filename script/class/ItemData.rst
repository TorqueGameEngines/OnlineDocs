ItemData
========

type.

Inherit:
	:doc:`ShapeBaseData`

Description
-----------

Stores properties for an individual Item type.

Items represent an object in the world, usually one that the player will interact with. One example is a health kit on the group that is automatically picked up when the player comes into contact with it.

ItemData provides the common properties for a set of Items. These properties include a DTS or DAE model used to render the Item in the world, its physical properties for when the Item interacts with the world (such as being tossed by the player), and any lights that emit from the Item.

Example::

	datablock ItemData(HealthKitSmall)
	{
	   category ="Health";
	   className = "HealthPatch";
	   shapeFile = "art/shapes/items/kit/healthkit.dts";
	   gravityMod = "1.0";
	   mass = 2;
	   friction = 1;
	   elasticity = 0.3;
	   density = 2;
	   drag = 0.5;
	   maxVelocity = "10.0";
	   emap = true;
	   sticky = false;
	   dynamicType = "0"
	;   lightOnlyStatic = false;
	   lightType = "NoLight";
	   lightColor = "1.0 1.0 1.0 1.0";
	   lightTime = 1000;
	   lightRadius = 10.0;
	   simpleServerCollision = true;   // Dynamic properties used by the scripts
	
	   pickupName = "a small health kit";
	   repairAmount = 50;
	};


Fields
------


.. cpp:member:: float  ItemData::elasticity

	A floating-point value specifying how 'bouncy' this ItemData is.

.. cpp:member:: float  ItemData::friction

	A floating-point value specifying how much velocity is lost to impact and sliding friction.

.. cpp:member:: float  ItemData::gravityMod

	Floating point value to multiply the existing gravity with, just for this ItemData .

.. cpp:member:: ColorF  ItemData::lightColor

	Color value to make this light. Example: "1.0,1.0,1.0".

.. cpp:member:: bool  ItemData::lightOnlyStatic

	If true, this ItemData will only cast a light if the Item for this ItemData has a static value of true.

.. cpp:member:: float  ItemData::lightRadius

	Distance from the center point of this ItemData for the light to affect.

.. cpp:member:: int  ItemData::lightTime

	Time value for the light of this ItemData , used to control the pulse speed of the PulsingLight LightType.

.. cpp:member:: ItemLightType ItemData::lightType

	Type of light to apply to this ItemData . Options are NoLight, ConstantLight, PulsingLight. Default is NoLight.

.. cpp:member:: float  ItemData::maxVelocity

	Maximum velocity that this ItemData is able to move.

.. cpp:member:: bool  ItemData::simpleServerCollision

	Determines if only simple server-side collision will be used (for pick ups). If set to true then only simple, server-side collision detection will be used. This is often the case if the item is used for a pick up object, such as ammo. If set to false then a full collision volume will be used as defined by the shape. The default is true.

.. cpp:member:: bool  ItemData::sticky

	If true, ItemData will 'stick' to any surface it collides with. When an item does stick to a surface, the Item::onStickyCollision() callback is called. The Item has methods to retrieve the world position and normal the Item is stuck to.
