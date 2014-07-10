GuiMLTextEditCtrl
=================

A text entry control that accepts the Gui Markup Language ('ML') tags and multiple lines.

Inherit:
	:doc:`GuiMLTextCtrl`

Description
-----------

A text entry control that accepts the Gui Markup Language ('ML') tags and multiple lines.

Example::

	newGuiMLTextEditCtrl()
	   {
	      lineSpacing = "2";
	      allowColorChars = "0";
	      maxChars = "-1";
	      deniedSound = "DeniedSoundProfile";
	      text = "";
	      escapeCommand = "onEscapeScriptFunction();";
	     //Properties not specific to this control have been omitted from this example.
	   };


Fields
------


.. cpp:member:: string  GuiMLTextEditCtrl::escapeCommand

	Script function to run whenever the 'escape' key is pressed when this control is in focus.
