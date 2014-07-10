GuiConsole
==========

The on-screen, in-game console.

Inherit:
	:doc:`GuiArrayCtrl`

Description
-----------

Calls getLog() to get the on-screen console entries, then renders them as needed.

Example::

	newGuiConsole()
	      {
	         //Properties not specific to this control have been omitted from this example.
	      };


Methods
-------


.. cpp:function:: void GuiConsole::onMessageSelected(ConsoleLogEntry::Level level, string message)

	Called when a message in the log is clicked.

	:param level: Diagnostic level of the message.
	:param message: Message text.
