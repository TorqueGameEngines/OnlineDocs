Decals
======

Decals are non-SimObject derived objects that are stored and loaded separately from the normal mission file. 

The DecalManager handles all aspects of decal management including loading, creation, saving, and automatically deleting decals that have exceeded their lifeSpan. 

The static decals associated with a mission are normally loaded immediately after the mission itself has loaded as shown below. 

Example::

	// Load the static mission decals.
	decalManagerLoad( %missionName @ ".decals" );

Classes
-------

  .. toctree::
	:maxdepth: 1
	
	class/DecalData
	class/DecalManager

Functions
---------

.. cpp:function:: int decalManagerAddDecal(Point3F position, Point3F normal, float rot, float scale, DecalData decalData, bool isImmortal)

	Adds a new decal to the decal manager.

	:param position: World position for the decal.
	:param normal: Decal normal vector (if the decal was a tire lying flat on a surface, this is the vector pointing in the direction of the axle).
	:param rot: Angle (in radians) to rotate this decal around its normal vector.
	:param scale: Scale factor applied to the decal.
	:param decalData: DecalData datablock to use for the new decal.
	:param isImmortal: Whether or not this decal is immortal. If immortal, it does not expire automatically and must be removed explicitly.

	:return: Returns the ID of the new Decal object or -1 on failure. 

	Example::

		// Specify the decal position
		%position = "1.0 1.0 1.0";
		
		// Specify the up vector
		%normal = "0.0 0.0 1.0";
		
		// Add the new decal.
		%decalObj = decalManagerAddDecal( %position, %normal, 0.5, 0.35, ScorchBigDecal, false );

.. cpp:function:: void decalManagerClear()

	Removes all decals currently loaded in the decal manager.

	Example::

		// Tell the decal manager to remove all existing decals.decalManagerClear();

.. cpp:function:: bool decalManagerDirty()

	Returns whether the decal manager has unsaved modifications.

	:return: True if the decal manager has unsaved modifications, false if everything has been saved. 

	Example::

		// Ask the decal manager if it has unsaved modifications.
		%hasUnsavedModifications = decalManagerDirty();

.. cpp:function:: bool decalManagerLoad(string fileName)

	Clears existing decals and replaces them with decals loaded from the specified file.

	:param fileName: Filename to load the decals from.

	:return: True if the decal manager was able to load the requested file, false if it could not. 

	Example::

		// Set the filename to load the decals from.
		%fileName = "./missionDecals.mis.decals";
		// Inform the decal manager to load the decals from the entered filename.decalManagerLoad( %fileName );

.. cpp:function:: bool decalManagerRemoveDecal(int decalID)

	Remove specified decal from the scene.

	:param decalID: ID of the decal to remove.

	:return: Returns true if successful, false if decal ID not found. 

	Example::

		// Specify a decal ID to be removed
		%decalID = 1;
		
		// Tell the decal manager to remove the specified decal ID.
		decalManagerRemoveDecal( %decalId )

.. cpp:function:: void decalManagerSave(String decalSaveFile)

	Saves the decals for the active mission in the entered filename.

	:param decalSaveFile: Filename to save the decals to.

	Example::

		// Set the filename to save the decals in. If no filename is set, then the
		// decals will default to <activeMissionName>.mis.decals
		%fileName = "./missionDecals.mis.decals";
		// Inform the decal manager to save the decals for the active mission.
		decalManagerSave( %fileName );

Variables
---------

.. cpp:member:: bool $Decals::debugRender

	If true, the decal spheres will be visualized when in the editor.

.. cpp:member:: bool $pref::Decals::enabled

	Controls whether decals are rendered.

.. cpp:member:: float $pref::Decals::lifeTimeScale

	Lifetime that decals will last after being created in the world. Deprecated. Use DecalData::lifeSpan instead.

.. cpp:member:: bool $Decals::poolBuffers

	If true, will merge all PrimitiveBuffers and VertexBuffers into a pair of pools before clearing them at the end of a frame. If false, will just clear them at the end of a frame.

.. cpp:member:: float $Decals::sphereDistanceTolerance

	The distance at which the decal system will start breaking up decal spheres when adding new decals.

.. cpp:member:: float $Decals::sphereRadiusTolerance

	The radius beyond which the decal system will start breaking up decal spheres when adding new decals.
