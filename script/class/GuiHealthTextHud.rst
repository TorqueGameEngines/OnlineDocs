GuiHealthTextHud
================

Shows the health or energy value of the current PlayerObjectType control object.

Inherit:
	:doc:`GuiControl`

Description
-----------

Shows the health or energy value of the current PlayerObjectType control object.

This gui can be configured to display either the health or energy value of the current Player Object. It can use an alternate display color if the health or drops below a set value. It can also be set to pulse if the health or energy drops below a set value. This control only works if a server connection exists and it's control object is a PlayerObjectType. If either of these requirements is false, the control is not rendered.

Example::

	newGuiHealthTextHud(){
	   fillColor = "0.0 0.0 0.0 0.5"; // Fills with a transparent black colorframeColor = "1.0 1.0 1.0 1.0"; // Solid white frame colortextColor = "0.0 1.0 0.0 1.0"// Solid green text colorwarningColor = "1.0 0.0 0.0 1.0"; // Solid red color, used when damagedshowFill = "true";
	   showFrame = "true";
	   showTrueValue = "false";
	   showEnergy = "false";
	   warnThreshold = "50";
	   pulseThreshold = "25";
	   pulseRate = "500";
	   profile = "GuiBigTextProfile";
	};


Fields
------


.. cpp:member:: ColorF  GuiHealthTextHud::fillColor

	Color for the background of the control.

.. cpp:member:: ColorF  GuiHealthTextHud::frameColor

	Color for the control's frame.

.. cpp:member:: int  GuiHealthTextHud::pulseRate

	Speed at which the control will pulse.

.. cpp:member:: float  GuiHealthTextHud::pulseThreshold

	Health level at which to begin pulsing.

.. cpp:member:: bool  GuiHealthTextHud::showEnergy

	If true, display the energy value rather than the damage value.

.. cpp:member:: bool  GuiHealthTextHud::showFill

	If true, draw the background.

.. cpp:member:: bool  GuiHealthTextHud::showFrame

	If true, draw the frame.

.. cpp:member:: bool  GuiHealthTextHud::showTrueValue

	If true, we don't hardcode maxHealth to 100.

.. cpp:member:: ColorF  GuiHealthTextHud::textColor

	Color for the text on this control.

.. cpp:member:: ColorF  GuiHealthTextHud::warningColor

	Color for the text when health is low.

.. cpp:member:: float  GuiHealthTextHud::warnThreshold

	The health level at which to use the warningColor.
