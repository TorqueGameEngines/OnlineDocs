GuiProgressCtrl
===============

GUI Control which displays a horizontal bar which increases as the progress value of 0.0 - 1.0 increases.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

GUI Control which displays a horizontal bar which increases as the progress value of 0.0 - 1.0 increases.

Example::

	newGuiProgressCtrl(JS_statusBar)
	    {
	          //Properties not specific to this control have been omitted from this example.
	     };
	
	// Define the value to set the progress bar%value = "0.5f"// Set the value of the progress bar, from 0.0 - 1.0
	%thisGuiProgressCtrl.setValue(%value);
	// Get the value of the progress bar.
	%progress = %thisGuiProgressCtrl.getValue();

