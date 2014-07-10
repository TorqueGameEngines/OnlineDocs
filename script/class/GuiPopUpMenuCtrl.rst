GuiPopUpMenuCtrl
================

A control that allows to select a value from a drop-down list.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

For a nearly identical GUI with additional features, use GuiPopUpMenuCtrlEx.

Example::

	newGuiPopUpMenuCtrl()
	{
	   maxPopupHeight = "200";
	   sbUsesNAColor = "0";
	   reverseTextList = "0";
	   bitmapBounds = "16 16";
	   maxLength = "1024";
	   position = "56 31";
	   extent = "64 64";
	   minExtent = "8 2";
	   profile = "GuiPopUpMenuProfile";
	   tooltipProfile = "GuiToolTipProfile";
	};


Methods
-------


.. cpp:function:: void GuiPopUpMenuCtrl::add(string name, int idNum, int scheme)


.. cpp:function:: void GuiPopUpMenuCtrl::addScheme(int id, ColorI fontColor, ColorI fontColorHL, ColorI fontColorSEL)


.. cpp:function:: void GuiPopUpMenuCtrl::changeTextById(int id, string text)


.. cpp:function:: void GuiPopUpMenuCtrl::clearEntry(S32 entry)


.. cpp:function:: int GuiPopUpMenuCtrl::findText(string text)

	Returns the position of the first entry containing the specified text.

.. cpp:function:: string GuiPopUpMenuCtrl::getTextById(int id)


.. cpp:function:: void GuiPopUpMenuCtrl::replaceText(bool doReplaceText)


.. cpp:function:: void GuiPopUpMenuCtrl::setEnumContent(string class, string enum)

	This fills the popup with a classrep's field enumeration type info. More of a helper function than anything. If console access to the field list is added, at least for the enumerated types, then this should go away..

.. cpp:function:: void GuiPopUpMenuCtrl::setFirstSelected()


.. cpp:function:: void GuiPopUpMenuCtrl::setSelected(int id)


Fields
------


.. cpp:member:: filename  GuiPopUpMenuCtrl::bitmap


.. cpp:member:: Point2I  GuiPopUpMenuCtrl::bitmapBounds


.. cpp:member:: void  GuiPopUpMenuCtrl::clear

	Clear the popup list.

.. cpp:member:: void  GuiPopUpMenuCtrl::forceClose


.. cpp:member:: void  GuiPopUpMenuCtrl::forceOnAction


.. cpp:member:: int  GuiPopUpMenuCtrl::getSelected


.. cpp:member:: string  GuiPopUpMenuCtrl::getText


.. cpp:member:: int  GuiPopUpMenuCtrl::maxPopupHeight


.. cpp:member:: bool  GuiPopUpMenuCtrl::reverseTextList


.. cpp:member:: bool  GuiPopUpMenuCtrl::sbUsesNAColor


.. cpp:member:: void  GuiPopUpMenuCtrl::setNoneSelected


.. cpp:member:: int  GuiPopUpMenuCtrl::size

	Get the size of the menu - the number of entries in it.

.. cpp:member:: void  GuiPopUpMenuCtrl::sort

	Sort the list alphabetically.

.. cpp:member:: void  GuiPopUpMenuCtrl::sortID

	Sort the list by ID.
