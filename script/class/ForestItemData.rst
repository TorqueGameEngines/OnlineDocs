ForestItemData
==============

Base class for defining a type of ForestItem. It does not implement loading or rendering of the shapeFile.

Inherit:
	:doc:`SimDataBlock`

Description
-----------

Base class for defining a type of ForestItem. It does not implement loading or rendering of the shapeFile.


Fields
------


.. cpp:member:: float  ForestItemData::branchAmp

	Amplitude of the effect on larger branches.

.. cpp:member:: bool  ForestItemData::collidable

	Can other objects or spacial queries hit items of this type.

.. cpp:member:: float  ForestItemData::dampingCoefficient

	Coefficient used in calculating spring forces on the trunk. Causes oscillation and forces to decay faster over time.

.. cpp:member:: float  ForestItemData::detailAmp

	Amplitude of the winds effect on leafs/fronds.

.. cpp:member:: float  ForestItemData::detailFreq

	Frequency (speed) of the effect on leafs/fronds.

.. cpp:member:: float  ForestItemData::mass

	Mass used in calculating spring forces on the trunk. Generally how springy a plant is.

.. cpp:member:: float  ForestItemData::radius

	Radius used during placement to ensure items are not crowded.

.. cpp:member:: float  ForestItemData::rigidity

	Rigidity used in calculating spring forces on the trunk. How much the plant resists the wind force.

.. cpp:member:: filename  ForestItemData::shapeFile

	Shape file for this item type.

.. cpp:member:: float  ForestItemData::tightnessCoefficient

	Coefficient used in calculating spring forces on the trunk. How much the plant resists bending.

.. cpp:member:: float  ForestItemData::trunkBendScale

	Overall bend amount of the tree trunk by wind and impacts.

.. cpp:member:: float  ForestItemData::windScale

	Overall scale to the effect of wind.
