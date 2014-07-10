GuiStackControl
===============

A container that stacks its children horizontally or vertically.

Inherit:
	:doc:`GuiControl`

Description
-----------

This container maintains a horizontal or vertical stack of GUI controls. If one is added, deleted, or resized, then the stack is resized to fit. The order of the stack is determined by the internal order of the children (ie. the order of addition).

Example::

	newGuiStackControl()
	{
	   stackingType = "Dynamic";
	   horizStacking = "Left to Right";
	   vertStacking = "Top to Bottom";
	   padding = "4";
	   dynamicSize = "1";
	   dynamicNonStackExtent = "0";
	   dynamicPos = "0";
	   changeChildSizeToFit = "1";
	   changeChildPosition = "1";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------

.. cpp:function:: void GuiStackControl::freeze(bool freeze)

	Prevents control from restacking - useful when adding or removing child controls.

	:param freeze: True to freeze the control, false to unfreeze it

	Example::

		%stackCtrl.freeze(true);
		// add controls to stack
		%stackCtrl.freeze(false);

.. cpp:function:: bool GuiStackControl::isFrozen()

	Return whether or not this control is frozen.

.. cpp:function:: void GuiStackControl::updateStack()

	Restack the child controls.

Fields
------

.. cpp:member:: bool  GuiStackControl::changeChildPosition

	Determines whether to reposition child controls. If true, horizontally stacked children are aligned along the top edge of the stack control. Vertically stacked children are aligned along the left edge of the stack control. If false, horizontally stacked children retain their Y position, and vertically stacked children retain their X position.

.. cpp:member:: bool  GuiStackControl::changeChildSizeToFit

	Determines whether to resize child controls. If true, horizontally stacked children keep their width, but have their height set to the stack control height. Vertically stacked children keep their height, but have their width set to the stack control width. If false, child controls are not resized.

.. cpp:member:: bool  GuiStackControl::dynamicNonStackExtent

	Determines whether to resize the stack control along the non-stack axis (change height for horizontal stacking, change width for vertical stacking). No effect if dynamicSize is false. If true, the stack will be resized to the maximum of the child control widths/heights. If false, the stack will not be resized.

.. cpp:member:: bool  GuiStackControl::dynamicPos

	Determines whether to reposition the stack along the stack axis when it is auto-resized. No effect if dynamicSize is false. If true, the stack will grow left for horizontal stacking, and grow up for vertical stacking. If false, the stack will grow right for horizontal stacking, and grow down for vertical stacking.

.. cpp:member:: bool  GuiStackControl::dynamicSize

	Determines whether to resize the stack control along the stack axis (change width for horizontal stacking, change height for vertical stacking). If true, the stack width/height will be resized to the sum of the child control widths/heights. If false, the stack will not be resized.

.. cpp:member:: GuiHorizontalStackingType GuiStackControl::horizStacking

	Controls the type of horizontal stacking to use ( Left to Right or Right to Left ).

.. cpp:member:: int  GuiStackControl::padding

	Distance (in pixels) between stacked child controls.

.. cpp:member:: GuiStackingType GuiStackControl::stackingType

	Determines the method used to position the child controls.

.. cpp:member:: GuiVerticalStackingType GuiStackControl::vertStacking

	Controls the type of vertical stacking to use ( Top to Bottom or Bottom to Top ).
