PathCamera
==========

A camera that moves along a path. The camera can then be made to travel along this path forwards or backwards.

Inherit:
	:doc:`ShapeBase`

Description
-----------

A camera's path is made up of knots, which define a position, rotation and speed for the camera. Traversal from one knot to another may be either linear or using a Catmull-Rom spline. If the knot is part of a spline, then it may be a normal knot or defined as a kink. Kinked knots are a hard transition on the spline rather than a smooth one. A knot may also be defined as a position only. In this case the knot is treated as a normal knot but is ignored when determining how to smoothly rotate the camera while it is travelling along the path (the algorithm moves on to the next knot in the path for determining rotation).

The datablock field for a PathCamera is a previously created PathCameraData, which acts as the interface between the script and the engine for this PathCamera object.

Example::

	%newPathCamera = newPathCamera()
	{
	  dataBlock = LoopingCam;
	  position = "0 0 300 1 0 0 0";
	};

Methods
-------

.. cpp:function:: void PathCamera::onNode(string node)

	A script callback that indicates the path camera has arrived at a specific node in its path. Server side only.

	:param Node: Unique ID assigned to this node.

.. cpp:function:: void PathCamera::popFront()

	Removes the knot at the front of the camera's path.

	Example::

		// Remove the first knot in the cameras path.
		%pathCamera.popFront();

.. cpp:function:: void PathCamera::pushBack(TransformF transform, float speed, string type, string path)

	Adds a new knot to the back of a path camera's path.

	:param transform: Transform for the new knot. In the form of "x y z ax ay az aa" such as returned by SceneObject::getTransform()
	:param speed: Speed setting for this knot.
	:param type: Knot type (Normal, Position Only, Kink).
	:param path: Path type (Linear, Spline).

	Example::

		// Transform vector for new knot.
		//  (Pos_X Pos_Y Pos_Z Rot_X Rot_Y Rot_Z Angle)
		%transform = "15.0 5.0 5.0 1.4 1.0 0.2 1.0"
		// Speed setting for knot.
		%speed = "1.0"
		// Knot type.
		//  (Normal, Position Only, Kink)
		%type = "Normal";
		
		// Path Type. (Linear, Spline)
		%path = "Linear";
		
		// Inform the path camera to add a new knot to the back of its path
		%pathCamera.pushBack(%transform,%speed,%type,%path);

.. cpp:function:: void PathCamera::pushFront(TransformF transform, float speed, string type, string path)

	Adds a new knot to the front of a path camera's path.

	:param transform: Transform for the new knot. In the form of "x y z ax ay az aa" such as returned by SceneObject::getTransform()
	:param speed: Speed setting for this knot.
	:param type: Knot type (Normal, Position Only, Kink).
	:param path: Path type (Linear, Spline).

	Example::

		// Transform vector for new knot.
		//  (Pos_X,Pos_Y,Pos_Z,Rot_X,Rot_Y,Rot_Z,Angle)
		%transform = "15.0 5.0 5.0 1.4 1.0 0.2 1.0"
		// Speed setting for knot.
		%speed = "1.0";
		
		// Knot type.
		//  (Normal, Position Only, Kink)
		%type = "Normal";
		
		// Path Type. (Linear, Spline)
		%path = "Linear";
		
		// Inform the path camera to add a new knot to the front of its path
		%pathCamera.pushFront(%transform, %speed, %type, %path);

.. cpp:function:: void PathCamera::reset(float speed)

	Clear the camera's path and set the camera's current transform as the start of the new path. What specifically occurs is a new knot is created from the camera's current transform. Then the current path is cleared and the new knot is pushed onto the path. Any previous target is cleared and the camera's movement state is set to Forward. The camera is now ready for a new path to be defined.

	:param speed: Speed for the camera to move along its path after being reset.

	Example::

		//Determine the new movement speed of this camera. If not set, the speed will default to 1.0.
		%speed = "0.50";
		
		// Inform the path camera to start a new path at
		// the cameras current position, and set the new
		// paths speed value.
		%pathCamera.reset(%speed);

.. cpp:function:: void PathCamera::setPosition(float position)

	Set the current position of the camera along the path.

	:param position: Position along the path, from 0.0 (path start) - 1.0 (path end), to place the camera.

	Example::

		// Set the camera on a position along its path from 0.0 - 1.0.
		%position = "0.35";
		
		// Force the pathCamera to its new position along the path.
		%pathCamera.setPosition(%position);

.. cpp:function:: void PathCamera::setState(string newState)

	Set the movement state for this path camera.

	:param newState: New movement state type for this camera. Forward, Backward or Stop.

	Example::

		// Set the state type (forward, backward, stop).
		// In this example, the camera will travel from the first node
		// to the last node (or target if given with setTarget())
		%state = "forward";
		
		// Inform the pathCamera to change its movement state to the defined value.
		%pathCamera.setState(%state);

.. cpp:function:: void PathCamera::setTarget(float position)

	Set the movement target for this camera along its path. The camera will attempt to move along the path to the given target in the direction provided by setState() (the default is forwards). Once the camera moves past this target it will come to a stop, and the target state will be cleared.

	:param position: Target position, between 0.0 (path start) and 1.0 (path end), for the camera to move to along its path.

	Example::

		// Set the position target, between 0.0 (path start) 
		// and 1.0 (path end), for this camera to move to.
		%position = "0.50";
		
		// Inform the pathCamera of the new target position it will move to.
		%pathCamera.setTarget(%position);
