GuiCrossHairHud
===============

Basic cross hair hud. Reacts to state of control object. Also displays health bar for named objects under the cross hair.

Inherit:
	:doc:`GuiBitmapCtrl`

Description
-----------

Basic cross hair hud. Reacts to state of control object. Also displays health bar for named objects under the cross hair.

Uses the base bitmap control to render a bitmap, and decides whether to draw or not depending on the current control object and it's state. If there is ShapeBase object under the cross hair and it's named, then a small health bar is displayed.

Example::

	newGuiCrossHairHud(){
	   damageFillColor = "1.0 0.0 0.0 1.0"; // Fills with a solid red colordamageFrameColor = "1.0 1.0 1.0 1.0"; // Solid white frame colordamageRect = "15 5";
	   damageOffset = "0 -10";
	};


Fields
------


.. cpp:member:: ColorF  GuiCrossHairHud::damageFillColor

	As the health bar depletes, this color will represent the health loss amount.

.. cpp:member:: ColorF  GuiCrossHairHud::damageFrameColor

	Color for the health bar's frame.

.. cpp:member:: Point2I  GuiCrossHairHud::damageOffset

	Offset for drawing the damage portion of the health control.

.. cpp:member:: Point2I  GuiCrossHairHud::damageRect

	Size for the health bar portion of the control.
