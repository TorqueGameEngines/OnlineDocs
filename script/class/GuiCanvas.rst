GuiCanvas
=========

A canvas on which rendering occurs.

Inherit:
	:doc:`GuiControl`

Description
-----------

A canvas on which rendering occurs.

What a GUICanvas Can Contain...
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A content control is the top level GuiControl for a screen. This GuiControl will be the parent control for all other GuiControls on that particular screen.

A dialog is essentially another screen, only it gets overlaid on top of the current content control, and all input goes to the dialog. This is most akin to the "Open File" dialog box found in most operating systems. When you choose to open a file, and the "Open File" dialog pops up, you can no longer send input to the application, and must complete or cancel the open file request. Torque keeps track of layers of dialogs. The dialog with the highest layer is on top and will get all the input, unless the dialog is modeless, which is a profile option.

Dirty Rectangles
~~~~~~~~~~~~~~~~

The GuiCanvas is based on dirty regions. Every frame the canvas paints only the areas of the canvas that are 'dirty' or need updating. In most cases, this only is the area under the mouse cursor. This is why if you look in guiCanvas.cc the call to glClear is commented out. What you will see is a black screen, except in the dirty regions, where the screen will be painted normally. If you are making an animated GuiControl you need to add your control to the dirty areas of the canvas.

Methods
-------

.. cpp:function:: Point2I GuiCanvas::clientToScreen(Point2I coordinate)

	Translate a coordinate from canvas window-space to screen-space.

	:param coordinate: The coordinate in window-space.

	:return: The given coordinate translated to screen-space. 

.. cpp:function:: void GuiCanvas::cursorOff()

	Turns on the mouse off.

	Example::

		Canvas.cursorOff();

.. cpp:function:: void GuiCanvas::cursorOn()

	Turns on the mouse cursor.

	Example::

		Canvas.cursorOn();

.. cpp:function:: int GuiCanvas::findFirstMatchingMonitor(string name)

	Find the first monitor index that matches the given name. The actual match algorithm depends on the implementation.

	:param name: The name to search for.

	:return: The number of monitors attached to the system, including the default monoitor. 

.. cpp:function:: int GuiCanvas::getContent()

	Get the GuiControl which is being used as the content.

	:return: ID of current content control 

	Example::

		Canvas.getContent();

.. cpp:function:: Point2I GuiCanvas::getCursorPos()

	Get the current position of the cursor.

	:param param: Description

	:return: Screen coordinates of mouse cursor, in format "X Y" 

	Example::

		%cursorPos = Canvas.getCursorPos();

.. cpp:function:: Point2I GuiCanvas::getExtent()

	Returns the dimensions of the canvas. Reimplemented from GuiControl .

	:return: Width and height of canvas. Formatted as numerical values in a single string "# #" 

	Example::

		%extent = Canvas.getExtent();

.. cpp:function:: string GuiCanvas::getMode(int modeId)

	Gets information on the specified mode of this device.

	:param modeId: Index of the mode to get data from.

	:return: A video mode string given an adapter and mode index.

.. cpp:function:: int GuiCanvas::getModeCount()

	Gets the number of modes available on this device.

	:param param: Description

	:return: The number of video modes supported by the device 

	Example::

		%modeCount = Canvas.getModeCount()

.. cpp:function:: int GuiCanvas::getMonitorCount()

	Gets the number of monitors attached to the system.

	:return: The number of monitors attached to the system, including the default monoitor. 

.. cpp:function:: string GuiCanvas::getMonitorName(int index)

	Gets the name of the requested monitor.

	:param index: The monitor index.

	:return: The name of the requested monitor. 

.. cpp:function:: RectI GuiCanvas::getMonitorRect(int index)

	Gets the region of the requested monitor.

	:param index: The monitor index.

	:return: The rectangular region of the requested monitor. 

.. cpp:function:: int GuiCanvas::getMouseControl()

	Gets the gui control under the mouse.

	:return: ID of the gui control, if one was found. NULL otherwise 

	Example::

		%underMouse = Canvas.getMouseControl();

.. cpp:function:: string GuiCanvas::getVideoMode()

	Gets the current screen mode as a string. The return string will contain 5 values (width, height, fullscreen, bitdepth, refreshRate). You will need to parse out each one for individual use.

	:return: String formatted with screen width, screen height, screen mode, bit depth, and refresh rate. 

	Example::

		%screenWidth = getWord(Canvas.getVideoMode(), 0);
		%screenHeight = getWord(Canvas.getVideoMode(), 1);
		%isFullscreen = getWord(Canvas.getVideoMode(), 2);
		%bitdepth = getWord(Canvas.getVideoMode(), 3);
		%refreshRate = getWord(Canvas.getVideoMode(), 4);

.. cpp:function:: Point2I GuiCanvas::getWindowPosition()

	Get the current position of the platform window associated with the canvas.

	:return: The window position of the canvas in screen-space. 

.. cpp:function:: void GuiCanvas::hideCursor()

	Disable rendering of the cursor.

	Example::

		Canvas.hideCursor();

.. cpp:function:: bool GuiCanvas::isCursorOn()

	Determines if mouse cursor is enabled.

	:return: Returns true if the cursor is on. 

	Example::

		// Is cursor on?if(Canvas.isCursorOn())
		   echo("Canvas cursor is on");

.. cpp:function:: bool GuiCanvas::isCursorShown()

	Determines if mouse cursor is rendering.

	:return: Returns true if the cursor is rendering. 

	Example::

		// Is cursor rendering?if(Canvas.isCursorShown())
		   echo("Canvas cursor is rendering");

.. cpp:function:: bool GuiCanvas::isFullscreen()

	Is this canvas currently fullscreen?

.. cpp:function:: bool GuiCanvas::isMaximized()


.. cpp:function:: bool GuiCanvas::isMinimized()


.. cpp:function:: void GuiCanvas::maximizeWindow()

	maximize this canvas' window.

.. cpp:function:: void GuiCanvas::minimizeWindow()

	minimize this canvas' window.

.. cpp:function:: void GuiCanvas::popDialog(GuiControl ctrl)

	Removes a specific dialog control.

	:param ctrl: Dialog to pop

	Example::

		Canvas.popDialog(RecordingsDlg);

.. cpp:function:: void GuiCanvas::popDialog()

	Removes a dialog at the front most layer.

	Example::

		// Pops whatever is on layer 0
		Canvas.popDialog();

.. cpp:function:: void GuiCanvas::popLayer()

	Removes the top most layer of dialogs.

	Example::

		Canvas.popLayer();

.. cpp:function:: void GuiCanvas::popLayer(S32 layer)

	Removes a specified layer of dialogs.

	:param layer: Number of the layer to pop

	Example::

		Canvas.popLayer(1);

.. cpp:function:: void GuiCanvas::pushDialog(GuiControl ctrl, int layer, bool center)

	Adds a dialog control onto the stack of dialogs.

	:param ctrl: Dialog to add
	:param layer: Layer to put dialog on (optional)
	:param center: True to center dialog on canvas (optional)

	Example::

		Canvas.pushDialog(RecordingsDlg);

.. cpp:function:: void GuiCanvas::renderFront(bool enable)

	This turns on/off front-buffer rendering.

	:param enable: True if all rendering should be done to the front buffer

	Example::

		Canvas.renderFront(false);

.. cpp:function:: void GuiCanvas::repaint(int elapsedMS)

	Force canvas to redraw. If the elapsed time is greater than the time since the last paint then the repaint will be skipped.

	:param elapsedMS: The optional elapsed time in milliseconds.

	Example::

		Canvas.repaint();

.. cpp:function:: void GuiCanvas::reset()

	Reset the update regions for the canvas.

	Example::

		Canvas.reset();

.. cpp:function:: void GuiCanvas::restoreWindow()

	restore this canvas' window.

.. cpp:function:: Point2I GuiCanvas::screenToClient(Point2I coordinate)

	Translate a coordinate from screen-space to canvas window-space.

	:param coordinate: The coordinate in screen-space.

	:return: The given coordinate translated to window-space. 

.. cpp:function:: void GuiCanvas::setContent(GuiControl ctrl)

	Set the content of the canvas to a specified control.

	:param ctrl: ID or name of GuiControl to set content to

	Example::

		Canvas.setContent(PlayGui);

.. cpp:function:: void GuiCanvas::setCursor(GuiCursor cursor)

	Sets the cursor for the canvas.

	:param cursor: Name of the GuiCursor to use

	Example::

		Canvas.setCursor("DefaultCursor");

.. cpp:function:: bool GuiCanvas::setCursorPos(Point2I pos)

	Sets the position of the cursor.

	:param pos: Point, in screenspace for the cursor. Formatted as ("x y")

	Example::

		Canvas.setCursorPos("0 0");

.. cpp:function:: bool GuiCanvas::setCursorPos(F32 posX, F32 posY)

	Sets the position of the cursor.

	:param posX: X-coordinate, in screenspace for the cursor.
	:param posY: Y-coordinate, in screenspace for the cursor.

	Example::

		Canvas.setCursorPos(0,0);

.. cpp:function:: void GuiCanvas::setFocus()

	Claim OS input focus for this canvas' window.

.. cpp:function:: void GuiCanvas::setVideoMode(int width, int height, bool fullscreen)

	Change the video mode of this canvas. This method has the side effect of setting the $pref::Video::mode to the new values.

	:param width: The screen width to set.
	:param height: The screen height to set.
	:param fullscreen: Specify true to run fullscreen or false to run in a window
	:param bitDepth: [optional] The desired bit-depth. Defaults to the current setting. This parameter is ignored if you are running in a window.
	:param refreshRate: [optional] The desired refresh rate. Defaults to the current setting. This parameter is ignored if you are running in a window
	:param antialiasLevel: [optional] The level of anti-aliasing to apply 0 = none

.. cpp:function:: void GuiCanvas::setWindowPosition(Point2I position)

	Set the position of the platform window associated with the canvas.

	:param position: The new position of the window in screen-space.

.. cpp:function:: void GuiCanvas::setWindowTitle(string newTitle)

	Change the title of the OS window.

	:param newTitle: String containing the new name

	Example::

		Canvas.setWindowTitle("Documentation Rocks!");

.. cpp:function:: void GuiCanvas::showCursor()

	Enable rendering of the cursor.

	Example::

		Canvas.showCursor();

.. cpp:function:: void GuiCanvas::toggleFullscreen()

	toggle canvas from fullscreen to windowed mode or back.

	Example::

		// If we are in windowed mode, the following will put is in fullscreen
		Canvas.toggleFullscreen();

Fields
------


.. cpp:member:: bool  GuiCanvas::alwaysHandleMouseButtons

	Deal with mouse buttons, even if the cursor is hidden.

.. cpp:member:: int  GuiCanvas::numFences

	The number of GFX fences to use.
