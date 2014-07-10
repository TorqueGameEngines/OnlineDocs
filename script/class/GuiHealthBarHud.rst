GuiHealthBarHud
===============

A basic health bar. Shows the damage value of the current PlayerObjectType control object.

Inherit:
	:doc:`GuiControl`

Description
-----------

A basic health bar. Shows the damage value of the current PlayerObjectType control object.

This gui displays the damage value of the current PlayerObjectType control object. The gui can be set to pulse if the health value drops below a set value. This control only works if a server connection exists and it's control object is a PlayerObjectType. If either of these requirements is false, the control is not rendered.

Example::

	newGuiHealthBarHud(){
	   fillColor = "0.0 1.0 0.0 1.0"; // Fills with a solid green colorframeColor = "1.0 1.0 1.0 1.0"; // Solid white frame colordamageFillColor = "1.0 0.0 0.0 1.0"; // Fills with a solid red colorpulseRate = "500";
	   pulseThreshold = "0.25";
	   showFill = "true";
	   showFrame = "true";
	   displayEnergy = "false";
	};


Fields
------


.. cpp:member:: ColorF  GuiHealthBarHud::damageFillColor

	As the health bar depletes, this color will represent the health loss amount.

.. cpp:member:: bool  GuiHealthBarHud::displayEnergy

	If true, display the energy value rather than the damage value.

.. cpp:member:: ColorF  GuiHealthBarHud::fillColor

	Standard color for the background of the control.

.. cpp:member:: ColorF  GuiHealthBarHud::frameColor

	Color for the control's frame.

.. cpp:member:: int  GuiHealthBarHud::pulseRate

	Speed at which the control will pulse.

.. cpp:member:: float  GuiHealthBarHud::pulseThreshold

	Health level the control must be under before the control will pulse.

.. cpp:member:: bool  GuiHealthBarHud::showFill

	If true, we draw the background color of the control.

.. cpp:member:: bool  GuiHealthBarHud::showFrame

	If true, we draw the frame of the control.
