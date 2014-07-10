GuiMouseEventCtrl
=================

Used to overlaps a 'hot region' where you want to catch inputs with and have specific events occur based on individual callbacks.

Inherit:
	:doc:`GuiControl`

Description
-----------

Mouse event callbacks supported by this control are: onMouseUp, onMouseDown, onMouseMove, onMouseDragged, onMouseEnter, onMouseLeave, onRightMouseDown, onRightMouseUp and onRightMouseDragged.

Example::

	newGuiMouseEventCtrl()
	{
	   lockMouse = "0";
	   //Properties not specific to this control have been omitted from this example.
	};


Methods
-------

.. cpp:function:: void GuiMouseEventCtrl::onMouseDown(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse is pressed down while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse was pressed down in this control, causing the callback
		GuiMouseEventCtrl::onMouseDown(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onMouseDragged(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse is dragged while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse was dragged in this control, causing the callback
		GuiMouseEventCtrl::onMouseDragged(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onMouseEnter(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse enters this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse entered this control, causing the callback
		GuiMouseEventCtrl::onMouseEnter(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onMouseLeave(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse leaves this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse left this control, causing the callback
		GuiMouseEventCtrl::onMouseLeave(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onMouseMove(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse is moved (without dragging) while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse was moved in this control, causing the callback
		GuiMouseEventCtrl::onMouseMove(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onMouseUp(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse is released while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Mouse was released in this control, causing the callback
		GuiMouseEventCtrl::onMouseUp(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onRightMouseDown(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the right mouse button is pressed while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Right mouse button was pressed in this control, causing the callback
		GuiMouseEventCtrl::onRightMouseDown(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onRightMouseDragged(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the mouse is dragged in this control while the right mouse button is pressed. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Right mouse button was dragged in this control, causing the callback
		GuiMouseEventCtrl::onRightMouseDragged(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

.. cpp:function:: void GuiMouseEventCtrl::onRightMouseUp(U8 modifier, Point2I mousePoint, U8 mouseClickCount)

	Callback that occurs whenever the right mouse button is released while in this control. $EventModifier::RSHIFT $EventModifier::SHIFT $EventModifier::LCTRL $EventModifier::RCTRL $EventModifier::CTRL $EventModifier::CTRL $EventModifier::RALT $EventModifier::ALT

	:param modifier: Key that was pressed during this callback. Values are:
	:param mousePoint: X/Y location of the mouse point
	:param mouseClickCount: How many mouse clicks have occured for this event

	Example::

		// Right mouse button was released in this control, causing the callback
		GuiMouseEventCtrl::onRightMouseUp(%this,%modifier,%mousePoint,%mouseClickCount)
		{
		   // Code to call when a mouse event occurs.
		}

Fields
------

.. cpp:member:: bool  GuiMouseEventCtrl::lockMouse

	Whether the control should lock the mouse between up and down button events.
