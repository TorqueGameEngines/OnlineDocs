GuiListBoxCtrl
==============

A list of text items.

Inherit:
	:doc:`GuiControl`

Description
-----------

A list of text items where each individual entry can have its own text value, text color and associated SimObject.

Example::

	newGuiListBoxCtrl(GuiMusicPlayerMusicList)
	{
	   allowMultipleSelections = "true";
	   fitParentWidth = "true";
	   mirrorSet = "AnotherGuiListBoxCtrl";
	   makeNameCallback = "";
	   colorBullet = "1";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiListBoxCtrl::addFilteredItem(string newItem)

	Checks if there is an item with the exact text of what is passed in, and if so the item is removed from the list and adds that item's data to the filtered list.

	:param itemName: Name of the item that we wish to add to the filtered item list of the GuiListBoxCtrl.

	Example::

		// Define the itemName that we wish to add to the filtered item list.
		%itemName = "This Item Name";
		
		// Add the item name to the filtered item list.
		%thisGuiListBoxCtrl.addFilteredItem(%filteredItemName);

.. cpp:function:: void GuiListBoxCtrl::clearItemColor(int index)

	Removes any custom coloring from an item at the defined index id in the list.

	:param index: Index id for the item to clear any custom color from.

	Example::

		// Define the index id
		%index = "4";
		
		// Request the GuiListBoxCtrl object to remove any custom coloring from the defined index entry
		%thisGuiListBoxCtrl.clearItemColor(%index);

.. cpp:function:: void GuiListBoxCtrl::clearItems()

	Clears all the items in the listbox.

	Example::

		// Inform the GuiListBoxCtrl object to clear all items from its list.
		%thisGuiListBoxCtrl.clearItems();

.. cpp:function:: void GuiListBoxCtrl::clearSelection()

	Sets all currently selected items to unselected. Detailed description

	Example::

		// Inform the GuiListBoxCtrl object to set all of its items to unselected./n%thisGuiListBoxCtrl.clearSelection();

.. cpp:function:: void GuiListBoxCtrl::deleteItem(int itemIndex)

	Removes the list entry at the requested index id from the control and clears the memory associated with it.

	:param itemIndex: Index id location to remove the item from.

	Example::

		// Define the index id we want to remove from the list
		%itemIndex = "8";
		
		// Inform the GuiListBoxCtrl object to remove the item at the defined index id.
		%thisGuiListBoxCtrl.deleteItem(%itemIndex);

.. cpp:function:: void GuiListBoxCtrl::doMirror()

	Informs the GuiListBoxCtrl object to mirror the contents of the GuiListBoxCtrl stored in the mirrorSet field.

	Example::

		\ Inform the object to mirror the object located at %thisGuiListBox.mirrorSet
		%thisGuiListBox.doMirror();

.. cpp:function:: int GuiListBoxCtrl::findItemText(string findText, bool bCaseSensitive)

	Returns index of item with matching text or -1 if none found.

	:param findText: Text in the list to find.
	:param isCaseSensitive: If true, the search will be case sensitive.

	:return: Index id of item with matching text or -1 if none found.

	Example::

		// Define the text we wish to find in the list.
		%findText = "Hickory Smoked Gideon"/n/n// Define if this is a case sensitive search or not.
		%isCaseSensitive = "false";
		
		// Ask the GuiListBoxCtrl object what item id in the list matches the requested text.
		%matchingId = %thisGuiListBoxCtrl.findItemText(%findText,%isCaseSensitive);

.. cpp:function:: int GuiListBoxCtrl::getItemCount()

	Returns the number of items in the list.

	:return: The number of items in the list.

	Example::

		// Request the number of items in the list of the GuiListBoxCtrl object.
		%listItemCount = %thisGuiListBoxCtrl.getItemCount();

.. cpp:function:: string GuiListBoxCtrl::getItemObject(int index)

	Returns the object associated with an item. This only makes sense if you are mirroring a simset.

	:param index: Index id to request the associated item from.

	:return: The object associated with the item in the list.

	Example::

		// Define the index id
		%index = "12";
		
		// Request the item from the GuiListBoxCtrl object
		%object = %thisGuiListBoxCtrl.getItemObject(%index);

.. cpp:function:: string GuiListBoxCtrl::getItemText(int index)

	Returns the text of the item at the specified index.

	:param index: Index id to return the item text from.

	:return: The text of the requested index id.

	Example::

		// Define the index id entry to request the text from
		%index = "12";
		
		// Request the item id text from the GuiListBoxCtrl object.
		%text = %thisGuiListBoxCtrl.getItemText(%index);

.. cpp:function:: int GuiListBoxCtrl::getLastClickItem()

	Request the item index for the item that was last clicked.

	:return: Index id for the last clicked item in the list.

	Example::

		// Request the item index for the last clicked item in the list
		%lastClickedIndex = %thisGuiListBoxCtrl.getLastClickItem();

.. cpp:function:: int GuiListBoxCtrl::getSelCount()

	Returns the number of items currently selected.

	:return: Number of currently selected items.

	Example::

		// Request the number of currently selected items
		%selectedItemCount = %thisGuiListBoxCtrl.getSelCount();

.. cpp:function:: int GuiListBoxCtrl::getSelectedItem()

	Returns the selected items index or -1 if none selected. If multiple selections exist it returns the first selected item.

	:return: The selected items index or -1 if none selected.

	Example::

		// Request the index id of the currently selected item
		%selectedItemId = %thisGuiListBoxCtrl.getSelectedItem();

.. cpp:function:: string GuiListBoxCtrl::getSelectedItems()

	Returns a space delimited list of the selected items indexes in the list.

	:return: Space delimited list of the selected items indexes in the list

	Example::

		// Request a space delimited list of the items in the GuiListBoxCtrl object.
		%selectionList = %thisGuiListBoxCtrl.getSelectedItems();

.. cpp:function:: void GuiListBoxCtrl::insertItem(string text, int index)

	Inserts an item into the list at the specified index and returns the index assigned or -1 on error.

	:param text: Text item to add.
	:param index: Index id to insert the list item text at.

	:return: If successful will return the index id assigned. If unsuccessful, will return -1.

	Example::

		// Define the text to insert
		%text = "Secret Agent Gideon";
		
		// Define the index entry to insert the text at
		%index = "14";
		
		// In form the GuiListBoxCtrl object to insert the text at the defined index.
		%assignedId = %thisGuiListBoxCtrl.insertItem(%text,%index);

.. cpp:function:: bool GuiListBoxCtrl::isObjectMirrored(string indexIdString)

	Checks if a list item at a defined index id is mirrored, and returns the result.

	:param indexIdString: Index id of the list to check.

	:return: A boolean value on if the list item is mirrored or not.

	Example::

		// Engine has requested of the script level to determine if a list entry is mirrored or not.GuiListBoxCtrl::isObjectMirrored(%this, %indexIdString)
		   {
		      // Perform code required to check and see if the list item at the index id is mirrored or not.return %isMirrored;
		   }

.. cpp:function:: void GuiListBoxCtrl::onClearSelection()

	Called whenever a selected item in the list is cleared.

	Example::

		// A selected item is cleared, causing the callback to occur.GuiListBoxCtrl::onClearSelection(%this)
		   {
		      // Code to run whenever a selected item is cleared
		   }

.. cpp:function:: void GuiListBoxCtrl::onDeleteKey()

	Called whenever the Delete key on the keyboard has been pressed while in this control.

	Example::

		// The delete key on the keyboard has been pressed while this control is in focus, causing the callback to occur.GuiListBoxCtrl::onDeleteKey(%this)
		   {
		      // Code to call whenever the delete key is pressed
		   }

.. cpp:function:: void GuiListBoxCtrl::onDoubleClick()

	Called whenever an item in the list has been double clicked.

	Example::

		// An item in the list is double clicked, causing the callback to occur.GuiListBoxCtrl::onDoubleClick(%this)
		   {
		      // Code to run whenever an item in the control has been double clicked
		   }

.. cpp:function:: void GuiListBoxCtrl::onMouseDragged()

	Called whenever the mouse is dragged across the control.

	Example::

		// Mouse is dragged across the control, causing the callback to occur.GuiListBoxCtrl::onMouseDragged(%this)
		   {
		      // Code to run whenever the mouse is dragged across the control
		   }

.. cpp:function:: void GuiListBoxCtrl::onMouseUp(string itemHit, string mouseClickCount)

	Called whenever the mouse has previously been clicked down (onMouseDown) and has now been raised on the control. If an item in the list was hit during the click cycle, then the index id of the clicked object along with how many clicks occured are passed into the callback. Detailed description

	:param itemHit: Index id for the list item that was hit
	:param mouseClickCount: How many mouse clicks occured on this list item

	Example::

		// Mouse was previously clicked down, and now has been released, causing the callback to occur.GuiListBoxCtrl::onMouseUp(%this, %itemHit, %mouseClickCount)
		   {
		      // Code to call whenever the mouse has been clicked and released on the control
		   }

.. cpp:function:: void GuiListBoxCtrl::onSelect(string index, string itemText)

	Called whenever an item in the list is selected.

	:param index: Index id for the item in the list that was selected.
	:param itemText: Text for the list item at the index that was selected.

	Example::

		// An item in the list is selected, causing the callback to occurGuiListBoxCtrl::onSelect(%this, %index, %itemText)
		   {
		      // Code to run whenever an item in the list is selected
		   }

.. cpp:function:: void GuiListBoxCtrl::onUnselect(string index, string itemText)

	Called whenever a selected item in the list has been unselected.

	:param index: Index id of the item that was unselected
	:param itemText: Text for the list entry at the index id that was unselected

	Example::

		// A selected item is unselected, causing the callback to occur
		GuiListBoxCtrl::onUnSelect(%this, %indexId, %itemText)
		   {
		      // Code to run whenever a selected list item is unselected
		   }

.. cpp:function:: void GuiListBoxCtrl::removeFilteredItem(string itemName)

	Removes an item of the entered name from the filtered items list.

	:param itemName: Name of the item to remove from the filtered list.

	Example::

		// Define the itemName that you wish to remove.
		%itemName = "This Item Name";
		
		// Remove the itemName from the GuiListBoxCtrl
		%thisGuiListBoxCtrl.removeFilteredItem(%itemName);

.. cpp:function:: void GuiListBoxCtrl::setCurSel(int indexId)

	Sets the currently selected item at the specified index.

	:param indexId: Index Id to set selected.

	Example::

		// Define the index id that we wish to select.
		%selectId = "4";
		
		// Inform the GuiListBoxCtrl object to set the requested index as selected.
		%thisGuiListBoxCtrl.setCurSel(%selectId);

.. cpp:function:: void GuiListBoxCtrl::setCurSelRange(int indexStart, int indexStop)

	Sets the current selection range from index start to stop. If no stop is specified it sets from start index to the end of the list.

	:param indexStart: Index Id to start selection.
	:param indexStop: Index Id to end selection.

	Example::

		// Set start id
		%indexStart = "3";
		
		// Set end id
		%indexEnd = "6";
		
		// Request the GuiListBoxCtrl object to select the defined range.
		%thisGuiListBoxCtrl.setCurSelRange(%indexStart,%indexEnd);

.. cpp:function:: void GuiListBoxCtrl::setItemColor(int index, ColorF color)

	Sets the color of a single list entry at the specified index id.

	:param index: Index id to modify the color of in the list.
	:param color: Color value to set the list entry to.

	Example::

		// Define the index id value
		%index = "5";
		
		// Define the color value
		%color = "1.0 0.0 0.0";
		
		// Inform the GuiListBoxCtrl object to change the color of the requested index
		%thisGuiListBoxCtrl.setItemColor(%index,%color);

.. cpp:function:: void GuiListBoxCtrl::setItemText(int index, string newtext)

	Sets the items text at the specified index.

	:param index: Index id to set the item text at.
	:param newtext: Text to change the list item at index id to.

	Example::

		// Define the index id/n%index = "12";// Define the text to set the list item to
		%newtext = "Gideons Fancy Goggles";
		
		// Inform the GuiListBoxCtrl object to change the text at the requested index
		%thisGuiListBoxCtrl.setItemText(%index,%newText);

.. cpp:function:: void GuiListBoxCtrl::setItemTooltip(int index, string text)

	Set the tooltip text to display for the given list item.

	:param index: Index id to change the tooltip text
	:param text: Text for the tooltip.

	Example::

		// Define the index id
		%index = "12";
		
		// Define the tooltip text
		%tooltip = "Gideons goggles can see through space and time."// Inform the GuiListBoxCtrl object to set the tooltop for the item at the defined index id
		%thisGuiListBoxCtrl.setItemToolTip(%index,%tooltip);

.. cpp:function:: void GuiListBoxCtrl::setMultipleSelection(bool allowMultSelections)

	Enable or disable multiple selections for this GuiListBoxCtrl object.

	:param allowMultSelections: Boolean variable to set the use of multiple selections or not.

	Example::

		// Define the multiple selection use state.
		%allowMultSelections = "true";
		
		// Set the allow  multiple selection state on the GuiListBoxCtrl object.
		%thisGuiListBoxCtrl.setMultipleSelection(%allowMultSelections);

.. cpp:function:: void GuiListBoxCtrl::setSelected(int index, bool setSelected)

	Sets the item at the index specified to selected or not. Detailed description

	:param index: Item index to set selected or unselected.
	:param setSelected: Boolean selection state to set the requested item index.

	Example::

		// Define the index
		%index = "5";
		
		// Define the selection state
		%selected = "true"// Inform the GuiListBoxCtrl object of the new selection state for the requested index entry.
		%thisGuiListBoxCtrl.setSelected(%index,%selected);

Fields
------


.. cpp:member:: bool  GuiListBoxCtrl::allowMultipleSelections

	If true, will allow the selection of multiple items in the listbox.

.. cpp:member:: bool  GuiListBoxCtrl::colorBullet

	If true, colored items will render a colored rectangular bullet next to the item text.

.. cpp:member:: bool  GuiListBoxCtrl::fitParentWidth

	If true, the width of the listbox will match the width of its parent control.

.. cpp:member:: string  GuiListBoxCtrl::makeNameCallback

	A script snippet to control what is displayed in the list for a SimObject . Within this snippet, $ThisControl is bound to the guiListBoxCtrl and $ThisObject to the contained object in question.

.. cpp:member:: string  GuiListBoxCtrl::mirrorSet

	If populated with the name of another GuiListBoxCtrl , then this list box will mirror the contents of the mirrorSet listbox.
