GuiBitmapButtonCtrl
===================

A button that renders its various states (mouse over, pushed, etc.) from separate bitmaps.

Inherit:
	:doc:`GuiButtonCtrl`

Description
-----------

A bitmapped button is a push button that uses one or more texture images for rendering its individual states.

To find the individual textures associated with the button, a naming scheme is used. For each state a suffix is appended to the texture file name given in the GuiBitmapButtonCtrl::bitmap field:

If a bitmap for a particular state cannot be found, the default bitmap will be used. To disable all state-based bitmap functionality, set useStates to false which will make the control solely render from the bitmap specified in the bitmap field.

Per-Modifier Button Actions
---------------------------

If GuiBitmapButtonCtrl::useModifiers is set to true, per-modifier button actions and textures are enabled. This functionality allows to associate different images and different actions with a button depending on which modifiers are pressed on the keyboard by the user.

When enabled, this functionality alters the texture lookup above by prepending the following strings to the suffixes listed above:

When this functionality is enabled, a new set of callbacks is used:

GuiControl::command or GuiControl::onAction() still work as before when per-modifier functionality is enabled.

Note that modifiers cannot be mixed. If two or more modifiers are pressed, a single one will take precedence over the remaining modifiers. The order of precedence corresponds to the order listed above.

Example::

	// Create an OK button that will trigger an onOk() call on its parent when clicked:
	%okButton = newGuiBitmapButtonCtrl()
	{
	   bitmap = "art/gui/okButton";
	   autoFitExtents = true;
	   command = "$ThisControl.getParent().onOk();";
	};


Methods
-------


.. cpp:function:: void GuiBitmapButtonCtrl::onAltClick()

	Called when per-modifier functionality is enabled and the user clicks on the button with the ALT key pressed. Per-Modifier Button Actions

.. cpp:function:: void GuiBitmapButtonCtrl::onCtrlClick()

	Called when per-modifier functionality is enabled and the user clicks on the button with the CTRL key pressed. Per-Modifier Button Actions

.. cpp:function:: void GuiBitmapButtonCtrl::onDefaultClick()

	Called when per-modifier functionality is enabled and the user clicks on the button without any modifier pressed. Per-Modifier Button Actions

.. cpp:function:: void GuiBitmapButtonCtrl::onShiftClick()

	Called when per-modifier functionality is enabled and the user clicks on the button with the SHIFT key pressed. Per-Modifier Button Actions

.. cpp:function:: void GuiBitmapButtonCtrl::setBitmap(string path)

	Set the bitmap to show on the button.

	:param path: Path to the texture file in any of the supported formats.

Fields
------


.. cpp:member:: bool  GuiBitmapButtonCtrl::autoFitExtents

	If true, the control's extents will be set to match the bitmap's extents when setting the bitmap. The bitmap extents will always be taken from the default/normal bitmap (in case the extents of the various bitmaps do not match up.)

.. cpp:member:: filename  GuiBitmapButtonCtrl::bitmap

	Texture file to display on this button. If useStates is false, this will be the file that renders on the control. Otherwise, this will specify the default texture name to which the various state and modifier suffixes are appended to find the per-state and per-modifier (if enabled) textures.

.. cpp:member:: GuiBitmapMode GuiBitmapButtonCtrl::bitmapMode

	Behavior for fitting the bitmap to the control extents. If set to 'Stretched', the bitmap will be stretched both verticall and horizontally to fit inside the control's extents. If set to 'Centered', the bitmap will stay at its original resolution centered in the control's rectangle (getting clipped if the control is smaller than the texture).

.. cpp:member:: bool  GuiBitmapButtonCtrl::useModifiers

	If true, per-modifier button functionality is enabled. Per-Modifier Button Actions

.. cpp:member:: bool  GuiBitmapButtonCtrl::useStates

	If true, per-mouse state button functionality is enabled. Defaults to true. If you do not use per-state images on this button set this to false to speed up the loading process by inhibiting searches for the individual images.
