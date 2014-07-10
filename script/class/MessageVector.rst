MessageVector
=============

Store a list of chat messages.

Inherit:
	:doc:`SimObject`

Description
-----------

This is responsible for managing messages which appear in the chat HUD, not the actual control rendered to the screen

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


.. cpp:function:: void MessageVector::clear()

	Clear all messages in the vector.

	Example::

		HudMessageVector.clear();

.. cpp:function:: bool MessageVector::deleteLine(int deletePos)

	Delete the line at the specified position.

	:param deletePos: Position in the vector containing the line to be deleted

	:return: False if deletePos is greater than the number of lines in the current vector 

	Example::

		// Delete the first line (index 0) in the vector...
		HudMessageVector.deleteLine(0);

.. cpp:function:: void MessageVector::dump(string filename)

	Dump the message vector to a file without a header.

	:param filename: Name and path of file to dump text to.

	Example::

		// Dump the entire chat log to a text file
		HudMessageVector.dump("./chatLog.txt");

.. cpp:function:: void MessageVector::dump(string filename, string header)

	Dump the message vector to a file with a header.

	:param filename: Name and path of file to dump text to.
	:param header: Prefix information for write out

	Example::

		// Arbitrary header data
		%headerInfo = "Ars Moriendi Chat Log";
		
		// Dump the entire chat log to a text file
		HudMessageVector.dump("./chatLog.txt", %headerInfo);

.. cpp:function:: int MessageVector::getLineIndexByTag(int tag)

	Scan through the vector, returning the line number of the first line that matches the specified tag; else returns -1 if no match was found.

	:param tag: Numerical value assigned to a message when it was added or inserted

	:return: Line with matching tag, other wise -1 

	Example::

		// Locate a line of text tagged with the value "1", then delete it.
		%taggedLine = HudMessageVector.getLineIndexByTag(1);
		HudMessageVector.deleteLine(%taggedLine);

.. cpp:function:: int MessageVector::getLineTag(int pos)

	Get the tag of a specified line.

	:param pos: Position in vector to grab tag from

	:return: Tag value of a given line, if the position is greater than the number of lines return 0 

	Example::

		// Remove all lines that do not have a tag value of 1.while( HudMessageVector.getNumLines())
		{
		   %tag = HudMessageVector.getLineTag(1);
		   if(%tag != 1)
		      %tag.delete();
		   HudMessageVector.popFrontLine();
		}

.. cpp:function:: string MessageVector::getLineText(int pos)

	Get the text at a specified line.

	:param pos: Position in vector to grab text from

	:return: Text at specified line, if the position is greater than the number of lines return "" 

	Example::

		// Print a line of text at position 1.
		%text = HudMessageVector.getLineText(1);
		echo(%text);

.. cpp:function:: string MessageVector::getLineTextByTag(int tag)

	Scan through the lines in the vector, returning the first line that has a matching tag.

	:param tag: Numerical value assigned to a message when it was added or inserted

	:return: Text from a line with matching tag, other wise "" 

	Example::

		// Locate text in the vector tagged with the value "1", then print it
		%taggedText = HudMessageVector.getLineTextByTag(1);
		echo(%taggedText);

.. cpp:function:: int MessageVector::getNumLines()

	Get the number of lines in the vector.

	Example::

		// Find out how many lines have been stored in HudMessageVector
		%chatLines = HudMessageVector.getNumLines();
		echo(%chatLines);

.. cpp:function:: bool MessageVector::insertLine(int insertPos, string msg, int tag)

	Push a line onto the back of the list.

	:param msg: Text that makes up the message
	:param tag: Numerical value associated with this message, useful for searching.

	:return: False if insertPos is greater than the number of lines in the current vector 

	Example::

		// Add the message...
		HudMessageVector.insertLine(1, "Hello World", 0);

.. cpp:function:: bool MessageVector::popBackLine()

	Pop a line from the back of the list; destroys the line.

	:return: False if there are no lines to pop (underflow), true otherwise 

	Example::

		HudMessageVector.popBackLine();

.. cpp:function:: bool MessageVector::popFrontLine()

	Pop a line from the front of the vector, destroying the line.

	:return: False if there are no lines to pop (underflow), true otherwise 

	Example::

		HudMessageVector.popFrontLine();

.. cpp:function:: void MessageVector::pushBackLine(string msg, int tag)

	Push a line onto the back of the list.

	:param msg: Text that makes up the message
	:param tag: Numerical value associated with this message, useful for searching.

	Example::

		// Add the message...
		HudMessageVector.pushBackLine("Hello World", 0);

.. cpp:function:: void MessageVector::pushFrontLine(string msg, int tag)

	Push a line onto the front of the vector.

	:param msg: Text that makes up the message
	:param tag: Numerical value associated with this message, useful for searching.

	Example::

		// Add the message...
		HudMessageVector.pushFrontLine("Hello World", 0);
