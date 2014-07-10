GuiSplitContainer
=================

A container that splits its area between two child controls.

Inherit:
	:doc:`GuiContainer`

Description
-----------

A GuiSplitContainer can be used to dynamically subdivide an area between two child controls. A splitter bar is placed between the two controls and allows to dynamically adjust the sizing ratio between the two sides. Splitting can be either horizontal (subdividing top and bottom) or vertical (subdividing left and right) depending on orientation.

By using fixedPanel, one of the panels can be chosen to remain at a fixed size (fixedSize).

Example::

	// Create a vertical splitter with a fixed-size left panel.
	%splitter = newGuiSplitContainer()
	{
	   orientation = "Vertical";
	   fixedPanel = "FirstPanel";
	   fixedSize = 100;
	
	   newGuiScrollCtrl()
	   {
	      newGuiMLTextCtrl()
	      {
	         text = %longText;
	      };
	   };
	
	   newGuiScrollCtrl()
	   {
	      newGuiMLTextCtrl()
	      {
	         text = %moreLongText;
	      };
	   };
	};


Fields
------

.. cpp:member:: GuiSplitFixedPanel GuiSplitContainer::fixedPanel

	Which (if any) side of the splitter to keep at a fixed size.

.. cpp:member:: int  GuiSplitContainer::fixedSize

	Width of the fixed panel specified by fixedPanel (if any).

.. cpp:member:: GuiSplitOrientation GuiSplitContainer::orientation

	Whether to split between top and bottom (horizontal) or between left and right (vertical).

.. cpp:member:: Point2I  GuiSplitContainer::splitPoint

	Point on control through which the splitter goes. Changed relatively if size of control changes.

.. cpp:member:: int  GuiSplitContainer::splitterSize

	Width of the splitter bar between the two sides. Default is 2.
