Core Controls
=============

Core parts of the Gui System. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/GuiCanvas
	class/GuiConsole
	class/GuiConsoleEditCtrl
	class/GuiControl
	class/GuiControlProfile
	class/GuiCursor
	class/GuiFadeinBitmapCtrl
	class/GuiIconButtonCtrl
	class/GuiListBoxCtrl
	class/GuiMenuBar
	class/GuiMLTextCtrl
	class/GuiMouseEventCtrl
	class/GuiTextCtrl
	class/GuiTextEditSliderBitmapCtrl
	class/GuiTextEditSliderCtrl

Enumeration
-----------

.. cpp:member:: enum  GuiAlignmentType

	:param Left: 
	:param Center: 
	:param Right: 
	:param Top: 
	:param Bottom: 

.. cpp:member:: enum  GuiFontCharset

	:param ANSI: 
	:param SYMBOL: 
	:param SHIFTJIS: 
	:param HANGEUL: 
	:param HANGUL: 
	:param GB2312: 
	:param CHINESEBIG5: 
	:param OEM: 
	:param JOHAB: 
	:param HEBREW: 
	:param ARABIC: 
	:param GREEK: 
	:param TURKISH: 
	:param VIETNAMESE: 
	:param THAI: 
	:param EASTEUROPE: 
	:param RUSSIAN: 
	:param MAC: 
	:param BALTIC: 

.. cpp:member:: enum  GuiHorizontalSizing

	Horizontal sizing behavior of a GuiControl .

	:param right: 
	:param width: 
	:param left: 
	:param center: 
	:param relative: 
	:param windowRelative: 

.. cpp:member:: enum  GuiVerticalSizing

	Vertical sizing behavior of a GuiControl .

	:param bottom: 
	:param height: 
	:param top: 
	:param center: 
	:param relative: 
	:param windowRelative: 

Functions
---------

.. cpp:function:: bool excludeOtherInstance(string appIdentifer)

	Used to exclude/prevent all other instances using the same identifier specified.

	:param appIdentifier: Name of the app set up for exclusive use.

	:return: False if another app is running that specified the same appIdentifier 

.. cpp:function:: string StripMLControlChars(string inString)

	Strip TorqueML control characters from the specified string, returning a 'clean' version.

	:param inString: String to strip TorqueML control characters from.

	:return: Version of the inputted string with all TorqueML characters removed.

	Example::

		// Define the string to strip TorqueML control characters from
		%string = "<font:Arial:24>How Now <color:c43c12>Brown <color:000000>Cow";
		
		// Request the stripped version of the string
		%strippedString = StripMLControlChars(%string);

Variables
---------

.. cpp:member:: GuiControl  $ThisControl

	The control for which a command is currently being evaluated. Only set during 'command' and altCommand callbacks to the control for which the command or altCommand is invoked.
