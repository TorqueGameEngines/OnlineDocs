GuiSeparatorCtrl
================

Inherit:
	:doc:`GuiControl`

Description
-----------

A control that renders a horizontal or vertical separator with an optional text label (horizontal only).

Example::

	newGuiSeparatorCtrl()
	{
	   profile = "GuiDefaultProfile";
	   position = "505 0";
	   extent = "10 17";
	   minExtent = "10 17";
	   canSave = "1";
	   visible = "1";
	   horizSizing = "left";
	};


Fields
------


.. cpp:member:: int  GuiSeparatorCtrl::borderMargin


.. cpp:member:: string  GuiSeparatorCtrl::caption

	Optional text label to display.

.. cpp:member:: bool  GuiSeparatorCtrl::invisible


.. cpp:member:: int  GuiSeparatorCtrl::leftMargin

	Left margin of text label.

.. cpp:member:: GuiSeparatorType GuiSeparatorCtrl::type

	Orientation of separator.
