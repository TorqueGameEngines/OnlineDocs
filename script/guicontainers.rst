Container Controls
==================

A collection of various containers (container, window, scroll, etc). 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/GuiAutoScrollCtrl
	class/GuiContainer
	class/GuiControlArrayControl
	class/GuiDynamicCtrlArrayControl
	class/GuiFrameSetCtrl
	class/GuiPaneControl
	class/GuiPanel
	class/GuiRolloutCtrl
	class/GuiScrollCtrl
	class/GuiSpeedometerHud
	class/GuiSplitContainer
	class/GuiStackControl
	class/GuiTabBookCtrl
	class/GuiTabPageCtrl
	class/GuiTreeViewCtrl
	class/GuiWindowCtrl

Enumeration
-----------

.. cpp:member:: enum  GuiAutoScrollDirection

	Direction in which to scroll the child control.

	:param Up: Scroll from bottom towards top.
	:param Down: Scroll from top towards bottom.
	:param Left: Scroll from right towards left.
	:param Right: Scroll from left towards right.

.. cpp:member:: enum  GuiDockingType


	:param None: 
	:param Client: 
	:param Top: 
	:param Bottom: 
	:param Left: 
	:param Right: 

.. cpp:member:: enum  GuiFrameState


	:param alwaysOn: 
	:param alwaysOff: 
	:param dynamic: 

.. cpp:member:: enum  GuiHorizontalStackingType

	Determines how child controls are stacked horizontally.

	:param Right: Child controls are positioned in order from left to right (left-most control is first).
	:param Left: Child controls are positioned in order from right to left (right-most control is first).

.. cpp:member:: enum  GuiScrollBarBehavior

	Display behavior of a scroll bar. Determines when a scrollbar will be visible.

	:param alwaysOn: Always visible.
	:param alwaysOff: Never visible.
	:param dynamic: Only visible when actually needed, i.e. when the child control(s) exceed the visible space on the given axis.

.. cpp:member:: enum  GuiSplitFixedPanel

	Which side of the splitter to keep at a fixed size (if any).

	:param None: Allow both childs to resize (default).
	:param FirstPanel: Keep.
	:param SecondPanel: 

.. cpp:member:: enum  GuiSplitOrientation

	Axis along which to divide the container's space.

	:param Vertical: Divide vertically placing one child left and one child right.
	:param Horizontal: Divide horizontally placing one child on top and one child below.

.. cpp:member:: enum  GuiStackingType

	Stacking method used to position child controls.

	:param Vertical: Stack children vertically by setting their Y position.
	:param Horizontal: Stack children horizontall by setting their X position.
	:param Dynamic: Automatically switch between Vertical and Horizontal stacking. Vertical stacking is chosen when the stack control is taller than it is wide, horizontal stacking is chosen when the stack control is wider than it is tall.

.. cpp:member:: enum  GuiTabPosition

	Where the control should put the tab headers for selecting individual pages.

	:param Top: Tab headers on top edge.
	:param Bottom: Tab headers on bottom edge.

.. cpp:member:: enum  GuiVerticalStackingType

	Determines how child controls are stacked vertically.

	:param Bottom: Child controls are positioned in order from top to bottom (top-most control is first).
	:param Top: Child controls are positioned in order from bottom to top (bottom-most control is first).
