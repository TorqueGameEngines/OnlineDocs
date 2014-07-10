StaticShape
===========

The most basic 3D shape with a datablock available in Torque 3D.

Inherit:
	:doc:`ShapeBase`

Description
-----------

The most basic 3D shape with a datablock available in Torque 3D.

When it comes to placing 3D objects in the scene, you technically have two options:

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

