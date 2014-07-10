GuiBitmapCtrl
=============

A gui control that is used to display an image.

Inherit:
	:doc:`GuiControl`

Description
-----------

The image is stretched to the constraints of the control by default. However, the control can also tile the image as well.

The image itself is stored inside the GuiBitmapCtrl::bitmap field. The boolean value that decides whether the image is stretched or tiled is stored inside the GuiBitmapCtrl::wrap field.

Example::

	// Create a tiling GuiBitmapCtrl that displays "myImage.png"
	%bitmapCtrl = newGuiBitmapCtrl()
	{
	   bitmap = "myImage.png";
	   wrap = "true";
	};


Methods
-------


.. cpp:function:: void GuiBitmapCtrl::setBitmap(String filename, bool resize)

	Assign an image to the control. Child controls with resize according to their layout settings.

	:param filename: The filename of the image.
	:param resize: Optional parameter. If true, the GUI will resize to fit the image.

.. cpp:function:: void GuiBitmapCtrl::setBitmap(String filename)

	Assign an image to the control. Child controls will resize according to their layout settings.

	:param filename: The filename of the image.
	:param resize: A boolean value that decides whether the ctrl refreshes or not.

.. cpp:function:: void GuiBitmapCtrl::setValue(int x, int y)

	Set the offset of the bitmap within the control.

	:param x: The x-axis offset of the image.
	:param y: The y-axis offset of the image.

Fields
------


.. cpp:member:: filename  GuiBitmapCtrl::bitmap

	The bitmap file to display in the control.

.. cpp:member:: bool  GuiBitmapCtrl::wrap

	If true, the bitmap is tiled inside the control rather than stretched to fit.
