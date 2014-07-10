GuiDynamicCtrlArrayControl
==========================

A container that arranges children into a grid.

Inherit:
	:doc:`GuiControl`

Description
-----------

This container maintains a 2D grid of GUI controls. If one is added, deleted, or resized, then the grid is updated. The insertion order into the grid is determined by the internal order of the children (ie. the order of addition).
Children are added to the grid by row or column until they fill the assocated GuiDynamicCtrlArrayControl extent (width or height). For example, a GuiDynamicCtrlArrayControl with 15 children, and fillRowFirst set to true may be arranged as follows:

If dynamicSize were set to true in this case, the GuiDynamicCtrlArrayControl height would be calculated to fit the 3 rows of child controls.

Example::

	newGuiDynamicCtrlArrayControl()
	{
	   colSize = "128";
	   rowSize = "18";
	   colSpacing = "2";
	   rowSpacing = "2";
	   frozen = "0";
	   autoCellSize = "1";
	   fillRowFirst = "1";
	   dynamicSize = "1";
	   padding = "0 0 0 0";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiDynamicCtrlArrayControl::refresh()

	Recalculates the position and size of this control and all its children.

Fields
------


.. cpp:member:: bool  GuiDynamicCtrlArrayControl::autoCellSize

	When true, the cell size is set to the widest/tallest child control.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::colCount

	Number of columns the child controls have been arranged into. This value is calculated automatically when children are added, removed or resized; writing it directly has no effect.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::colSize

	Width of each column. If autoCellSize is set, this will be calculated automatically from the widest child control.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::colSpacing

	Spacing between columns.

.. cpp:member:: bool  GuiDynamicCtrlArrayControl::dynamicSize

	If true, the width or height of this control will be automatically calculated based on the number of child controls (width if fillRowFirst is false, height if fillRowFirst is true).

.. cpp:member:: bool  GuiDynamicCtrlArrayControl::fillRowFirst

	Controls whether rows or columns are filled first. If true, controls are added to the grid left-to-right (to fill a row); then rows are added top-to-bottom as shown below: If false, controls are added to the grid top-to-bottom (to fill a column); then columns are added left-to-right as shown below:

.. cpp:member:: bool  GuiDynamicCtrlArrayControl::frozen

	When true, the array will not update when new children are added or in response to child resize events. This is useful to prevent unnecessary resizing when adding, removing or resizing a number of child controls.

.. cpp:member:: RectSpacingI  GuiDynamicCtrlArrayControl::padding

	Padding around the top, bottom, left, and right of this control. This reduces the area available for child controls.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::rowCount

	Number of rows the child controls have been arranged into. This value is calculated automatically when children are added, removed or resized; writing it directly has no effect.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::rowSize

	Height of each row. If autoCellSize is set, this will be calculated automatically from the tallest child control.

.. cpp:member:: int  GuiDynamicCtrlArrayControl::rowSpacing

	Spacing between rows.
