GuiChunkedBitmapCtrl
====================

This is a control that will render a specified bitmap or a bitmap specified in a referenced variable.

Inherit:
	:doc:`GuiControl`

Description
-----------

This control allows you to either set a bitmap with the "bitmap" field or with the setBitmap method. You can also choose to reference a variable in the "variable" field such as "$image" and then set "useVariable" to true. This will cause it to synchronize the variable with the bitmap displayed (if the variable holds a valid image). You can then change the variable and effectively changed the displayed image.

Example::

	$image = "anotherbackground.png";
	newGuiChunkedBitmapCtrl(ChunkedBitmap)
	{
	   bitmap = "background.png";
	   variable = "$image";
	   useVariable = false;
	}
	
	// This will result in the control rendering "background.png"// If we now set the useVariable to true it will now render "anotherbackground.png"
	ChunkedBitmap.useVariable = true;

Methods
-------

.. cpp:function:: void GuiChunkedBitmapCtrl::setBitmap(string filename)

	Set the image rendered in this control.

	:param filename: The image name you want to set

	Example::

		ChunkedBitmap.setBitmap("images/background.png");

Fields
------

.. cpp:member:: filename  GuiChunkedBitmapCtrl::bitmap

	This is the bitmap to render to the control.

.. cpp:member:: bool  GuiChunkedBitmapCtrl::tile

	This is no longer in use.

.. cpp:member:: bool  GuiChunkedBitmapCtrl::useVariable

	This decides whether to use the "bitmap" file or a bitmap stored in "variable".
