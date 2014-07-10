GuiRadioCtrl
============

A button based around the radio concept.

Inherit:
	:doc:`GuiCheckBoxCtrl`

Description
-----------

GuiRadioCtrl's functionality is based around GuiButtonBaseCtrl's ButtonTypeRadio type.

A button control with a radio box and a text label. This control is used in groups where multiple radio buttons present a range of options out of which one can be chosen. A radio button automatically signals its siblings when it is toggled on.

Example::

	// Create a GuiCheckBoxCtrl that calls randomFunction with its current value when clicked.
	%radio = newGuiRadioCtrl()
	{
	   profile = "GuiRadioProfile";
	};

