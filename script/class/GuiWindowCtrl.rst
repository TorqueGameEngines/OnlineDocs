GuiWindowCtrl
=============

A window with a title bar and an optional set of buttons.

Inherit:
	:doc:`GuiContainer`

Description
-----------

The GuiWindowCtrl class implements windows that can be freely placed within the render window. Additionally, the windows can be resized and maximized/minimized.

Example::

	newGuiWindowCtrl( MyWindow )
	{
	   text = "My Window"; // The text that is displayed on the title bar.
	   resizeWidth = true; // Allow horizontal resizing by user via mouse.
	   resizeHeight = true; // Allow vertical resizing by user via mouse.
	   canClose = true; // Display a close button in the title bar.
	   canMinimize = true; // Display a minimize button in the title bar.
	   canMaximize = true; // Display a maximize button in the title bar.
	};


Methods
-------

.. cpp:function:: static void GuiWindowCtrl::attach(GuiWindowCtrl bottomWindow, GuiWindowCtrl topWindow)

	Attach bottomWindow to  so that bottomWindow moves along with topWindow when it is dragged.

	:param bottomWindow: 
	:param topWindow: 

.. cpp:function:: void GuiWindowCtrl::attachTo(GuiWindowCtrl window)


.. cpp:function:: void GuiWindowCtrl::onClose()

	Called when the close button has been pressed.

.. cpp:function:: void GuiWindowCtrl::onCollapse()

	Called when the window is collapsed by clicking its title bar.

.. cpp:function:: void GuiWindowCtrl::onMaximize()

	Called when the window has been maximized.

.. cpp:function:: void GuiWindowCtrl::onMinimize()

	Called when the window has been minimized.

.. cpp:function:: void GuiWindowCtrl::onRestore()

	Called when the window is restored from minimized, maximized, or collapsed state.

.. cpp:function:: void GuiWindowCtrl::selectWindow()

	Bring the window to the front.

.. cpp:function:: void GuiWindowCtrl::setCollapseGroup(bool state)

	Set the window's collapsing state.

.. cpp:function:: void GuiWindowCtrl::toggleCollapseGroup()

	Toggle the window collapsing.

Fields
------

.. cpp:member:: bool  GuiWindowCtrl::canClose

	Whether the window has a close button.

.. cpp:member:: bool  GuiWindowCtrl::canCollapse

	Whether the window can be collapsed by clicking its title bar.

.. cpp:member:: bool  GuiWindowCtrl::canMaximize

	Whether the window has a maximize button.

.. cpp:member:: bool  GuiWindowCtrl::canMinimize

	Whether the window has a minimize button.

.. cpp:member:: bool  GuiWindowCtrl::canMove

	Whether the window can be moved by dragging its titlebar.

.. cpp:member:: string  GuiWindowCtrl::closeCommand

	Script code to execute when the window is closed.

.. cpp:member:: bool  GuiWindowCtrl::edgeSnap

	If true, the window will snap to the edges of other windows when moved close to them.

.. cpp:member:: bool  GuiWindowCtrl::resizeHeight

	Whether the window can be resized vertically.

.. cpp:member:: bool  GuiWindowCtrl::resizeWidth

	Whether the window can be resized horizontally.

.. cpp:member:: string  GuiWindowCtrl::text

	Text label to display in titlebar.
