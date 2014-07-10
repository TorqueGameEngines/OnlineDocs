GuiFrameSetCtrl
===============

A gui control allowing a window to be subdivided into panes, each of which displays a gui control child of the GuiFrameSetCtrl.

Inherit:
	:doc:`GuiContainer`

Description
-----------

Each gui control child will have an associated FrameDetail through which frame-specific details can be assigned. Frame-specific values override the values specified for the entire frameset.

Note that it is possible to have more children than frames, or more frames than children. In the former case, the extra children will not be visible (they are moved beyond the visible extent of the frameset). In the latter case, frames will be empty. For example, if a frameset had two columns and two rows but only three gui control children they would be assigned to frames as follows:

The last frame would be blank.

Example::

	newGuiFrameSetCtrl()
	{
	   columns = "3";
	   rows = "2";
	   borderWidth = "1";
	   borderColor = "128 128 128";
	   borderEnable = "dynamic";
	   borderMovable = "dynamic";
	   autoBalance = "1";
	   fudgeFactor = "0";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiFrameSetCtrl::addColumn()

	Add a new column.

.. cpp:function:: void GuiFrameSetCtrl::addRow()

	Add a new row.

.. cpp:function:: void GuiFrameSetCtrl::frameBorder(int index, string state)

	Override the borderEnable setting for this frame.

	:param index: Index of the frame to modify
	:param state: New borderEnable state: "on", "off" or "dynamic"

.. cpp:function:: void GuiFrameSetCtrl::frameMinExtent(int index, int width, int height)

	Set the minimum width and height for the frame. It will not be possible for the user to resize the frame smaller than this.

	:param index: Index of the frame to modify
	:param width: Minimum width in pixels
	:param height: Minimum height in pixels

.. cpp:function:: void GuiFrameSetCtrl::frameMovable(int index, string state)

	Override the borderMovable setting for this frame.

	:param index: Index of the frame to modify
	:param state: New borderEnable state: "on", "off" or "dynamic"

.. cpp:function:: void GuiFrameSetCtrl::framePadding(int index, RectSpacingI padding)

	Set the padding for this frame. Padding introduces blank space on the inside edge of the frame.

	:param index: Index of the frame to modify
	:param padding: Frame top, bottom, left, and right padding

.. cpp:function:: int GuiFrameSetCtrl::getColumnCount()

	Get the number of columns.

	:return: The number of columns 

.. cpp:function:: int GuiFrameSetCtrl::getColumnOffset(int index)

	Get the horizontal offset of a column.

	:param index: Index of the column to query

	:return: Column offset in pixels 

.. cpp:function:: RectSpacingI GuiFrameSetCtrl::getFramePadding(int index)

	Get the padding for this frame.

	:param index: Index of the frame to query

.. cpp:function:: int GuiFrameSetCtrl::getRowCount()

	Get the number of rows.

	:return: The number of rows 

.. cpp:function:: int GuiFrameSetCtrl::getRowOffset(int index)

	Get the vertical offset of a row.

	:param index: Index of the row to query

	:return: Row offset in pixels 

.. cpp:function:: void GuiFrameSetCtrl::removeColumn()

	Remove the last (rightmost) column.

.. cpp:function:: void GuiFrameSetCtrl::removeRow()

	Remove the last (bottom) row.

.. cpp:function:: void GuiFrameSetCtrl::setColumnOffset(int index, int offset)

	Set the horizontal offset of a column. Note that column offsets must always be in increasing order, and therefore this offset must be between the offsets of the colunns either side.

	:param index: Index of the column to modify
	:param offset: New column offset

.. cpp:function:: void GuiFrameSetCtrl::setRowOffset(int index, int offset)

	Set the vertical offset of a row. Note that row offsets must always be in increasing order, and therefore this offset must be between the offsets of the rows either side.

	:param index: Index of the row to modify
	:param offset: New row offset

.. cpp:function:: void GuiFrameSetCtrl::updateSizes()

	Recalculates child control sizes.

Fields
------


.. cpp:member:: bool  GuiFrameSetCtrl::autoBalance

	If true, row and column offsets are automatically scaled to match the new extents when the control is resized.

.. cpp:member:: ColorI  GuiFrameSetCtrl::borderColor

	Color of interior borders between cells.

.. cpp:member:: GuiFrameState GuiFrameSetCtrl::borderEnable

	Controls whether frame borders are enabled. Frames use this value unless overridden for that frame using ctrl.frameBorder(index)

.. cpp:member:: GuiFrameState GuiFrameSetCtrl::borderMovable

	Controls whether borders can be dynamically repositioned with the mouse by the user. Frames use this value unless overridden for that frame using ctrl.frameMovable(index)

.. cpp:member:: int  GuiFrameSetCtrl::borderWidth

	Width of interior borders between cells in pixels.

.. cpp:member:: intList  GuiFrameSetCtrl::columns

	A vector of column offsets (determines the width of each column).

.. cpp:member:: int  GuiFrameSetCtrl::fudgeFactor

	Offset for row and column dividers in pixels.

.. cpp:member:: intList  GuiFrameSetCtrl::rows

	A vector of row offsets (determines the height of each row).
