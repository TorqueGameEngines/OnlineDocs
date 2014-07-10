GuiControl
==========

Base class for all Gui control objects.

Inherit:
	:doc:`SimGroup`

Description
-----------

GuiControl is the basis for the Gui system. It represents an individual control that can be placed on the canvas and with which the mouse and keyboard can potentially interact with.

Control Hierarchies
~~~~~~~~~~~~~~~~~~~

GuiControls are arranged in a hierarchy. All children of a control are placed in their parent's coordinate space, i.e. their coordinates are relative to the upper left corner of their immediate parent. When a control is moved, all its child controls are moved along with it.

Since GuiControl's are SimGroups, hierarchy also implies ownership. This means that if a control is destroyed, all its children are destroyed along with it. It also means that a given control can only be part of a single GuiControl hierarchy. When adding a control to another control, it will automatically be reparented from another control it may have previously been parented to.

Layout System
~~~~~~~~~~~~~

GuiControls have a two-dimensional position and are rectangular in shape.

Event System
~~~~~~~~~~~~

Control Profiles
~~~~~~~~~~~~~~~~

Common data accessed by GuiControls is stored in so-called "Control Profiles." This includes font, color, and texture information. By pooling this data in shared objects, the appearance of any number of controls can be changed quickly and easily by modifying only the shared profile object.

If not explicitly assigned a profile, a control will by default look for a profile object that matches its class name. This means that the class GuiMyCtrl, for example, will look for a profile called 'GuiMyProfile'. If this profile cannot be found, the control will fall back to GuiDefaultProfile which must be defined in any case for the Gui system to work.

In addition to its primary profile, a control may be assigned a second profile called 'tooltipProfile' that will be used to render tooltip popups for the control.

Triggered Actions
~~~~~~~~~~~~~~~~~

First Responders
~~~~~~~~~~~~~~~~

At any time, a single control can be what is called the "first responder" on the GuiCanvas is placed on. This control will be the first control to receive keyboard events not bound in the global ActionMap. If the first responder choses to handle a particular keyboard event,

Waking and Sleeping
~~~~~~~~~~~~~~~~~~~

Visibility and Activeness
~~~~~~~~~~~~~~~~~~~~~~~~~

By default, a GuiControl is active which means that it

Methods
-------

.. cpp:function:: void GuiControl::addGuiControl(GuiControl control)

	Add the given control as a child to this control. This is synonymous to calling SimGroup::addObject.

	:param control: The control to add as a child.

.. cpp:function:: void GuiControl::clearFirstResponder(bool ignored)

	Clear this control from being the first responder in its hierarchy chain.

	:param ignored: Ignored. Supported for backwards-compatibility.

.. cpp:function:: bool GuiControl::controlIsChild(GuiControl control)

	Test whether the given control is a direct or indirect child to this control.

	:param control: The potential child control.

	:return: True if the given control is a direct or indirect child to this control. 

.. cpp:function:: GuiControl  GuiControl::findHitControl(int x, int y)

	Find the topmost child control located at the given coordinates.

	:param x: The X coordinate in the control's own coordinate space.
	:param y: The Y coordinate in the control's own coordinate space.

	:return: The topmost child control at the given coordintes or the control on which the method was called if no matching child could be found. 

.. cpp:function:: string GuiControl::findHitControls(int x, int y, int width, int height)

	Find all visible child controls that intersect with the given rectangle.

	:param x: The X coordinate of the rectangle's upper left corner in the control's own coordinate space.
	:param y: The Y coordinate of the rectangle's upper left corner in the control's own coordinate space.
	:param width: The width of the search rectangle in pixels.
	:param height: The height of the search rectangle in pixels.

	:return: A space-separated list of the IDs of all visible control objects intersecting the given rectangle.

	Example::

		// Lock all controls in the rectangle at x=10 and y=10 and the extent width=100 and height=100.foreach$( %ctrl in %this.findHitControls( 10, 10, 100, 100 ) )
		   %ctrl.setLocked( true );

.. cpp:function:: float GuiControl::getAspect()

	Get the aspect ratio of the control's extents.

	:return: The width of the control divided by its height. 

.. cpp:function:: Point2I GuiControl::getCenter()

	Get the coordinate of the control's center point relative to its parent.

	:return: The coordinate of the control's center point in parent-relative coordinates. 

.. cpp:function:: Point2I GuiControl::getExtent()

	Get the width and height of the control. Reimplemented in GuiCanvas .

	:return: A point structure containing the width of the control in x and the height in y. 

.. cpp:function:: GuiControl  GuiControl::getFirstResponder()

	Get the first responder set on this GuiControl tree.

	:return: The first responder set on the control's subtree. 

.. cpp:function:: Point2I GuiControl::getGlobalCenter()

	Get the coordinate of the control's center point in coordinates relative to the root control in its control hierarchy. the center coordinate of the control in root-relative coordinates.

.. cpp:function:: Point2I GuiControl::getGlobalPosition()

	Get the position of the control relative to the root of the GuiControl hierarchy it is contained in.

	:return: The control's current position in root-relative coordinates. 

.. cpp:function:: Point2I GuiControl::getMinExtent()

	Get the minimum allowed size of the control.

	:return: The minimum size to which the control can be shrunk. 

.. cpp:function:: GuiControl  GuiControl::getParent()

	Get the immediate parent control of the control.

	:return: . 

.. cpp:function:: Point2I GuiControl::getPosition()

	Get the control's current position relative to its parent.

	:return: The coordinate of the control in its parent's coordinate space. 

.. cpp:function:: GuiCanvas  GuiControl::getRoot()

	Get the canvas on which the control is placed.

	:return: . 

.. cpp:function:: bool GuiControl::isAwake()

	Test whether the control is currently awake. If a control is awake it means that it is part of the GuiControl hierarchy of a GuiCanvas .

	:return: Waking and Sleeping

.. cpp:function:: bool GuiControl::isFirstResponder()

	Test whether the control is the current first responder.

	:return: True if the control is the current first responder. 

.. cpp:function:: bool GuiControl::isMouseLocked()

	Indicates if the mouse is locked in this control.

	:return: True if the mouse is currently locked. 

.. cpp:function:: bool GuiControl::isVisible()

	Test whether the control is currently set to be visible. Visibility and Activeness

	:return: True if the control is currently set to be visible.

.. cpp:function:: void GuiControl::makeFirstResponder(bool isFirst)


.. cpp:function:: void GuiControl::onAction()

	Called when the control's associated action is triggered and no 'command' is defined for the control. Triggered Actions

.. cpp:function:: void GuiControl::onActive(bool state)

	Called when the control changes its activeness state, i.e. when going from active to inactive or vice versa.

	:param stat: The new activeness state.

.. cpp:function:: void GuiControl::onAdd()

	Called when the control object is registered with the system after the control has been created.

.. cpp:function:: void GuiControl::onControlDragEnter(GuiControl control, Point2I dropPoint)

	Called when a drag amp drop operation through GuiDragAndDropControl has entered the control. This is only called for topmost visible controls as the GuiDragAndDropControl moves over them.

	:param control: The payload of the drag operation.
	:param dropPoint: The point at which the payload would be dropped if it were released now. Relative to the canvas.

.. cpp:function:: void GuiControl::onControlDragExit(GuiControl control, Point2I dropPoint)

	Called when a drag amp drop operation through GuiDragAndDropControl has exited the control and moved over a different control. This is only called for topmost visible controls as the GuiDragAndDropControl moves off of them.

	:param control: The payload of the drag operation.
	:param dropPoint: The point at which the payload would be dropped if it were released now. Relative to the canvas.

.. cpp:function:: void GuiControl::onControlDragged(GuiControl control, Point2I dropPoint)

	Called when a drag amp drop operation through GuiDragAndDropControl is moving across the control after it has entered it. This is only called for topmost visible controls as the GuiDragAndDropControl moves across them.

	:param control: The payload of the drag operation.
	:param dropPoint: The point at which the payload would be dropped if it were released now. Relative to the canvas.

.. cpp:function:: void GuiControl::onControlDropped(GuiControl control, Point2I dropPoint)

	Called when a drag amp drop operation through GuiDragAndDropControl has completed and is dropping its payload onto the control. This is only called for topmost visible controls as the GuiDragAndDropControl drops its payload on them.

	:param control: The control that is being dropped onto this control.
	:param dropPoint: The point at which the control is being dropped. Relative to the canvas.

.. cpp:function:: void GuiControl::onDialogPop()

	Called when the control is removed as a dialog from the canvas.

.. cpp:function:: void GuiControl::onDialogPush()

	Called when the control is pushed as a dialog onto the canvas.

.. cpp:function:: void GuiControl::onGainFirstResponder()

	Called when the control gains first responder status on the GuiCanvas .

.. cpp:function:: void GuiControl::onLoseFirstResponder()

	Called when the control loses first responder status on the GuiCanvas .

.. cpp:function:: void GuiControl::onRemove()

	Called when the control object is removed from the system before it is deleted.

.. cpp:function:: void GuiControl::onSleep()

	Called when the control is put to sleep. Waking and Sleeping

.. cpp:function:: void GuiControl::onVisible(bool state)

	Called when the control changes its visibility state, i.e. when going from visible to invisible or vice versa.

	:param state: The new visibility state.

.. cpp:function:: void GuiControl::onWake()

	Called when the control is woken up. Waking and Sleeping

.. cpp:function:: bool GuiControl::pointInControl(int x, int y)

	Test whether the given point lies within the rectangle of the control.

	:param x: X coordinate of the point in parent-relative coordinates.
	:param y: Y coordinate of the point in parent-relative coordinates.

	:return: True if the point is within the control, false if not. 

.. cpp:function:: void GuiControl::resize(int x, int y, int width, int height)

	Resize and reposition the control using the give coordinates and dimensions. Child controls will resize according to their layout behaviors.

	:param x: The new X coordinate of the control in its parent's coordinate space.
	:param y: The new Y coordinate of the control in its parent's coordinate space.
	:param width: The new width to which the control should be resized.
	:param height: The new height to which the control should be resized.

.. cpp:function:: void GuiControl::setActive(bool state)


.. cpp:function:: void GuiControl::setCenter(int x, int y)

	Set the control's position by its center point.

	:param x: The X coordinate of the new center point of the control relative to the control's parent.
	:param y: The Y coordinate of the new center point of the control relative to the control's parent.

.. cpp:function:: void GuiControl::setExtent(S32 width, S32 height)

	Resize the control to the given dimensions. Child controls will resize according to their layout settings.

	:param width: The new width of the control in pixels.
	:param height: The new height of the control in pixels.

.. cpp:function:: void GuiControl::setExtent(Point2I p)

	Resize the control to the given dimensions. Child controls with resize according to their layout settings.

	:param p: The new ( width, height ) extents of the control.

.. cpp:function:: void  GuiControl::setFirstResponder()

	Make this control the current first responder.

.. cpp:function:: void GuiControl::setPosition(int x, int y)

	Position the control in the local space of the parent control.

	:param x: The new X coordinate of the control relative to its parent's upper left corner.
	:param y: The new Y coordinate of the control relative to its parent's upper left corner.

.. cpp:function:: void GuiControl::setPositionGlobal(int x, int y)

	Set position of the control relative to the root of the GuiControl hierarchy it is contained in.

	:param x: The new X coordinate of the control relative to the root's upper left corner.
	:param y: The new Y coordinate of the control relative to the root's upper left corner.

.. cpp:function:: void GuiControl::setProfile(GuiControlProfile profile)

	Set the control profile for the control to use. The profile used by a control determines a great part of its behavior and appearance.

	:param profile: The new profile the control should use. Control Profiles

.. cpp:function:: void GuiControl::setValue(string value)

	Set the value associated with the control.

	:param value: The new value for the control.

.. cpp:function:: void GuiControl::setVisible(bool state)

	Set whether the control is visible or not.

	:param state: The new visiblity flag state for the control. Visibility and Activeness

Fields
------


.. cpp:member:: string  GuiControl::accelerator

	Key combination that triggers the control's primary action when the control is on the canvas.

.. cpp:member:: bool  GuiControl::active

	Whether the control is enabled for user interaction.

.. cpp:member:: string  GuiControl::altCommand

	Command to execute on the secondary action of the control.

.. cpp:member:: string  GuiControl::command

	Command to execute on the primary action of the control.

.. cpp:member:: Point2I  GuiControl::extent

	The width and height of the control.

.. cpp:member:: string  GuiControl::getValue


.. cpp:member:: GuiHorizontalSizing GuiControl::horizSizing

	The horizontal resizing behavior.

.. cpp:member:: int  GuiControl::hovertime

	Time for mouse to hover over control until tooltip is shown (in milliseconds).

.. cpp:member:: bool  GuiControl::isActive


.. cpp:member:: bool  GuiControl::isContainer

	If true, the control may contain child controls.

.. cpp:member:: string  GuiControl::langTableMod

	Name of string table to use for lookup of internationalized text.

.. cpp:member:: Point2I  GuiControl::minExtent

	The minimum width and height of the control. The control will not be resized smaller than this.

.. cpp:member:: deprecated  GuiControl::modal


.. cpp:member:: Point2I  GuiControl::position

	The position relative to the parent control.

.. cpp:member:: GuiControlProfile GuiControl::profile

	The control profile that determines fill styles, font settings, etc.

.. cpp:member:: deprecated  GuiControl::setFirstResponder


.. cpp:member:: string  GuiControl::tooltip

	String to show in tooltip for this control.

.. cpp:member:: GuiControlProfile GuiControl::tooltipProfile

	Control profile to use when rendering tooltips for this control.

.. cpp:member:: string  GuiControl::variable

	Name of the variable to which the value of this control will be synchronized.

.. cpp:member:: GuiVerticalSizing GuiControl::vertSizing

	The vertical resizing behavior.

.. cpp:member:: bool  GuiControl::visible

	Whether the control is visible or hidden.
