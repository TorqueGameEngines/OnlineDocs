Platform
========

Enumeration
-----------

.. cpp:member:: enum MBButtons

	Which buttons to display on a message box.

	:param Ok:
	:param OkCancel:
	:param RetryCancel:
	:param SaveDontSave:
	:param SaveDontSaveCancel:

.. cpp:member:: enum MBIcons

	What icon to show on a message box.

	:param Information:
	:param Warning:
	:param Stop:
	:param Question:

.. cpp:member:: enum MBReturnVal

	Return value for messageBox() indicating which button was pressed by the user.

	:param OK:
	:param Cancelled:
	:param Retry:
	:param DontSave:


Functions
---------

.. cpp:function:: bool displaySplashWindow(string path = "art/gui/splash.bmp")

	Display a startup splash window suitable for showing while the engine still starts up.

	Note: This is currently only implemented on Windows.

	:return: True if the splash window could be successfully initialized.

.. cpp:function:: int getRealTime() 	

	:return: Return the current real time in milliseconds. Real time is platform defined; typically time since the computer booted.

.. cpp:function:: int getSimTime() 	

	Sim time is time since the game started.

	:return: Return the current sim time in milliseconds.

.. cpp:function:: bool getWebDeployment() 	

	Test whether Torque is running in web-deployment mode.

	In this mode, Torque will usually run within a browser and certain restrictions apply (e.g. Torque will not be able to enter fullscreen exclusive mode).

	:return: True if Torque is running in web-deployment mode.

.. cpp:function:: void gotoWebPage(string address) 	

	Open the given URL or file in the user's web browser.

	:param address:	The address to open. If this is not prefixed by a protocol specifier ("...://"), then the function checks whether the address refers to a file or directory and if so, prepends "file://" to adress; if the file check fails, "http://" is prepended to address.
	
	Example::

		gotoWebPage( "http://www.garagegames.com" );

.. cpp:function:: bool isDebugBuild() 	

	Test whether the engine has been compiled with TORQUE_DEBUG, i.e. if it includes debugging functionality.

	:return: True if this is a debug build; false otherwise.

.. cpp:function:: bool isShippingBuild() 	

	Test whether the engine has been compiled with TORQUE_SHIPPING, i.e. in a form meant for final release.

	:returns: True if this is a shipping build; false otherwise.

.. cpp:function:: bool isToolBuild() 	

	Test whether the engine has been compiled with TORQUE_TOOLS, i.e. if it includes tool-related functionality.

	:returns: True if this is a tool build; false otherwise.

.. cpp:function:: int messageBox(string	title, string message, MBButtons buttons = MBOkCancel, MBIcons icons = MIInformation)			

	Display a modal message box using the platform's native message box implementation.

	:param title: The title to display on the message box window.
	:param message:	The text message to display in the box.
	:param buttons:	Which buttons to put on the message box.
	:param icons: Which icon to show next to the message.
	:returns: One of $MROK, $MRCancel, $MRRetry, and $MRDontSave identifying the button that the user pressed.

	Example::

		messageBox( "Error", "" );

.. cpp:function:: void playJournal(string filename) 	

	Begin playback of a journal from a specified field.

	:param filename: Name and path of file journal file

.. cpp:function:: void quit()

	Shut down the engine and exit its process. This function cleanly uninitializes the engine and then exits back to the system with a process exit status indicating a clean exit.

.. cpp:function:: void quitWithErrorMessage(string message) 	

	Display an error message box showing the given message and then shut down the engine and exit its process. This function cleanly uninitialized the engine and then exits back to the system with a process exit status indicating an error.

	:param message:	The message to log to the console and show in an error message box.

.. cpp:function:: void saveJournal(string filename) 	

	Save the journal to the specified file.

.. cpp:function:: bool shellExecute(string executable, string args, string directory)

	Launches an outside executable or batch file.

	:param executable: Name of the executable or batch file
	:param args: Optional list of arguments, in string format, to pass to the executable
	:param directory: Optional string containing path to output or shell

Variables
---------

.. cpp:member:: int $MRCancel

	Determines the cancel button press state in a message box.

.. cpp:member:: int $MRDontSave

	Determines the don't save button press state in a message box.

.. cpp:member:: int $MROk

	Determines the ok button press state in a message box.

.. cpp:member:: int $MRRetry

	Determines the retry button press state in a message box.

.. cpp:member:: int $platform::backgroundSleepTime

	Controls processor time usage when the game window is out of focus.

.. cpp:member:: int $platform::timeManagerProcessInterval

	Controls processor time usage when the game window is in focus.
