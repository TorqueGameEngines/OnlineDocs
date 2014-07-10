GuiGameListOptionsCtrl
======================

A control for showing pages of options that are gamepad friendly.

Inherit:
	:doc:`GuiGameListMenuCtrl`

Description
-----------

Each row in this control allows the selection of one value from a set of options using the keyboard, gamepad or mouse. The row is rendered as 2 columns: the first column contains the row label, the second column contains left and right arrows (for mouse picking) and the currently selected value.

Methods
-------

.. cpp:function:: void GuiGameListOptionsCtrl::addRow(string label, string options, bool wrapOptions, string callback, int icon, int yPad, bool enabled)

	Add a row to the list control.

	:param label: The text to display on the row as a label.
	:param options: A tab separated list of options.
	:param wrapOptions: Specify true to allow options to wrap at each end or false to prevent wrapping.
	:param callback: Name of a script function to use as a callback when this row is activated.
	:param icon: [optional] Index of the icon to use as a marker.
	:param yPad: [optional] An extra amount of height padding before the row. Does nothing on the first row.
	:param enabled: [optional] If this row is initially enabled.

.. cpp:function:: string GuiGameListOptionsCtrl::getCurrentOption(int row)

	Gets the text for the currently selected option of the given row.

	:param row: Index of the row to get the option from.

	:return: A string representing the text currently displayed as the selected option on the given row. If there is no such displayed text then the empty string is returned. 

.. cpp:function:: bool GuiGameListOptionsCtrl::selectOption(int row, string option)

	Set the row's current option to the one specified.

	:param row: Index of the row to set an option on.
	:param option: The option to be made active.

	:return: True if the row contained the option and was set, false otherwise. 

.. cpp:function:: void GuiGameListOptionsCtrl::setOptions(int row, string optionsList)

	Sets the list of options on the given row.

	:param row: Index of the row to set options on.
	:param optionsList: A tab separated list of options for the control.
