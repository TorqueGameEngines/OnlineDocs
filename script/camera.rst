Camera
======

This section is dedicated to the various camera objects in Torque 3D. The base Camera object that is typically manipulated by a GameConnection's input. A Path Camera moves along a path.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/Camera
	class/CameraData
	class/PathCamera
	class/PathCameraData

Functions
---------

.. cpp:function:: void setDefaultFov(float defaultFOV)

	Set the default FOV for a camera.

	:param defaultFOV: The default field of view in degrees

.. cpp:function:: void setFov(float FOV)

	Set the FOV of the camera.

	:param FOV: The camera's new FOV in degrees

.. cpp:function:: void setZoomSpeed(int speed)

	Set the zoom speed of the camera. This affects how quickly the camera changes from one field of view to another.

	:param speed: The camera's zoom speed in ms per 90deg FOV change

Enumerations
------------

.. cpp:type:: enum CameraMotionMode
	
	Movement behavior type for Camera.

	:param Stationary: Camera does not rotate or move.
	:param FreeRotate: Camera may rotate but does not move.
	:param Fly: Camera may rotate and move freely.
	:param OrbitObject: Camera orbits about a given object. Damage flash and white out is determined by the object being orbited. See Camera::setOrbitMode() to set the orbit object and other parameters.
	:param OrbitPoint: Camera orbits about a given point. See Camera::setOrbitMode() to set the orbit point and other parameters.
	:param TrackObject: Camera always faces a given object. See Camera::setTrackObject() to set the object to track and a distance to remain from the object.
	:param Overhead: Camera moves in the XY plane.
	:param EditOrbit: Used by the World Editor to orbit about a point. When first activated, the camera is rotated to face the orbit point rather than move to it.

Variables
---------

.. cpp:member:: int Camera::extendedMovePosRotIndex

	The ExtendedMove position/rotation index used for camera movements.

.. cpp:member:: float Camera::movementSpeed

	Global camera movement speed in units/s (typically m/s), with a base value of 40.

	Used in the following camera modes:

	* Edit Orbit Mode
	* Fly Mode
	* Overhead Mode
