GuiBitmapBorderCtrl
===================

A control that renders a skinned border specified in its profile.

Inherit:
	:doc:`GuiControl`

Description
-----------

This control uses the bitmap specified in it's profile (GuiControlProfile::bitmapName). It takes this image and breaks up aspects of it to skin the border of this control with. It is also important to set GuiControlProfile::hasBitmapArray to true on the profile as well.

The bitmap referenced should be broken up into a 3 x 3 grid (using the top left color pixel as a border color between each of the images) in which it will map to the following places: 1 = Top Left Corner 2 = Top Right Corner 3 = Top Center 4 = Left Center 5 = Right Center 6 = Bottom Left Corner 7 = Bottom Center 8 = Bottom Right Corner 0 = Nothing

1 2 3 4 5 0 6 7 8

Example::

	singleton GuiControlProfile (BorderGUIProfile)
	{
	   bitmap = "core/art/gui/images/borderArray";
	   hasBitmapArray = true;
	   opaque = false;
	};
	
	newGuiBitmapBorderCtrl(BitmapBorderGUI)
	{
	   profile = "BorderGUIProfile";
	   position = "0 0";
	   extent = "400 40";
	   visible = "1";
	};

