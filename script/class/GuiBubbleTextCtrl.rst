GuiBubbleTextCtrl
=================

A single-line text control that displays its text in a multi-line popup when clicked.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

This control acts like a GuiTextCtrl (and inherits from it), when clicked it creates a GuiMLTextCtrl roughly where you clicked with the same text in it. This allows you to have a single line text control which upon clicking will display the entire text contained in a multi-line format.

Example::

	newGuiBubbleTextCtrl(BubbleTextGUI)
	{
	   text = "This is the first sentence. This second sentence can be sized outside of the default single line view, upon clicking this will be displayed in a multi-line format.";
	};

