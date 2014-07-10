RazerHydraFrame
===============



Inherit:
	:doc:`SimObject`

Description
-----------

UNDOCUMENTED!


Methods
-------


.. cpp:function:: bool RazerHydraFrame::getControllerButton1(int index)

	Get the button 1 state for the requested controller.

	:param index: The controller index to check.

	:return: Button 1 state requested controller as true or false. 

.. cpp:function:: bool RazerHydraFrame::getControllerButton2(int index)

	Get the button 2 state for the requested controller.

	:param index: The controller index to check.

	:return: Button 2 state requested controller as true or false. 

.. cpp:function:: bool RazerHydraFrame::getControllerButton3(int index)

	Get the button 3 state for the requested controller.

	:param index: The controller index to check.

	:return: Button 3 state requested controller as true or false. 

.. cpp:function:: bool RazerHydraFrame::getControllerButton4(int index)

	Get the button 4 state for the requested controller.

	:param index: The controller index to check.

	:return: Button 4 state requested controller as true or false. 

.. cpp:function:: int RazerHydraFrame::getControllerCount()

	Get the number of controllers defined in this frame.

	:return: The number of defined controllers. 

.. cpp:function:: bool RazerHydraFrame::getControllerDocked(int index)

	Get the docked state of the controller.

	:param index: The controller index to check.

	:return: True if the requested controller is docked. 

.. cpp:function:: bool RazerHydraFrame::getControllerEnabled(int index)

	Get the enabled state of the controller.

	:param index: The controller index to check.

	:return: True if the requested controller is enabled. 

.. cpp:function:: Point3I RazerHydraFrame::getControllerPos(int index)

	Get the position of the requested controller. The position is the controller's integer position converted to Torque 3D coordinates (in millimeters).

	:param index: The controller index to check.

	:return: Integer position of the requested controller (in millimeters). 

.. cpp:function:: Point3F RazerHydraFrame::getControllerRawPos(int index)

	Get the raw position of the requested controller. The raw position is the controller's floating point position converted to Torque 3D coordinates (in millimeters).

	:param index: The controller index to check.

	:return: Raw position of the requested controller (in millimeters). 

.. cpp:function:: TransformF RazerHydraFrame::getControllerRawTransform(int index)

	Get the raw transform of the requested controller.

	:param index: The controller index to check.

	:return: The raw position and rotation of the requested controller (in Torque 3D coordinates). 

.. cpp:function:: AngAxisF RazerHydraFrame::getControllerRot(int index)

	Get the rotation of the requested controller. The Razer Hydra controller rotation as converted into the Torque 3Dcoordinate system.

	:param index: The controller index to check.

	:return: Rotation of the requested controller. 

.. cpp:function:: Point2F RazerHydraFrame::getControllerRotAxis(int index)

	Get the axis rotation of the requested controller. This is the axis rotation of the controller as if the controller were a gamepad thumb stick. Imagine a stick coming out the top of the controller and tilting the controller front, back, left and right controls that stick. The values returned along the x and y stick axis are normalized from -1.0 to 1.0 with the maximum controller tilt angle for these values as defined by $RazerHydra::MaximumAxisAngle .

	:param index: The controller index to check.

	:return: Axis rotation of the requested controller.

.. cpp:function:: int RazerHydraFrame::getControllerSequenceNum(int index)

	Get the controller sequence number.

	:param index: The controller index to check.

	:return: The sequence number of the requested controller. 

.. cpp:function:: bool RazerHydraFrame::getControllerShoulderButton(int index)

	Get the shoulder button state for the requested controller.

	:param index: The controller index to check.

	:return: Shoulder button state requested controller as true or false. 

.. cpp:function:: bool RazerHydraFrame::getControllerStartButton(int index)

	Get the start button state for the requested controller.

	:param index: The controller index to check.

	:return: Start button state requested controller as true or false. 

.. cpp:function:: bool RazerHydraFrame::getControllerThumbButton(int index)

	Get the thumb button state for the requested controller.

	:param index: The controller index to check.

	:return: Thumb button state requested controller as true or false. 

.. cpp:function:: Point2F RazerHydraFrame::getControllerThumbStick(int index)

	Get the thumb stick values of the requested controller. The thumb stick values are in the range of -1.0..1.0

	:param index: The controller index to check.

	:return: Thumb stick values of the requested controller. 

.. cpp:function:: TransformF RazerHydraFrame::getControllerTransform(int index)

	Get the transform of the requested controller.

	:param index: The controller index to check.

	:return: The position and rotation of the requested controller (in Torque 3D coordinates). 

.. cpp:function:: float RazerHydraFrame::getControllerTrigger(int index)

	Get the trigger value for the requested controller. The trigger value is in the range of -1.0..1.0

	:param index: The controller index to check.

	:return:  value of the requested controller. 

.. cpp:function:: int RazerHydraFrame::getFrameInternalId()

	Provides the internal ID for this frame.

	:return: Internal ID of this frame. 

.. cpp:function:: int RazerHydraFrame::getFrameRealTime()

	Get the real time that this frame was generated.

	:return: Real time of this frame in milliseconds. 

.. cpp:function:: int RazerHydraFrame::getFrameSimTime()

	Get the sim time that this frame was generated.

	:return: Sim time of this frame in milliseconds. 

.. cpp:function:: bool RazerHydraFrame::isFrameValid()

	Checks if this frame is valid.

	:return: True if the frame is valid. 
