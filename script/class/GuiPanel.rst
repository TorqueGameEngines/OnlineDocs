GuiPanel
========

The GuiPanel panel is a container that when opaque will draw a left to right gradient using its profile fill and fill highlight colors.

Inherit:
	:doc:`GuiContainer`

Description
-----------

The GuiPanel panel is a container that when opaque will draw a left to right gradient using its profile fill and fill highlight colors.

Example::

	// Mandatory GuiDefaultProfile// Contains the fill color information required by a GuiPanel// Some values left out for sake of this examplenewGuiControlProfile (GuiDefaultProfile)
	{
	   // fill color
	   opaque = false;
	   fillColor = "242 241 240";
	   fillColorHL ="228 228 235";
	   fillColorSEL = "98 100 137";
	   fillColorNA = "255 255 255 ";
	};
	
	newGuiPanel(TestPanel)
	{
	   position = "45 33";
	   extent = "342 379";
	   minExtent = "16 16";
	   horizSizing = "right";
	   vertSizing = "bottom";
	   profile = "GuiDefaultProfile"; // Color fill info is in this profileisContainer = "1";
	};

