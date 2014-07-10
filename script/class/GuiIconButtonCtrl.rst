GuiIconButtonCtrl
=================

Draws the bitmap within a special button control. Only a single bitmap is used and the button will be drawn in a highlighted mode when the mouse hovers over it or when it has been clicked.

Inherit:
	:doc:`GuiButtonCtrl`

Description
-----------

Draws the bitmap within a special button control. Only a single bitmap is used and the button will be drawn in a highlighted mode when the mouse hovers over it or when it has been clicked.

Example::

	newGuiIconButtonCtrl(TestIconButton)
	{
	   buttonMargin = "4 4";
	   iconBitmap = "art/gui/lagIcon.png";
	   iconLocation = "Center";
	   sizeIconToButton = "0";
	   makeIconSquare = "1";
	   textLocation = "Bottom";
	   textMargin = "-2";
	   autoSize = "0";
	   text = "Lag Icon";
	   textID = ""STR_LAG"";
	   buttonType = "PushButton";
	   profile = "GuiIconButtonProfile";
	};


Methods
-------


.. cpp:function:: void GuiIconButtonCtrl::setBitmap(string buttonFilename)

	Set the bitmap to use for the button portion of this control.

	:param buttonFilename: Filename for the image

	Example::

		// Define the button filename
		%buttonFilename = "pearlButton";
		
		// Inform the GuiIconButtonCtrl control to update its main button graphic to the defined bitmap
		%thisGuiIconButtonCtrl.setBitmap(%buttonFilename);

Fields
------


.. cpp:member:: bool  GuiIconButtonCtrl::autoSize

	If true, the text and icon will be automatically sized to the size of the control.

.. cpp:member:: Point2I  GuiIconButtonCtrl::buttonMargin

	Margin area around the button.

.. cpp:member:: filename  GuiIconButtonCtrl::iconBitmap

	Bitmap file for the icon to display on the button.

.. cpp:member:: GuiIconButtonIconLocation GuiIconButtonCtrl::iconLocation

	Where to place the icon on the control. Options are 0 (None), 1 (Left), 2 (Right), 3 (Center).

.. cpp:member:: bool  GuiIconButtonCtrl::makeIconSquare

	If true, will make sure the icon is square.

.. cpp:member:: bool  GuiIconButtonCtrl::sizeIconToButton

	If true, the icon will be scaled to be the same size as the button.

.. cpp:member:: GuiIconButtonTextLocation GuiIconButtonCtrl::textLocation

	Where to place the text on the control. Options are 0 (None), 1 (Bottom), 2 (Right), 3 (Top), 4 (Left), 5 (Center).

.. cpp:member:: int  GuiIconButtonCtrl::textMargin

	Margin between the icon and the text.
