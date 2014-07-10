GuiTextEditSliderCtrl
=====================

GUI Control which displays a numerical value which can be increased or decreased using a pair of arrows.

Inherit:
	:doc:`GuiTextEditCtrl`

Description
-----------

GUI Control which displays a numerical value which can be increased or decreased using a pair of arrows.

Example::

	newGuiTextEditSliderCtrl()
	{
	   format = "%3.2f";
	   range = "-1e+03 1e+03";
	   increment = "0.1";
	   focusOnMouseWheel = "0";
	   //Properties not specific to this control have been omitted from this example.
	};


Fields
------


.. cpp:member:: bool  GuiTextEditSliderCtrl::focusOnMouseWheel

	If true, the control will accept giving focus to the user when the mouse wheel is used.

.. cpp:member:: string  GuiTextEditSliderCtrl::format

	Character format type to place in the control.

.. cpp:member:: float  GuiTextEditSliderCtrl::increment

	How far to increment the slider on each step.

.. cpp:member:: Point2F  GuiTextEditSliderCtrl::range

	Maximum vertical and horizontal range to allow in the control.
