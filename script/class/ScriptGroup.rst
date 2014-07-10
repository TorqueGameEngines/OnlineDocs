ScriptGroup
===========

Essentially a SimGroup, but with onAdd and onRemove script callbacks.

Inherit:
	:doc:`SimGroup`

Description
-----------

Essentially a SimGroup, but with onAdd and onRemove script callbacks.

Example::

	// First container, SimGroup containing a ScriptGroupnewSimGroup(Scenes)
	{
	   // Subcontainer, ScriptGroup containing variables
	   // related to a cut scene and a starting 
	   WayPointnewScriptGroup(WelcomeScene)
	   {
	      class = "Scene";
	      pathName = "Pathx";
	      description = "A small orc village set in the Hardesty mountains. This town and its surroundings will be used to illustrate some the Torque Game Engines features.";
	      pathTime = "0";
	      title = "Welcome to Orc Town";
	
	      newWayPoint(start)
	      {
	         position = "163.873 -103.82 208.354";
	         rotation = "0.136165 -0.0544916 0.989186 44.0527";
	         scale = "1 1 1";
	         dataBlock = "WayPointMarker";
	         team = "0";
	      };
	   };
	};


Methods
-------

.. cpp:function:: void ScriptGroup::onAdd(SimObjectId ID)

	Called when this ScriptGroup is added to the system.

	:param ID: Unique object ID assigned when created (this in script).

.. cpp:function:: void ScriptGroup::onRemove(SimObjectId ID)

	Called when this ScriptObject is removed from the system.

	:param ID: Unique object ID assigned when created (this in script).
