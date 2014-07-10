GuiMessageVectorCtrl
====================

A chat HUD control that displays messages from a MessageVector.

Inherit:
	:doc:`GuiControl`

Description
-----------

A chat HUD control that displays messages from a MessageVector.

This renders messages from a MessageVector; the important thing here is that the MessageVector holds all the messages we care about, while we can destroy and create these GUI controls as needed.

Example::

	// Declare ChatHud, which is what will display the actual chat from a MessageVectornewGuiMessageVectorCtrl(ChatHud) {
	   profile = "ChatHudMessageProfile";
	   horizSizing = "width";
	   vertSizing = "height";
	   position = "1 1";
	   extent = "252 16";
	   minExtent = "8 8";
	   visible = "1";
	   helpTag = "0";
	   lineSpacing = "0";
	   lineContinuedIndex = "10";
	   matchColor = "0 0 255 255";
	   maxColorIndex = "5";
	};
	
	// All messages are stored in this HudMessageVector, the actual// MainChatHud only displays the contents of this vector.newMessageVector(HudMessageVector);
	
	// Attach the MessageVector to the chat control
	chatHud.attach(HudMessageVector);

Methods
-------

.. cpp:function:: bool GuiMessageVectorCtrl::attach(MessageVector item)

	Push a line onto the back of the list.

	:param item: The GUI element being pushed into the control

	:return: Value 

	Example::

		// All messages are stored in this HudMessageVector, the actual
		// MainChatHud only displays the contents of this vector.
		newMessageVector(HudMessageVector);
		
		// Attach the MessageVector to the chat control
		chatHud.attach(HudMessageVector);

.. cpp:function:: void GuiMessageVectorCtrl::detach()

	Stop listing messages from the MessageVector previously attached to, if any. Detailed description

	:param param: Description

	Example::

		// Deatch the MessageVector from HudMessageVector
		// HudMessageVector will no longer render the text
		chatHud.detach();

Fields
------

.. cpp:member:: string  GuiMessageVectorCtrl::allowedMatches [16]


.. cpp:member:: int  GuiMessageVectorCtrl::lineContinuedIndex


.. cpp:member:: int  GuiMessageVectorCtrl::lineSpacing


.. cpp:member:: ColorI  GuiMessageVectorCtrl::matchColor


.. cpp:member:: int  GuiMessageVectorCtrl::maxColorIndex

