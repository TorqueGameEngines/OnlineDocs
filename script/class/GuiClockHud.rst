GuiClockHud
===========

Basic HUD clock. Displays the current simulation time offset from some base.

Inherit:
	:doc:`GuiControl`

Description
-----------

Basic HUD clock. Displays the current simulation time offset from some base.

Example::

	newGuiClockHud(){
	   fillColor = "0.0 1.0 0.0 1.0"; // Fills with a solid green colorframeColor = "1.0 1.0 1.0 1.0"; // Solid white frame colortextColor = "1.0 1.0 1.0 1.0"; // Solid white text ColorshowFill = "true";
	   showFrame = "true";
	};


Methods
-------


.. cpp:function:: float GuiClockHud::getTime()

	Returns the current time, in seconds.

	:return: timeInseconds Current time, in seconds 

	Example::

		// Get the current time from the GuiClockHud control
		%timeInSeconds = %guiClockHud.getTime();

.. cpp:function:: void GuiClockHud::setReverseTime(float timeInSeconds)

	Sets a time for a countdown clock. Setting the time like this will cause the clock to count backwards from the specified time.

	:param timeInSeconds: Time to set the clock, in seconds (IE: 00:02 would be 120)

.. cpp:function:: void GuiClockHud::setTime(float timeInSeconds)

	Sets the current base time for the clock.

	:param timeInSeconds: Time to set the clock, in seconds (IE: 00:02 would be 120)

	Example::

		// Define the time, in seconds
		%timeInSeconds = 120;
		
		// Change the time on the GuiClockHud control
		%guiClockHud.setTime(%timeInSeconds);

Fields
------


.. cpp:member:: ColorF  GuiClockHud::fillColor

	Standard color for the background of the control.

.. cpp:member:: ColorF  GuiClockHud::frameColor

	Color for the control's frame.

.. cpp:member:: bool  GuiClockHud::showFill

	If true, draws a background color behind the control.

.. cpp:member:: bool  GuiClockHud::showFrame

	If true, draws a frame around the control.

.. cpp:member:: ColorF  GuiClockHud::textColor

	Color for the text on this control.
