GuiTextEditCtrl
===============

A component that places a text entry box on the screen.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

A component that places a text entry box on the screen.

Fonts and sizes are changed using profiles. The text value can be set or entered by a user.

Example::

	newGuiTextEditCtrl(MessageHud_Edit)
	   {
	       text = "Hello World";
	       validate = "validateCommand();"escapeCommand = "escapeCommand();";
	       historySize = "5";
	       tabComplete = "true";
	       deniedSound = "DeniedSoundProfile";
	       sinkAllKeyEvents = "true";
	       password = "true";
	       passwordMask = "*";
	        //Properties not specific to this control have been omitted from this example.
	   };


Methods
-------


.. cpp:function:: void GuiTextEditCtrl::clearSelectedText()

	Unselects all selected text in the control.

	Example::

		// Inform the control to unselect all of its selected text
		%thisGuiTextEditCtrl.clearSelectedText();

.. cpp:function:: void GuiTextEditCtrl::forceValidateText()

	Force a validation to occur.

	Example::

		// Inform the control to force a validation of its text.
		%thisGuiTextEditCtrl.forceValidateText();

.. cpp:function:: int GuiTextEditCtrl::getCursorPos()

	Returns the current position of the text cursor in the control.

	:return: Text cursor position within the control.

	Example::

		// Acquire the cursor position in the control
		%position = %thisGuiTextEditCtrl.getCursorPost();

.. cpp:function:: string GuiTextEditCtrl::getText()

	Acquires the current text displayed in this control.

	:return: The current text within the control.

	Example::

		// Acquire the value of the text control.
		%text = %thisGuiTextEditCtrl.getText();

.. cpp:function:: bool GuiTextEditCtrl::isAllTextSelected()

	Checks to see if all text in the control has been selected.

	:return: True if all text in the control is selected, otherwise false.

	Example::

		// Check to see if all text has been selected or not.
		%allSelected = %thisGuiTextEditCtrl.isAllTextSelected();

.. cpp:function:: void GuiTextEditCtrl::onReturn()

	Called when the 'Return' or 'Enter' key is pressed.

	Example::

		// Return or Enter key was pressed, causing the callback to occur.GuiTextEditCtrl::onReturn(%this)
		   {
		      // Code to run when the onReturn callback occurs
		   }

.. cpp:function:: void GuiTextEditCtrl::onTabComplete(string val)

	Called if tabComplete is true, and the 'tab' key is pressed.

	:param val: Input to mimick the '1' sent by the actual tab key button press.

	Example::

		// Tab key has been pressed, causing the callback to occur.GuiTextEditCtrl::onTabComplete(%this,%val)
		   {
		      //Code to run when the onTabComplete callback occurs
		   }

.. cpp:function:: void GuiTextEditCtrl::onValidate()

	Called whenever the control is validated.

	Example::

		// The control gets validated, causing the callback to occur
		GuiTextEditCtrl::onValidated(%this)
		   {
		      // Code to run when the control is validated
		   }

.. cpp:function:: void GuiTextEditCtrl::selectAllText()

	Selects all text within the control.

	Example::

		// Inform the control to select all of its text.
		%thisGuiTextEditCtrl.selectAllText();

.. cpp:function:: void GuiTextEditCtrl::setCursorPos(int position)

	Sets the text cursor at the defined position within the control.

	:param position: Text position to set the text cursor.

	Example::

		// Define the cursor position
		%position = "12";
		
		// Inform the GuiTextEditCtrl control to place the text cursor at the defined position
		%thisGuiTextEditCtrl.setCursorPos(%position);

.. cpp:function:: void GuiTextEditCtrl::setText(string text)

	Sets the text in the control. Reimplemented from GuiTextCtrl .

	:param text: Text to place in the control.

	Example::

		// Define the text to display
		%text = "Text!"// Inform the GuiTextEditCtrl to display the defined text
		%thisGuiTextEditCtrl.setText(%text);

Fields
------


.. cpp:member:: SFXTrack GuiTextEditCtrl::deniedSound

	If the attempted text cannot be entered, this sound effect will be played.

.. cpp:member:: string  GuiTextEditCtrl::escapeCommand

	Script command to be called when the Escape key is pressed.

.. cpp:member:: int  GuiTextEditCtrl::historySize

	How large of a history buffer to maintain.

.. cpp:member:: bool  GuiTextEditCtrl::password

	If true, all characters entered will be stored in the control, however will display as the character stored in passwordMask.

.. cpp:member:: string  GuiTextEditCtrl::passwordMask

	If 'password' is true, this is the character that will be used to mask the characters in the control.

.. cpp:member:: bool  GuiTextEditCtrl::sinkAllKeyEvents

	If true, every key event will act as if the Enter key was pressed.

.. cpp:member:: bool  GuiTextEditCtrl::tabComplete

	If true, when the 'tab' key is pressed, it will act as if the Enter key was pressed on the control.

.. cpp:member:: string  GuiTextEditCtrl::validate

	Script command to be called when the first validater is lost.
