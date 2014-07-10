GameBaseData
============

objects.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Scriptable, demo-able datablock. Used by GameBase objects.


Methods
-------


.. cpp:function:: void GameBaseData::onAdd(GameBase obj)

	Called when the object is added to the scene.

	:param obj: the GameBase object

	Example::

		datablock GameBaseData(MyObjectData)
		{
		   category = "Misc";
		};
		
		function MyObjectData::onAdd( %this, %obj )
		{
		   echo( "Added " @ %obj.getName() @ " to the scene." );
		}
		
		function MyObjectData::onNewDataBlock( %this, %obj )
		{
		   echo( "Assign " @ %this.getName() @ " datablock to " %obj.getName() );
		}
		
		function MyObjectData::onRemove( %this, %obj )
		{
		   echo( "Removed " @ %obj.getName() @ " to the scene." );
		}
		
		function MyObjectData::onMount( %this, %obj, %mountObj, %node )
		{
		   echo( %obj.getName() @ " mounted to " @ %mountObj.getName() );
		}
		
		function MyObjectData::onUnmount( %this, %obj, %mountObj, %node )
		{
		   echo( %obj.getName() @ " unmounted from " @ %mountObj.getName() );
		}

.. cpp:function:: void GameBaseData::onMount(GameBase obj, SceneObject mountObj, int node)

	Called when the object is mounted to another object in the scene.

	:param obj: the GameBase object being mounted
	:param mountObj: the object we are mounted to
	:param node: the mountObj node we are mounted to

.. cpp:function:: void GameBaseData::onNewDataBlock(GameBase obj)

	Called when the object has a new datablock assigned.

	:param obj: the GameBase object

.. cpp:function:: void GameBaseData::onRemove(GameBase obj)

	Called when the object is removed from the scene.

	:param obj: the GameBase object

.. cpp:function:: void GameBaseData::onUnmount(GameBase obj, SceneObject mountObj, int node)

	Called when the object is unmounted from another object in the scene.

	:param obj: the GameBase object being unmounted
	:param mountObj: the object we are unmounted from
	:param node: the mountObj node we are unmounted from

Fields
------


.. cpp:member:: caseString  GameBaseData::category

	The group that this datablock will show up in under the "Scripted" tab in the World Editor Library.
