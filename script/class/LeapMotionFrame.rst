LeapMotionFrame
===============



Inherit:
	:doc:`SimObject`

Description
-----------

UNDOCUMENTED!


Methods
-------


.. cpp:function:: int LeapMotionFrame::getFrameInternalId()

	Provides the internal ID for this frame.

	:return: Internal ID of this frame. 

.. cpp:function:: int LeapMotionFrame::getFrameRealTime()

	Get the real time that this frame was generated.

	:return: Real time of this frame in milliseconds. 

.. cpp:function:: int LeapMotionFrame::getFrameSimTime()

	Get the sim time that this frame was generated.

	:return: Sim time of this frame in milliseconds. 

.. cpp:function:: int LeapMotionFrame::getHandCount()

	Get the number of hands defined in this frame.

	:return: The number of defined hands. 

.. cpp:function:: int LeapMotionFrame::getHandId(int index)

	Get the ID of the requested hand.

	:param index: The hand index to check.

	:return: ID of the requested hand. 

.. cpp:function:: int LeapMotionFrame::getHandPointablesCount(int index)

	Get the number of pointables associated with this hand.

	:param index: The hand index to check.

	:return: Number of pointables that belong with this hand. 

.. cpp:function:: Point3I LeapMotionFrame::getHandPos(int index)

	Get the position of the requested hand. The position is the hand's integer position converted to Torque 3D coordinates (in millimeters).

	:param index: The hand index to check.

	:return: Integer position of the requested hand (in millimeters). 

.. cpp:function:: Point3F LeapMotionFrame::getHandRawPos(int index)

	Get the raw position of the requested hand. The raw position is the hand's floating point position converted to Torque 3D coordinates (in millimeters).

	:param index: The hand index to check.

	:return: Raw position of the requested hand. 

.. cpp:function:: TransformF LeapMotionFrame::getHandRawTransform(int index)

	Get the raw transform of the requested hand.

	:param index: The hand index to check.

	:return: The raw position and rotation of the requested hand (in Torque 3D coordinates). 

.. cpp:function:: AngAxisF LeapMotionFrame::getHandRot(int index)

	Get the rotation of the requested hand. The Leap Motion hand rotation as converted into the Torque 3Dcoordinate system.

	:param index: The hand index to check.

	:return: Rotation of the requested hand. 

.. cpp:function:: Point2F LeapMotionFrame::getHandRotAxis(int index)

	Get the axis rotation of the requested hand. This is the axis rotation of the hand as if the hand were a gamepad thumb stick. Imagine a stick coming out the top of the hand and tilting the hand front, back, left and right controls that stick. The values returned along the x and y stick axis are normalized from -1.0 to 1.0 with the maximum hand tilt angle for these values as defined by $LeapMotion::MaximumHandAxisAngle .

	:param index: The hand index to check.

	:return: Axis rotation of the requested hand.

.. cpp:function:: TransformF LeapMotionFrame::getHandTransform(int index)

	Get the transform of the requested hand.

	:param index: The hand index to check.

	:return: The position and rotation of the requested hand (in Torque 3D coordinates). 

.. cpp:function:: bool LeapMotionFrame::getHandValid(int index)

	Check if the requested hand is valid.

	:param index: The hand index to check.

	:return: True if the hand is valid. 

.. cpp:function:: int LeapMotionFrame::getPointableHandIndex(int index)

	Get the index of the hand that this pointable belongs to, if any.

	:param index: The pointable index to check.

	:return: Index of the hand this pointable belongs to, or -1 if there is no associated hand. 

.. cpp:function:: int LeapMotionFrame::getPointableId(int index)

	Get the ID of the requested pointable.

	:param index: The pointable index to check.

	:return: ID of the requested pointable. 

.. cpp:function:: float LeapMotionFrame::getPointableLength(int index)

	Get the length of the requested pointable.

	:param index: The pointable index to check.

	:return: Length of the requested pointable (in millimeters). 

.. cpp:function:: Point3I LeapMotionFrame::getPointablePos(int index)

	Get the position of the requested pointable. The position is the pointable's integer position converted to Torque 3D coordinates (in millimeters).

	:param index: The pointable index to check.

	:return: Integer position of the requested pointable (in millimeters). 

.. cpp:function:: Point3F LeapMotionFrame::getPointableRawPos(int index)

	Get the raw position of the requested pointable. The raw position is the pointable's floating point position converted to Torque 3D coordinates (in millimeters).

	:param index: The pointable index to check.

	:return: Raw position of the requested pointable. 

.. cpp:function:: TransformF LeapMotionFrame::getPointableRawTransform(int index)

	Get the raw transform of the requested pointable.

	:param index: The pointable index to check.

	:return: The raw position and rotation of the requested pointable (in Torque 3D coordinates). 

.. cpp:function:: AngAxisF LeapMotionFrame::getPointableRot(int index)

	Get the rotation of the requested pointable. The Leap Motion pointable rotation as converted into the Torque 3Dcoordinate system.

	:param index: The pointable index to check.

	:return: Rotation of the requested pointable. 

.. cpp:function:: int LeapMotionFrame::getPointablesCount()

	Get the number of pointables defined in this frame.

	:return: The number of defined pointables. 

.. cpp:function:: TransformF LeapMotionFrame::getPointableTransform(int index)

	Get the transform of the requested pointable.

	:param index: The pointable index to check.

	:return: The position and rotation of the requested pointable (in Torque 3D coordinates). 

.. cpp:function:: LeapMotionFramePointableType  LeapMotionFrame::getPointableType(int index)

	Get the type of the requested pointable.

	:param index: The pointable index to check.

	:return: Type of the requested pointable. 

.. cpp:function:: bool LeapMotionFrame::getPointableValid(int index)

	Check if the requested pointable is valid.

	:param index: The pointable index to check.

	:return: True if the pointable is valid. 

.. cpp:function:: float LeapMotionFrame::getPointableWidth(int index)

	Get the width of the requested pointable.

	:param index: The pointable index to check.

	:return: Width of the requested pointable (in millimeters). 

.. cpp:function:: bool LeapMotionFrame::isFrameValid()

	Checks if this frame is valid.

	:return: True if the frame is valid. 
