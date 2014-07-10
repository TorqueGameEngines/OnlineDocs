GuiMLTextCtrl
=============

A text control that uses the Gui Markup Language ('ML') tags to dynamically change the text.

Inherit:
	:doc:`GuiControl`

Description
-----------

Example of dynamic changes include colors, styles, and/or hyperlinks. These changes can occur without having to use separate text controls with separate text profiles.

Example::

	newGuiMLTextCtrl(CenterPrintText)
	{
	    lineSpacing = "2";
	    allowColorChars = "0";
	    maxChars = "-1";
	    deniedSound = "DeniedSoundProfile";
	    text = "The Text for This Control.";
	    useURLMouseCursor = "true";
	    //Properties not specific to this control have been omitted from this example.
	};


Methods
-------


.. cpp:function:: void GuiMLTextCtrl::addText(string text, bool reformat)

	Appends the text in the control with additional text. Also .

	:param text: New text to append to the existing text.
	:param reformat: If true, the control will also be visually reset (defaults to true).

	Example::

		// Define new text to add
		%text = "New Text to Add";
		
		// Set reformat boolean
		%reformat = "true";
		
		// Inform the control to add the new text
		%thisGuiMLTextCtrl.addText(%text,%reformat);

.. cpp:function:: void GuiMLTextCtrl::forceReflow()

	Forces the text control to reflow the text after new text is added, possibly resizing the control.

	Example::

		// Define new text to add
		%newText = "BACON!";
		
		// Add the new text to the control
		%thisGuiMLTextCtrl.addText(%newText);
		
		// Inform the GuiMLTextCtrl object to force a reflow to ensure the added text fits properly.
		%thisGuiMLTextCtrl.forceReflow();

.. cpp:function:: string GuiMLTextCtrl::getText()

	Returns the text from the control, including TorqueML characters.

	:return: Text string displayed in the control, including any TorqueML characters.

	Example::

		// Get the text displayed in the control
		%controlText = %thisGuiMLTextCtrl.getText();

.. cpp:function:: void GuiMLTextCtrl::onResize(string width, string maxY)

	Called whenever the control size changes.

	:param width: The new width value for the control
	:param maxY: The current maximum allowed Y value for the control

	Example::

		// Control size changed, causing the callback to occur.GuiMLTextCtrl::onResize(%this,%width,%maxY)
		   {
		      // Code to call when the control size changes
		   }

.. cpp:function:: void GuiMLTextCtrl::onURL(string url)

	Called whenever a URL was clicked on within the control.

	:param url: The URL address that was clicked on.

	Example::

		// A URL address was clicked on in the control, causing the callback to occur.
		GuiMLTextCtrl::onUrl(%this,%url)
		   {
		      // Code to run whenever a URL was clicked on
		   }

.. cpp:function:: void GuiMLTextCtrl::scrollToBottom()

	Scroll to the bottom of the text.

	Example::

		// Inform GuiMLTextCtrl object to scroll to its bottom
		%thisGuiMLTextCtrl.scrollToBottom();

.. cpp:function:: void GuiMLTextCtrl::scrollToTag(int tagID)

	Scroll down to a specified tag. Detailed description

	:param tagID: TagID to scroll the control to

	Example::

		// Define the TagID we want to scroll the control to
		%tagId = "4";
		
		// Inform the GuiMLTextCtrl to scroll to the defined TagID
		%thisGuiMLTextCtrl.scrollToTag(%tagId);

.. cpp:function:: void GuiMLTextCtrl::scrollToTop(int param1, int param2)

	Scroll to the top of the text.

	Example::

		// Inform GuiMLTextCtrl object to scroll to its top
		%thisGuiMLTextCtrl.scrollToTop();

.. cpp:function:: void GuiMLTextCtrl::setAlpha(float alphaVal)

	Sets the alpha value of the control.

	:param alphaVal: n - 1.0 floating value for the alpha

	Example::

		// Define the alphe value
		%alphaVal = "0.5";
		
		// Inform the control to update its alpha value.
		%thisGuiMLTextCtrl.setAlpha(%alphaVal);

.. cpp:function:: bool GuiMLTextCtrl::setCursorPosition(int newPos)

	Change the text cursor's position to a new defined offset within the text in the control.

	:param newPos: Offset to place cursor.

	:return: Returns true if the cursor position moved, or false if the position was not changed.

	Example::

		// Define cursor offset position
		%position = "23";
		
		// Inform the GuiMLTextCtrl object to move the cursor to the new position.
		%thisGuiMLTextCtrl.setCursorPosition(%position);

.. cpp:function:: void GuiMLTextCtrl::setText(string text)

	Set the text contained in the control.

	:param text: The text to display in the control.

	Example::

		// Define the text to display
		%text = "Nifty Control Text";
		
		// Set the text displayed within the control
		%thisGuiMLTextCtrl.setText(%text);

Fields
------


.. cpp:member:: bool  GuiMLTextCtrl::allowColorChars

	If true, the control will allow characters to have unique colors.

.. cpp:member:: SFXTrack GuiMLTextCtrl::deniedSound

	If the text will not fit in the control, the deniedSound is played.

.. cpp:member:: int  GuiMLTextCtrl::lineSpacing

	The number of blank pixels to place between each line.

.. cpp:member:: int  GuiMLTextCtrl::maxChars

	Maximum number of characters that the control will display.

.. cpp:member:: caseString  GuiMLTextCtrl::text

	Text to display in this control.

.. cpp:member:: bool  GuiMLTextCtrl::useURLMouseCursor

	If true, the mouse cursor will turn into a hand cursor while over a link in the text. This is dependant on the markup language used by the GuiMLTextCtrl
