GuiSpeedometerHud
=================

Displays the speed of the current Vehicle based control object.

Inherit:
	:doc:`GuiBitmapCtrl`

Description
-----------

This control only works if a server connection exists, and its control object is a Vehicle derived class. If either of these requirements is false, the control is not rendered.
The control renders the speedometer needle as a colored quad, rotated to indicate the Vehicle speed as determined by the minAngle, maxAngle, and maxSpeed properties. This control is normally placed on top of a GuiBitmapCtrl representing the speedometer dial.

Example::

	newGuiSpeedometerHud()
	{
	   maxSpeed = "100";
	   minAngle = "215";
	   maxAngle = "0";
	   color = "1 0.3 0.3 1";
	   center = "130 123";
	   length = "100";
	   width = "2";
	   tail = "0";
	   //Properties not specific to this control have been omitted from this example.
	};


Fields
------


.. cpp:member:: Point2F  GuiSpeedometerHud::center

	Center of the needle, offset from the GuiSpeedometerHud control top left corner.

.. cpp:member:: ColorF  GuiSpeedometerHud::color

	Color of the needle.

.. cpp:member:: float  GuiSpeedometerHud::length

	Length of the needle from center to end.

.. cpp:member:: float  GuiSpeedometerHud::maxAngle

	Angle (in radians) of the needle when the Vehicle speed is gt = maxSpeed. An angle of 0 points right, 90 points up etc).

.. cpp:member:: float  GuiSpeedometerHud::maxSpeed

	Maximum Vehicle speed (in Torque units per second) to represent on the speedo ( Vehicle speeds greater than this are clamped to maxSpeed).

.. cpp:member:: float  GuiSpeedometerHud::minAngle

	Angle (in radians) of the needle when the Vehicle speed is 0. An angle of 0 points right, 90 points up etc).

.. cpp:member:: float  GuiSpeedometerHud::tail

	Length of the needle from center to tail.

.. cpp:member:: float  GuiSpeedometerHud::width

	Width of the needle.
