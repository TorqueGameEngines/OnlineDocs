ForestBrushElement
==================

Represents a type of ForestItem and parameters for how it is placed when painting with a ForestBrush that contains it.

Inherit:
	:doc:`SimObject`

Description
-----------

Represents a type of ForestItem and parameters for how it is placed when painting with a ForestBrush that contains it.


Fields
------


.. cpp:member:: float  ForestBrushElement::elevationMax

	The max world space elevation this item will be placed.

.. cpp:member:: float  ForestBrushElement::elevationMin

	The min world space elevation this item will be placed.

.. cpp:member:: ForestItemData ForestBrushElement::ForestItemData

	The type of ForestItem this element holds placement parameters for.

.. cpp:member:: float  ForestBrushElement::probability

	The probability that this element will be created during an editor brush stroke is the sum of all element probabilities in the brush divided by the probability of this element.

.. cpp:member:: float  ForestBrushElement::rotationRange

	The max rotation in degrees that items will be placed.

.. cpp:member:: float  ForestBrushElement::scaleExponent

	An exponent used to bias between the minimum and maximum random sizes.

.. cpp:member:: float  ForestBrushElement::scaleMax

	The maximum random size of each item.

.. cpp:member:: float  ForestBrushElement::scaleMin

	The minimum random size for each item.

.. cpp:member:: float  ForestBrushElement::sinkMax

	Max variation in the sink radius.

.. cpp:member:: float  ForestBrushElement::sinkMin

	Min variation in the sink radius.

.. cpp:member:: float  ForestBrushElement::sinkRadius

	This is the radius used to calculate how much to sink the trunk at its base and is used to sink the tree into the ground when its on a slope.

.. cpp:member:: float  ForestBrushElement::slopeMax

	The max surface slope in degrees this item will be placed on.

.. cpp:member:: float  ForestBrushElement::slopeMin

	The min surface slope in degrees this item will be placed on.
