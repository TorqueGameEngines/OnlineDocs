GuiTabBookCtrl
==============

A container.

Inherit:
	:doc:`GuiContainer`

Description
-----------

A container.

Example::

	// Create 


Methods
-------


.. cpp:function:: void GuiTabBookCtrl::addPage(string title)

	Add a new tab page to the control.

	:param title: Title text for the tab page header.

.. cpp:function:: int GuiTabBookCtrl::getSelectedPage()

	Get the index of the currently selected tab page.

	:return: Index of the selected tab page or -1 if no tab page is selected. 

.. cpp:function:: void GuiTabBookCtrl::onTabRightClick(String text, int index)

	Called when the user right-clicks on a tab page header.

	:param text: Text of the page header for the tab that is being selected.
	:param index: Index of the tab page being selected.

.. cpp:function:: void GuiTabBookCtrl::onTabSelected(String text, int index)

	Called when a new tab page is selected.

	:param text: Text of the page header for the tab that is being selected.
	:param index: Index of the tab page being selected.

.. cpp:function:: void GuiTabBookCtrl::selectPage(int index)

	Set the selected tab page.

	:param index: Index of the tab page.

Fields
------


.. cpp:member:: bool  GuiTabBookCtrl::allowReorder

	Whether reordering tabs with the mouse is allowed.

.. cpp:member:: int  GuiTabBookCtrl::defaultPage

	Index of page to select on first onWake() call (-1 to disable).

.. cpp:member:: int  GuiTabBookCtrl::frontTabPadding

	X offset of first tab page header.

.. cpp:member:: int  GuiTabBookCtrl::minTabWidth

	Minimum width allocated to a tab page header.

.. cpp:member:: int  GuiTabBookCtrl::selectedPage

	Index of currently selected page.

.. cpp:member:: int  GuiTabBookCtrl::tabHeight

	Height of tab page headers.

.. cpp:member:: int  GuiTabBookCtrl::tabMargin

	Spacing to put between individual tab page headers.

.. cpp:member:: GuiTabPosition GuiTabBookCtrl::tabPosition

	Where to place the tab page headers.
