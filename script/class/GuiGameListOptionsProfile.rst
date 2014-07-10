GuiGameListOptionsProfile
=========================

A GuiControlProfile with additional fields specific to GuiGameListOptionsCtrl.

Inherit:
	:doc:`GuiGameListMenuProfile`

Description
-----------

A GuiControlProfile with additional fields specific to GuiGameListOptionsCtrl.

Example::

	newGuiGameListOptionsProfile()
	{
	   columnSplit = "100";
	   rightPad = "4";
	   //Properties not specific to this control have been omitted from this example.
	};


Fields
------


.. cpp:member:: int  GuiGameListOptionsProfile::columnSplit

	Padding between the leftmost edge of the control, and the row's left arrow.

.. cpp:member:: int  GuiGameListOptionsProfile::rightPad

	Padding between the rightmost edge of the control and the row's right arrow.
