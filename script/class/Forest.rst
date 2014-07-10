Forest
======

Forest is a global-bounds scene object provides collision and rendering for a (.forest) data file.

Inherit:
	:doc:`SceneObject`

Description
-----------

Forest is a global-bounds scene object provides collision and rendering for a (.forest) data file.

Forest is designed to efficiently render a large number of static meshes: trees, rocks plants, etc. These cannot be moved at game-time or play animations but do support wind effects using vertex shader transformations guided by vertex color in the asset and user placed wind emitters ( or weapon explosions ).

Script level manipulation of forest data is not possible through Forest, it is only the rendering/collision. All editing is done through the world editor.


Methods
-------


.. cpp:function:: void Forest::clear()


.. cpp:function:: bool Forest::isDirty()


.. cpp:function:: void Forest::regenCells()


Fields
------


.. cpp:member:: filename  Forest::dataFile

	The source forest data file.

.. cpp:member:: float  Forest::lodReflectScalar

	Scalar applied to the farclip distance when Forest renders into a reflection.

.. cpp:member:: bool  Forest::saveDataFile

	saveDataFile( [path] )
