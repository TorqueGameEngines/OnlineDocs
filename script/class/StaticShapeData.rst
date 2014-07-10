StaticShapeData
===============

derrived shape datablock available in Torque 3D.

Inherit:
	:doc:`ShapeBaseData`

Description
-----------

The most basic ShapeBaseData derrived shape datablock available in Torque 3D.

When it comes to placing 3D objects in the scene, you effectively have two options:

1. TSStatic objects

2. ShapeBase derived objects

Since ShapeBase and ShapeBaseData are not meant to be instantiated in script, you will use one of its child classes instead. Several game related objects are derived from ShapeBase: Player, Vehicle, Item, and so on.

When you need a 3D object with datablock capabilities, you will use an object derived from ShapeBase. When you need an object with extremely low overhead, and with no other purpose than to be a 3D object in the scene, you will use TSStatic.

The most basic child of ShapeBase is StaticShape. It does not introduce any of the additional functionality you see in Player, Item, Vehicle or the other game play heavy classes. At its core, it is comparable to a TSStatic, but with a datbalock. Having a datablock provides a location for common variables as well as having access to various ShapeBaseData, GameBaseData and SimDataBlock callbacks.

Example::

	// Create a StaticShape using a datablock
	datablock StaticShapeData(BasicShapeData)
	{
	   shapeFile = "art/shapes/items/kit/healthkit.dts";
	   testVar = "Simple string, not a stock variable";
	};
	
	newStaticShape()
	{
	   dataBlock = "BasicShapeData";
	   position = "0.0 0.0 0.0";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	};


Fields
------


.. cpp:member:: int  StaticShapeData::dynamicType

	An integer value which, if speficied, is added to the value retured by getType(). This allows you to extend the type mask for a StaticShape that uses this datablock. Type masks are used for container queries, etc.

.. cpp:member:: bool  StaticShapeData::noIndividualDamage

	Deprecated.
