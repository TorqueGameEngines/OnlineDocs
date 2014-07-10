GuiPopUpMenuCtrlEx
==================

A control that allows to select a value from a drop-down list.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

This is essentially a GuiPopUpMenuCtrl, but with quite a few more features.

Example::

	newGuiPopUpMenuCtrlEx()
	{
	   maxPopupHeight = "200";
	   sbUsesNAColor = "0";
	   reverseTextList = "0";
	   bitmapBounds = "16 16";
	   hotTrackCallback = "0";
	   extent = "64 64";
	   profile = "GuiDefaultProfile";
	   tooltipProfile = "GuiToolTipProfile";
	};


Methods
-------


.. cpp:function:: void GuiPopUpMenuCtrlEx::add(string name, int idNum, int scheme)


.. cpp:function:: void GuiPopUpMenuCtrlEx::add(string name, S32 idNum, S32 scheme)

	Adds an entry to the list.

	:param name: String containing the name of the entry
	:param idNum: Numerical value assigned to the name
	:param scheme: Optional ID associated with a scheme for font coloring, highlight coloring, and selection coloring

.. cpp:function:: void GuiPopUpMenuCtrlEx::addCategory(string text)

	Add a category to the list. Acts as a separator between entries, allowing for sub-lists

	:param text: Name of the new category

.. cpp:function:: void GuiPopUpMenuCtrlEx::addScheme(int id, ColorI fontColor, ColorI fontColorHL, ColorI fontColorSEL)

	Create a new scheme and add it to the list of choices for when a new text entry is added.

	:param id: Numerical id associated with this scheme
	:param fontColor: The base text font color. Formatted as "Red Green Blue", each a numerical between 0 and 255.
	:param fontColorHL: Color of text when being highlighted. Formatted as "Red Green Blue", each a numerical between 0 and 255.
	:param fontColorSel: Color of text when being selected. Formatted as "Red Green Blue", each a numerical between 0 and 255.

.. cpp:function:: void GuiPopUpMenuCtrlEx::clear()

	Clear the popup list. Reimplemented from SimSet .

.. cpp:function:: void GuiPopUpMenuCtrlEx::clearEntry(S32 entry)


.. cpp:function:: int GuiPopUpMenuCtrlEx::findText(string text)

	Returns the id of the first entry containing the specified text or -1 if not found.

	:param text: String value used for the query

	:return: Numerical ID of entry containing the text. 

.. cpp:function:: void GuiPopUpMenuCtrlEx::forceClose()

	Manually force this control to collapse and close.

.. cpp:function:: void GuiPopUpMenuCtrlEx::forceOnAction()

	Manually for the onAction function, which updates everything in this control.

.. cpp:function:: int GuiPopUpMenuCtrlEx::getSelected()

	Get the current selection of the menu.

	:return: Returns the ID of the currently selected entry 

.. cpp:function:: string GuiPopUpMenuCtrlEx::getText()

	Get the. Detailed description

	:param param: Description

	:return: Returns current text in string format 

	Example::

		// Comment
		code();

.. cpp:function:: string GuiPopUpMenuCtrlEx::getTextById(int id)

	Get the text of an entry based on an ID.

	:param id: The ID assigned to the entry being queried

	:return: String contained by the specified entry, NULL if empty or bad ID 

.. cpp:function:: void GuiPopUpMenuCtrlEx::setNoneSelected(int param)

	Clears selection in the menu.

.. cpp:function:: GuiPopUpMenuCtrlEx::setSelected(int id, bool scriptCallback)

	brief Manually set an entry as selected int his control

	:param id: The ID of the entry to select
	:param scripCallback: Optional boolean that forces the script callback if true

.. cpp:function:: GuiPopUpMenuCtrlEx::setSelected(bool scriptCallback)

	brief Manually set the selection to the first entry

	:param scripCallback: Optional boolean that forces the script callback if true

.. cpp:function:: void GuiPopUpMenuCtrlEx::setText(string text)

	Set the current text to a specified value. Reimplemented from GuiTextCtrl .

	:param text: String containing new text to set

.. cpp:function:: void GuiPopUpMenuCtrlEx::sort()

	Sort the list alphabetically.

.. cpp:function:: void GuiPopUpMenuCtrlEx::sortID()

	Sort the list by ID.

Fields
------


.. cpp:member:: filename  GuiPopUpMenuCtrlEx::bitmap

	File name of bitmap to use.

.. cpp:member:: Point2I  GuiPopUpMenuCtrlEx::bitmapBounds

	Boundaries of bitmap displayed.

.. cpp:member:: string  GuiPopUpMenuCtrlEx::getColorById

	Get color of an entry's box.

	:param id: ID number of entry to query

	:return: ColorI in the format of "Red Green Blue Alpha", each of with is a value between 0 - 255 

.. cpp:member:: bool  GuiPopUpMenuCtrlEx::hotTrackCallback

	Whether to provide a 'onHotTrackItem' callback when a list item is hovered over.

.. cpp:member:: int  GuiPopUpMenuCtrlEx::maxPopupHeight

	Length of menu when it extends.

.. cpp:member:: void  GuiPopUpMenuCtrlEx::replaceText

	Flag that causes each new text addition to replace the current entry.

	:param True: to turn on replacing, false to disable it

.. cpp:member:: bool  GuiPopUpMenuCtrlEx::reverseTextList

	Reverses text list if popup extends up, instead of down.

.. cpp:member:: bool  GuiPopUpMenuCtrlEx::sbUsesNAColor

	Deprecated.

.. cpp:member:: void  GuiPopUpMenuCtrlEx::setEnumContent

	This fills the popup with a classrep's field enumeration type info. More of a helper function than anything. If console access to the field list is added, at least for the enumerated types, then this should go away.

	:param class: Name of the class containing the enum
	:param enum: Name of the enum value to acces

.. cpp:member:: int  GuiPopUpMenuCtrlEx::size

	Get the size of the menu.

	:return: Number of entries in the menu 
