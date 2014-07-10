GuiTextListCtrl
===============

GUI control that displays a list of text. Text items in the list can be individually selected.

Inherit:
	:doc:`GuiArrayCtrl`

Description
-----------

GUI control that displays a list of text. Text items in the list can be individually selected.

Example::

	newGuiTextListCtrl(EndGameGuiList)
	      {
	         columns = "0 256";
	           fitParentWidth = "1";
	         clipColumnText = "0";
	          //Properties not specific to this control have been omitted from this example.
	      };


Methods
-------


.. cpp:function:: int GuiTextListCtrl::addRow(int id, string text, int index)

	Adds a new row at end of the list with the defined id and text. If index is used, then the new row is inserted at the row location of 'index'.

	:param id: Id of the new row.
	:param text: Text to display at the new row.
	:param index: Index to insert the new row at. If not used, new row will be placed at the end of the list.

	:return: Returns the row index of the new row. If 'index' was defined, then this just returns the number of rows in the list.

	Example::

		// Define the id
		%id = "4";
		
		// Define the text to display
		%text = "Display Text"// Define the index (optional)
		%index = "2"// Inform the GuiTextListCtrl control to add the new row with the defined information.
		%rowIndex = %thisGuiTextListCtrl.addRow(%id,%text,%index);

.. cpp:function:: void GuiTextListCtrl::clear()

	Clear the list.

	Example::

		// Inform the GuiTextListCtrl control to clear its contents
		%thisGuiTextListCtrl.clear();

.. cpp:function:: void GuiTextListCtrl::clearSelection()

	Set the selection to nothing.

	Example::

		// Deselect anything that is currently selected
		%thisGuiTextListCtrl.clearSelection();

.. cpp:function:: int GuiTextListCtrl::findTextIndex(string needle)

	Find needle in the list, and return the row number it was found in.

	:param needle: Text to find in the list.

	:return: Row number that the defined text was found in,

	Example::

		// Define the text to find in the list
		%needle = "Text To Find";
		
		// Request the row number that contains the defined text to find
		
		%rowNumber = %thisGuiTextListCtrl.findTextIndex(%needle);

.. cpp:function:: int GuiTextListCtrl::getRowId(int index)

	Get the row ID for an index.

	:param index: Index to get the RowID at

	:return: RowId at the defined index.

	Example::

		// Define the index
		%index = "3";
		
		// Request the row ID at the defined index
		%rowId = %thisGuiTextListCtrl.getRowId(%index);

.. cpp:function:: int GuiTextListCtrl::getRowNumById(int id)

	Get the row number for a specified id.

	:param id: Id to get the row number at

	Example::

		// Define the id
		%id = "4";
		
		// Request the row number from the GuiTextListCtrl control at the defined id.
		%rowNumber = %thisGuiTextListCtrl.getRowNumById(%id);

.. cpp:function:: string GuiTextListCtrl::getRowText(int index)

	Get the text of the row with the specified index.

	:param index: Row index to acquire the text at.

	:return: Text at the defined row index.

	Example::

		// Define the row index
		%index = "5";
		
		// Request the text from the row at the defined index
		%rowText = %thisGuiTextListCtrl.getRowText(%index);

.. cpp:function:: string GuiTextListCtrl::getRowTextById(int id)

	Get the text of a row with the specified id.

	:return: Row text at the requested row id.

	Example::

		// Define the id
		%id = "4";
		
		// Inform the GuiTextListCtrl control to return the text at the defined row id
		%rowText = %thisGuiTextListCtrl.getRowTextById(%id);

.. cpp:function:: int GuiTextListCtrl::getSelectedId()

	Get the ID of the currently selected item.

	:return: The id of the selected item in the list.

	Example::

		// Acquire the ID of the selected item in the list.
		%id = %thisGuiTextListCtrl.getSelectedId();

.. cpp:function:: int GuiTextListCtrl::getSelectedRow()

	Returns the selected row index (not the row ID).

	:return: Index of the selected row

	Example::

		// Acquire the selected row index
		%rowIndex = %thisGuiTextListCtrl.getSelectedRow();

.. cpp:function:: bool GuiTextListCtrl::isRowActive(int rowNum)

	Check if the specified row is currently active or not.

	:param rowNum: Row number to check the active state.

	:return: Active state of the defined row number.

	Example::

		// Define the row number
		%rowNum = "5";
		
		// Request the active state of the defined row number from the GuiTextListCtrl control.
		%rowActiveState = %thisGuiTextListCtrl.isRowActive(%rowNum);

.. cpp:function:: void GuiTextListCtrl::onDeleteKey(string id)

	Called when the delete key has been pressed.

	:param id: Id of the selected item in the list

	Example::

		// The delete key was pressed while the GuiTextListCtrl was in focus, causing the callback to occur.GuiTextListCtrl::onDeleteKey(%this,%id)
		   {
		      // Code to run when the delete key is pressed
		   }

.. cpp:function:: void GuiTextListCtrl::onSelect(string cellid, string text)

	Called whenever an item in the list is selected.

	:param cellid: The ID of the cell that was selected
	:param text: The text in the selected cel

	Example::

		// A cel in the control was selected, causing the callback to occurGuiTextListCtrl::onSelect(%this,%callid,%text)
		   {
		      // Code to run when a cel item is selected
		   }

.. cpp:function:: void GuiTextListCtrl::removeRow(int index)

	Remove a row from the table, based on its index.

	:param index: Row index to remove from the list.

	Example::

		// Define the row index
		%index = "4";
		
		// Inform the GuiTextListCtrl control to remove the row at the defined row index
		%thisGuiTextListCtrl.removeRow(%index);

.. cpp:function:: void GuiTextListCtrl::removeRowById(int id)

	Remove row with the specified id.

	:param id: Id to remove the row entry at

	Example::

		// Define the id
		%id = "4";
		
		// Inform the GuiTextListCtrl control to remove the row at the defined id
		%thisGuiTextListCtrl.removeRowById(%id);

.. cpp:function:: int GuiTextListCtrl::rowCount()

	Get the number of rows.

	:return: Number of rows in the list.

	Example::

		// Get the number of rows in the list
		%rowCount = %thisGuiTextListCtrl.rowCount();

.. cpp:function:: void GuiTextListCtrl::scrollVisible(int rowNum)

	Scroll so the specified row is visible.

	:param rowNum: Row number to make visible

	Example::

		// Define the row number to make visible
		%rowNum = "4";
		
		// Inform the GuiTextListCtrl control to scroll the list so the defined rowNum is visible.
		%thisGuiTextListCtrl.scrollVisible(%rowNum);

.. cpp:function:: void GuiTextListCtrl::setRowActive(int rowNum, bool active)

	Mark a specified row as active/not.

	:param rowNum: Row number to change the active state.
	:param active: Boolean active state to set the row number.

	Example::

		// Define the row number
		%rowNum = "4";
		
		// Define the boolean active state
		%active = "true";
		
		// Informthe GuiTextListCtrl control to set the defined active state at the defined row number.
		%thisGuiTextListCtrl.setRowActive(%rowNum,%active);

.. cpp:function:: void GuiTextListCtrl::setRowById(int id, string text)

	Sets the text at the defined id.

	:param id: Id to change.
	:param text: Text to use at the Id.

	Example::

		// Define the id
		%id = "4";
		
		// Define the text
		%text = "Text To Display";
		
		// Inform the GuiTextListCtrl control to display the defined text at the defined id
		%thisGuiTextListCtrl.setRowById(%id,%text);

.. cpp:function:: void GuiTextListCtrl::setSelectedById(int id)

	Finds the specified entry by id, then marks its row as selected.

	:param id: Entry within the text list to make selected.

	Example::

		// Define the id
		%id = "5";
		
		// Inform the GuiTextListCtrl control to set the defined id entry as selected
		%thisGuiTextListCtrl.setSelectedById(%id);

.. cpp:function:: void GuiTextListCtrl::setSelectedRow(int rowNum)

	the specified row.

	:param rowNum: Row number to set selected.

	Example::

		// Define the row number to set selected
		%rowNum = "4";
		
		%guiTextListCtrl.setSelectedRow(%rowNum);

.. cpp:function:: void GuiTextListCtrl::sort(int columnId, bool increasing)

	Performs a standard (alphabetical) sort on the values in the specified column.

	:param columnId: Column ID to perform the sort on.
	:param increasing: If false, sort will be performed in reverse.

	Example::

		// Define the columnId
		%id = "1";
		
		// Define if we are increasing or not
		%increasing = "false";
		
		// Inform the GuiTextListCtrl to perform the sort operation
		%thisGuiTextListCtrl.sort(%id,%increasing);

.. cpp:function:: void GuiTextListCtrl::sortNumerical(int columnID, bool increasing)

	Perform a numerical sort on the values in the specified column. Detailed description

	:param columnId: Column ID to perform the sort on.
	:param increasing: If false, sort will be performed in reverse.

	Example::

		// Define the columnId
		%id = "1";
		
		// Define if we are increasing or not
		%increasing = "false";
		
		// Inform the GuiTextListCtrl to perform the sort operation
		%thisGuiTextListCtrl.sortNumerical(%id,%increasing);

Fields
------


.. cpp:member:: bool  GuiTextListCtrl::clipColumnText

	If true, text exceeding a column's given width will get clipped.

.. cpp:member:: intList  GuiTextListCtrl::columns

	A vector of column offsets. The number of values determines the number of columns in the table.

.. cpp:member:: bool  GuiTextListCtrl::fitParentWidth

	If true, the width of this control will match the width of its parent.
