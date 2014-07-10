GuiBitmapButtonTextCtrl
=======================

An extension of GuiBitmapButtonCtrl that additionally renders a text label on the bitmapped button.

Inherit:
	:doc:`GuiBitmapButtonCtrl`

Description
-----------

The text for the label is taken from the GuiButtonBaseCtrl::text property.

For rendering, the label is placed, relative to the control's upper left corner, at the text offset specified in the control's profile (GuiControlProfile::textOffset) and justified according to the profile's setting (GuiControlProfile::justify).

