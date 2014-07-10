GuiButtonBaseCtrl
=================

The base class for the various button controls.

Inherit:
	:doc:`GuiControl`

Description
-----------

This is the base class for the various types of button controls. If no more specific functionality is required than offered by this class, then it can be instantiated and used directly. Otherwise, its subclasses should be used:

Methods
-------

.. cpp:function:: string GuiButtonBaseCtrl::getText()

	Get the text display on the button's label (if any).

	:return: The button's label. 

.. cpp:function:: void GuiButtonBaseCtrl::onClick()

	Called when the primary action of the button is triggered (e.g. by a left mouse click).

.. cpp:function:: void GuiButtonBaseCtrl::onDoubleClick()

	Called when the left mouse button is double-clicked on the button.

.. cpp:function:: void GuiButtonBaseCtrl::onMouseDown()

	If useMouseEvents is true, this is called when the left mouse button is pressed on an (active) button.

.. cpp:function:: void GuiButtonBaseCtrl::onMouseDragged()

	If useMouseEvents is true, this is called when a left mouse button drag is detected, i.e. when the user pressed the left mouse button on the control and then moves the mouse over a certain distance threshold with the mouse button still pressed.

.. cpp:function:: void GuiButtonBaseCtrl::onMouseEnter()

	If useMouseEvents is true, this is called when the mouse cursor moves over the button (only if the button is the front-most visible control, though).

.. cpp:function:: void GuiButtonBaseCtrl::onMouseLeave()

	If useMouseEvents is true, this is called when the mouse cursor moves off the button (only if the button had previously received an onMouseEvent() event).

.. cpp:function:: void GuiButtonBaseCtrl::onMouseUp()

	If useMouseEvents is true, this is called when the left mouse button is release over an (active) button.

.. cpp:function:: void GuiButtonBaseCtrl::onRightClick()

	Called when the right mouse button is clicked on the button.

.. cpp:function:: void GuiButtonBaseCtrl::performClick()

	Simulate a click on the button. This method will trigger the button's action just as if the button had been pressed by the user.

.. cpp:function:: void GuiButtonBaseCtrl::resetState()

	Reset the mousing state of the button. This method should not generally be called.

.. cpp:function:: void GuiButtonBaseCtrl::setStateOn(bool isOn)

	For toggle or radio buttons, set whether the button is currently activated or not. For radio buttons, toggling a button on will toggle all other radio buttons in its group to off. Reimplemented in GuiCheckBoxCtrl .

	:param isOn: If true, the button will be toggled on (if not already); if false, it will be toggled off.

.. cpp:function:: void GuiButtonBaseCtrl::setText(string text)

	Set the text displayed on the button's label.

	:param text: The text to display as the button's text label.

.. cpp:function:: void GuiButtonBaseCtrl::setTextID(string id)

	Set the text displayed on the button's label using a string from the string table assigned to the control. Internationalization

	:param id: Name of the variable that contains the integer string ID. Used to look up string in table.

Fields
------

.. cpp:member:: GuiButtonType GuiButtonBaseCtrl::buttonType

	Button behavior type.

.. cpp:member:: int  GuiButtonBaseCtrl::groupNum

	Radio button toggle group number. All radio buttons that are assigned the same groupNum and that are parented to the same control will synchronize their toggle state, i.e. if one radio button is toggled on all other radio buttons in its group will be toggled off. The default group is -1.

.. cpp:member:: caseString  GuiButtonBaseCtrl::text

	Text label to display on button (if button class supports text labels).

.. cpp:member:: string  GuiButtonBaseCtrl::textID

	ID of string in string table to use for text label on button.

.. cpp:member:: bool  GuiButtonBaseCtrl::useMouseEvents

	If true, mouse events will be passed on to script. Default is false.
