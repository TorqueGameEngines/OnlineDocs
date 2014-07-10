GuiInputCtrl
============

A control that locks the mouse and reports all keyboard input events to script.

Inherit:
	:doc:`GuiMouseEventCtrl`

Description
-----------

This is useful for implementing custom keyboard handling code, and most commonly used in Torque for a menu that allows a user to remap their in-game controls

Example::

	newGuiInputCtrl(OptRemapInputCtrl)
	{
	   lockMouse = "0";
	   position = "0 0";
	   extent = "64 64";
	   minExtent = "8 8";
	   horizSizing = "center";
	   vertSizing = "bottom";
	   profile = "GuiInputCtrlProfile";
	   visible = "1";
	   active = "1";
	   tooltipProfile = "GuiToolTipProfile";
	   hovertime = "1000";
	   isContainer = "0";
	   canSave = "1";
	   canSaveDynamicFields = "0";
	};

Methods
-------

.. cpp:function:: void GuiInputCtrl::onInputEvent(string device, string action, bool state)

	Callback that occurs when an input is triggered on this control.

	:param device: The device type triggering the input, such as keyboard, mouse, etc
	:param action: The actual event occuring, such as a key or button
	:param state: True if the action is being pressed, false if it is being release
