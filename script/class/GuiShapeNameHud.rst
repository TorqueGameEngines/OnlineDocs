GuiShapeNameHud
===============

Displays name and damage of ShapeBase objects in its bounds. Must be a child of a GuiTSCtrl and a server connection must be present.

Inherit:
	:doc:`GuiControl`

Description
-----------

This control displays the name and damage value of all named ShapeBase objects on the client. The name and damage of objects within the control's display area are overlayed above the object.

This GUI control must be a child of a TSControl, and a server connection and control object must be present. This is a stand-alone control and relies only on the standard base GuiControl.

Example::

	newGuiShapeNameHud(){
	   fillColor = "0.0 1.0 0.0 1.0"; // Fills with a solid green colorframeColor = "1.0 1.0 1.0 1.0"; // Solid white frame colortextColor = "1.0 1.0 1.0 1.0"; // Solid white text ColorshowFill = "true";
	   showFrame = "true";
	   labelFillColor = "0.0 1.0 0.0 1.0"; // Fills with a solid green colorlabelFrameColor = "1.0 1.0 1.0 1.0"; // Solid white frame colorshowLabelFill = "true";
	   showLabelFrame = "true";
	   verticalOffset = "0.15";
	   distanceFade = "15.0";
	};


Fields
------


.. cpp:member:: float  GuiShapeNameHud::distanceFade

	Visibility distance (how far the player must be from the ShapeBase object in focus) for this control to render.

.. cpp:member:: ColorF  GuiShapeNameHud::fillColor

	Standard color for the background of the control.

.. cpp:member:: ColorF  GuiShapeNameHud::frameColor

	Color for the control's frame.

.. cpp:member:: ColorF  GuiShapeNameHud::labelFillColor

	Color for the background of each shape name label.

.. cpp:member:: ColorF  GuiShapeNameHud::labelFrameColor

	Color for the frames around each shape name label.

.. cpp:member:: Point2I  GuiShapeNameHud::labelPadding

	The padding (in pixels) between the label text and the frame.

.. cpp:member:: bool  GuiShapeNameHud::showFill

	If true, we draw the background color of the control.

.. cpp:member:: bool  GuiShapeNameHud::showFrame

	If true, we draw the frame of the control.

.. cpp:member:: bool  GuiShapeNameHud::showLabelFill

	If true, we draw a background for each shape name label.

.. cpp:member:: bool  GuiShapeNameHud::showLabelFrame

	If true, we draw a frame around each shape name label.

.. cpp:member:: ColorF  GuiShapeNameHud::textColor

	Color for the text on this control.

.. cpp:member:: float  GuiShapeNameHud::verticalOffset

	Amount to vertically offset the control in relation to the ShapeBase object in focus.
