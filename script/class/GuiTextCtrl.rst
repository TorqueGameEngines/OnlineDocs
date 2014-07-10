GuiTextCtrl
===========

GUI control object this displays a single line of text, without TorqueML.

Inherit:
	:doc:`GuiContainer`

Description
-----------

GUI control object this displays a single line of text, without TorqueML.

Example::

	newGuiTextCtrl()
	   {
	      text = "Hello World";
	      textID = ""STR_HELLO"";
	      maxlength = "1024";
	       //Properties not specific to this control have been omitted from this example.
	   };


Methods
-------


.. cpp:function:: void GuiTextCtrl::setText(string text)

	Sets the text in the control. Reimplemented in GuiTextEditCtrl , and GuiPopUpMenuCtrlEx .

	:param text: Text to display in the control.

	Example::

		// Set the text to show in the control
		%text = "Gideon - Destroyer of World";
		
		// Inform the GuiTextCtrl control to change its text to the defined value
		%thisGuiTextCtrl.setText(%text);

.. cpp:function:: void GuiTextCtrl::setTextID(string textID)

	Maps the text ctrl to a variable used in localization, rather than raw text.

	:param textID: Name of variable text should be mapped to

	Example::

		// Inform the GuiTextCtrl control of the textID to use
		%thisGuiTextCtrl.setTextID("STR_QUIT");

Fields
------


.. cpp:member:: int  GuiTextCtrl::maxLength

	Defines the maximum length of the text. The default is 1024.

.. cpp:member:: caseString  GuiTextCtrl::text

	The text to show on the control.

.. cpp:member:: string  GuiTextCtrl::textID

	Maps the text of this control to a variable used in localization, rather than raw text.
