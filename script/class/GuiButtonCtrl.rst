GuiButtonCtrl
=============

The most widely used button class.

Inherit:
	:doc:`GuiButtonBaseCtrl`

Description
-----------

GuiButtonCtrl renders seperately of, but utilizes all of the functionality of GuiBaseButtonCtrl. This grants GuiButtonCtrl the versatility to be either of the 3 button types.

Example::

	// Create a PushButton GuiButtonCtrl that calls randomFunction when clicked
	%button = newGuiButtonCtrl()
	{
	   profile    = "GuiButtonProfile";
	   buttonType = "PushButton";
	   command    = "randomFunction();";
	};

