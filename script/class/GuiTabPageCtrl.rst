GuiTabPageCtrl
==============

A single page in a GuiTabBookCtrl.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

A single page in a GuiTabBookCtrl.

Example::

	newGuiTabPageCtrl()
	{
	   fitBook = "1";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiTabPageCtrl::select()

	Select this page in its tab book.

Fields
------


.. cpp:member:: bool  GuiTabPageCtrl::fitBook

	Determines whether to resize this page when it is added to the tab book. If true, the page will be resized according to the tab book extents and tabPosition property.
