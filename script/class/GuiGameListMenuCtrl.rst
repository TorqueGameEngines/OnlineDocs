GuiGameListMenuCtrl
===================

A base class for cross platform menu controls that are gamepad friendly.

Inherit:
	:doc:`GuiControl`

Description
-----------

A base class for cross platform menu controls that are gamepad friendly.

This class is used to build row-based menu GUIs that can be easily navigated using the keyboard, mouse or gamepad. The desired row can be selected using the mouse, or by navigating using the Up and Down buttons.

Example::

	newGuiGameListMenuCtrl()
	{
	   debugRender = "0";
	   callbackOnA = "applyOptions();";
	   callbackOnB = "Canvas.setContent(MainMenuGui);";
	   callbackOnX = "";
	   callbackOnY = "revertOptions();";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiGameListMenuCtrl::activateRow()

	Activates the current row. The script callback of the current row will be called (if it has one).

.. cpp:function:: void GuiGameListMenuCtrl::addRow(string label, string callback, int icon, int yPad, bool useHighlightIcon, bool enabled)

	Add a row to the list control.

	:param label: The text to display on the row as a label.
	:param callback: Name of a script function to use as a callback when this row is activated.
	:param icon: [optional] Index of the icon to use as a marker.
	:param yPad: [optional] An extra amount of height padding before the row. Does nothing on the first row.
	:param useHighlightIcon: [optional] Does this row use the highlight icon?.
	:param enabled: [optional] If this row is initially enabled.

.. cpp:function:: int GuiGameListMenuCtrl::getRowCount()

	Gets the number of rows on the control.

	:return: (int) The number of rows on the control. 

.. cpp:function:: string GuiGameListMenuCtrl::getRowLabel(int row)

	Gets the label displayed on the specified row.

	:param row: Index of the row to get the label of.

	:return: The label for the row. 

.. cpp:function:: int GuiGameListMenuCtrl::getSelectedRow()

	Gets the index of the currently selected row.

	:return: Index of the selected row. 

.. cpp:function:: bool GuiGameListMenuCtrl::isRowEnabled(int row)

	Determines if the specified row is enabled or disabled.

	:param row: The row to set the enabled status of.

	:return: True if the specified row is enabled. False if the row is not enabled or the given index was not valid. 

.. cpp:function:: void GuiGameListMenuCtrl::onChange()

	Called when the selected row changes.

.. cpp:function:: void GuiGameListMenuCtrl::setRowEnabled(int row, bool enabled)

	Sets a row's enabled status according to the given parameters.

	:param row: The index to check for validity.
	:param enabled: Indicate true to enable the row or false to disable it.

.. cpp:function:: void GuiGameListMenuCtrl::setRowLabel(int row, string label)

	Sets the label on the given row.

	:param row: Index of the row to set the label on.
	:param label: Text to set as the label of the row.

.. cpp:function:: void GuiGameListMenuCtrl::setSelected(int row)

	Sets the selected row. Only rows that are enabled can be selected.

	:param row: Index of the row to set as selected.

Fields
------


.. cpp:member:: string  GuiGameListMenuCtrl::callbackOnA

	Script callback when the 'A' button is pressed. 'A' inputs are Keyboard: A, Return, Space; Gamepad: A, Start.

.. cpp:member:: string  GuiGameListMenuCtrl::callbackOnB

	Script callback when the 'B' button is pressed. 'B' inputs are Keyboard: B, Esc, Backspace, Delete; Gamepad: B, Back.

.. cpp:member:: string  GuiGameListMenuCtrl::callbackOnX

	Script callback when the 'X' button is pressed. 'X' inputs are Keyboard: X; Gamepad: X.

.. cpp:member:: string  GuiGameListMenuCtrl::callbackOnY

	Script callback when the 'Y' button is pressed. 'Y' inputs are Keyboard: Y; Gamepad: Y.

.. cpp:member:: bool  GuiGameListMenuCtrl::debugRender

	Enable debug rendering.
