GuiConsoleEditCtrl
==================

Inherit:
	:doc:`GuiTextEditCtrl`

Description
-----------

Text entry element of a GuiConsole.

Example::

	newGuiConsoleEditCtrl(ConsoleEntry)
	{
	   profile = "ConsoleTextEditProfile";
	   horizSizing = "width";
	   vertSizing = "top";
	   position = "0 462";
	   extent = "640 18";
	   minExtent = "8 8";
	   visible = "1";
	   altCommand = "ConsoleEntry::eval();";
	   helpTag = "0";
	   maxLength = "255";
	   historySize = "40";
	   password = "0";
	   tabComplete = "0";
	   sinkAllKeyEvents = "1";
	   useSiblingScroller = "1";
	};

Fields
------

.. cpp:member:: bool  GuiConsoleEditCtrl::useSiblingScroller

