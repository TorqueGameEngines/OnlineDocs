GuiProgressBitmapCtrl
=====================

A horizontal progress bar rendered from a repeating image.

Inherit:
	:doc:`GuiTextCtrl`

Description
-----------

This class is used give progress feedback to the user. Unlike GuiProgressCtrl which simply renders a filled rectangle, GuiProgressBitmapCtrl renders the bar using a bitmap.

This bitmap can either be simple, plain image which is then stretched into the current extents of the bar as it fills up or it can be a bitmap array with three entries. In the case of a bitmap array, the first entry in the array is used to render the left cap of the bar and the third entry in the array is used to render the right cap of the bar. The second entry is streched in-between the two caps.

Example::

	// This example shows one way to break down a long-running computation into phases// and incrementally update a progress bar between the phases.newGuiProgressBitmapCtrl( Progress )
	{
	   bitmap = "core/art/gui/images/loading";
	   extent = "300 50";
	   position = "100 100";
	};
	
	// Put the control on the canvas.
	%wrapper = newGuiControl();
	%wrapper.addObject( Progress );
	Canvas.pushDialog( %wrapper );
	
	// Start the computation.schedule( 1, 0, "phase1" );
	
	function phase1()
	{
	   Progress.setValue( 0 );
	
	   // Perform some computation.//...// Update progress.
	   Progress.setValue( 0.25 );
	
	   // Schedule next phase.  Dont call directly so engine gets a change to run refresh.schedule( 1, 0, "phase2" );
	}
	
	function phase2()
	{
	   // Perform some computation.//...// Update progress.
	   Progress.setValue( 0.7 );
	
	   // Schedule next phase.  Dont call directly so engine gets a change to run refresh.schedule( 1, 0, "phase3" );
	}
	
	function phase3()
	{
	   // Perform some computation.//...// Update progress.
	   Progress.setValue( 0.9 );
	
	   // Schedule next phase.  Dont call directly so engine gets a change to run refresh.schedule( 1, 0, "phase4" );
	}
	
	function phase4()
	{
	   // Perform some computation.//...// Final update of progress.
	   Progress.setValue( 1.0 );
	}


Methods
-------


.. cpp:function:: void GuiProgressBitmapCtrl::setBitmap(string filename)

	Set the bitmap to use for rendering the progress bar.

	:param filename: ~Path to the bitmap file.

Fields
------


.. cpp:member:: filename  GuiProgressBitmapCtrl::bitmap

	~Path to the bitmap file to use for rendering the progress bar. If the profile assigned to the control already has a bitmap assigned, this property need not be set in which case the bitmap from the profile is used.
