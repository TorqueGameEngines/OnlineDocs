Foliage
=======

Objects used for mass replication of foliage, such as grass, rocks, and bushes. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/fxFoliageReplicator
	class/fxShapeReplicatedStatic
	class/fxShapeReplicator
	class/GroundCover

Functions
---------

.. cpp:function:: void StartClientReplication()

	Activates the shape replicator.

	Example::

		// Call the function
		StartClientReplication()

.. cpp:function:: void StartFoliageReplication()

	Activates the foliage replicator.

	Example::

		// Call the function
		StartFoliageReplication();

Variables
---------

.. cpp:member:: float $pref::GroundCover::densityScale

	A global LOD scalar which can reduce the overall density of placed GroundCover .

.. cpp:member:: int  GroundCover::renderedBatches  [static, inherited]

	Stat for number of rendered billboard batches.

.. cpp:member:: int  GroundCover::renderedBillboards  [static, inherited]

	Stat for number of rendered billboards.

.. cpp:member:: int  GroundCover::renderedCells  [static, inherited]

	Stat for number of rendered cells.

.. cpp:member:: int  GroundCover::renderedShapes  [static, inherited]

	Stat for number of rendered shapes.
