GuiSwatchButtonCtrl
===================

A button that is used to represent color; often used in correlation with a color picker.

Inherit:
	:doc:`GuiButtonBaseCtrl`

Description
-----------

A swatch button is a push button that uses its color field to designate the color drawn over an image, on top of a button.

The color itself is a float value stored inside the GuiSwatchButtonCtrl::color field. The texture path that represents the image underlying the color is stored inside the GuiSwatchButtonCtrl::gridBitmap field. The default value assigned toGuiSwatchButtonCtrl::color is "1 1 1 1"( White ). The default/fallback image assigned to GuiSwatchButtonCtrl::gridBitmap is "tools/gui/images/transp_grid".

Example::

	// Create a GuiSwatchButtonCtrl that calls randomFunction with its current color when clicked
	%swatchButton = newGuiSwatchButtonCtrl()
	{
	   profile = "GuiInspectorSwatchButtonProfile";
	   command = "randomFunction( $ThisControl.color );";
	};

Methods
-------

.. cpp:function:: void GuiSwatchButtonCtrl::setColor(string newColor)

	Set the color of the swatch control.

	:param newColor: The new color string given to the swatch control in float format "r g b a".

Fields
------

.. cpp:member:: ColorF  GuiSwatchButtonCtrl::color

	The foreground color of GuiSwatchButtonCtrl .

.. cpp:member:: string  GuiSwatchButtonCtrl::gridBitmap

	The bitmap used for the transparent grid.
