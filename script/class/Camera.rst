Camera
======

Represents a position, direction and field of view to render a scene from.

Inherit:
	:doc:`ShapeBase`

Description
-----------

A camera is typically manipulated by a GameConnection. When set as the connection's control object, the camera handles all movement actions ($mvForwardAction, $mvPitch, etc.) just like a Player.

Example::

	// Set an already created camera as the GameConnections control object
	%connection.setControlObject(%camera);

Methods of Operation
~~~~~~~~~~~~~~~~~~~~

The camera has two general methods of operation. The first is the standard mode where the camera starts and stops its motion and rotation instantly. This is the default operation of the camera and is used by most games. It may be specifically set with Camera::setFlyMode() for 6 DoF motion. It is also typically the method used with Camera::setOrbitMode() or one of its helper methods to orbit about a specific object (such as the Player's dead body) or a specific point.

The second method goes under the name of Newton as it follows Newton's 2nd law of motion: F=ma. This provides the camera with an ease-in and ease-out feel for both movement and rotation. To activate this method for movement, either use Camera::setNewtonFlyMode() or set the Camera::newtonMode field to true. To activate this method for rotation, set the Camera::newtonRotation to true. This method of operation is not typically used in games, and was developed to allow for a smooth fly through of a game level while recording a demo video. But with the right force and drag settings, it may give a more organic feel to the camera to games that use an overhead view, such as a RTS.

There is a third, minor method of operation but it is not generally used for games. This is when the camera is used with Torque's World Editor in Edit Orbit Mode. When set, this allows the camera to rotate about a specific point in the world, and move towards and away from this point. See Camera::setEditOrbitMode() and Camera::setEditOrbitPoint(). While in this mode, Camera::autoFitRadius() may also be used.

Example::

	// Create a camera in the level and set its position to a given spawn point.
	// Note: The camera starts in the standard fly mode.
	%cam = newCamera() {
	   datablock = "Observer";
	};
	MissionCleanup.add( %cam );
	%cam.setTransform( %spawnPoint.getTransform() );

Example::

	// Create a camera at the given spawn point for the specified
	// GameConnection i.e. the client.  Uses the standard
	// Sim::spawnObject() function to create the camera using the
	// defined default settings.
	// Note: The camera starts in the standard fly mode.
	function GameConnection::spawnCamera(%this, %spawnPoint)
	{
	   // Set the control object to the default camera
	   if (!isObject(%this.camera))
	   {
	      if (isDefined("$Game::DefaultCameraClass"))
	         %this.camera = spawnObject($Game::DefaultCameraClass, $Game::DefaultCameraDataBlock);
	   }
	
	   // If we have a camera then set up some properties
	   if (isObject(%this.camera))
	   {
	      // Make sure were cleaned up when the mission ends
	      MissionCleanup.add( %this.camera );
	
	      // Make sure the camera is always in scope for the connection
	      %this.camera.scopeToClient(%this);
	
	      // Send all user input from the connection to the camera
	      %this.setControlObject(%this.camera);
	
	      if (isDefined("%spawnPoint"))
	      {
	         // Attempt to treat %spawnPoint as an object, such as a
	         // SpawnSphere class.
	         if (getWordCount(%spawnPoint) == 1 &&isObject(%spawnPoint))
	         {
	            %this.camera.setTransform(%spawnPoint.getTransform());
	         }
	         else
	         {
	            // Treat %spawnPoint as an AngleAxis transform
	            %this.camera.setTransform(%spawnPoint);
	         }
	      }
	   }
	}

Motion Modes
~~~~~~~~~~~~

Beyond the different operation methods, the Camera may be set to one of a number of motion modes. These motion modes determine how the camera will respond to input and may be used to constrain how the Camera moves. The CameraMotionMode enumeration defines the possible set of modes and the Camera's current may be obtained by using getMode().

Some of the motion modes may be set using specific script methods. These often provide additional parameters to set up the mode in one go. Otherwise, it is always possible to set a Camera's motion mode using the controlMode property. Just pass in the name of the mode enum. The following table lists the motion modes, how to set them up, and what they offer:

===========================  ====================  =============  ==================  ====================
Mode                         Set From Script       Input Move     Input Rotate        Can Use Newton Mode?
Stationary                   controlMode property  No             No                  No
FreeRotate                   controlMode property  No             Yes                 Rotate Only
Fly                          setFlyMode()          Yes            Yes                 Yes
OrbitObject                  setOrbitMode()        Orbits object  Points to object    Move only
OrbitPoint                   setOrbitPoint()       Orbits point	  Points to location  Move only
TrackObject                  setTrackObject()      No             Points to object    Yes
Overhead                     controlMode property  Yes            No                  Yes
EditOrbit (object selected)  setEditOrbitMode()    Orbits object  Points to object    Move only
EditOrbit (no object)        setEditOrbitMode()    Yes            Yes                 Yes
===========================  ====================  =============  ==================  ====================

Trigger Input
~~~~~~~~~~~~~

Passing a move trigger ($mvTriggerCount0, $mvTriggerCount1, etc.) on to a Camera performs different actions depending on which mode the camera is in. While in Fly, Overhead or EditOrbit mode, either trigger0 or trigger1 will cause a camera to move twice its normal movement speed. You can see this in action within the World Editor, where holding down the left mouse button while in mouse look mode (right mouse button is also down) causes the Camera to move faster.

Passing along trigger2 will put the camera into strafe mode. While in this mode a Fly, FreeRotate or Overhead Camera will not rotate from the move input. Instead the yaw motion will be applied to the Camera's x motion, and the pitch motion will be applied to the Camera's z motion. You can see this in action within the World Editor where holding down the middle mouse button allows the user to move the camera up, down and side-to-side.

While the camera is operating in Newton Mode, trigger0 and trigger1 behave slightly differently. Here trigger0 activates a multiplier to the applied acceleration force as defined by speedMultiplier. This has the affect of making the camera move up to speed faster. trigger1 has the opposite affect by acting as a brake. When trigger1 is active a multiplier is added to the Camera's drag as defined by brakeMultiplier.

Methods
-------

.. cpp:function:: void Camera::autoFitRadius(float radius)

	Move the camera to fully view the given radius.

	:param radius: The radius to view.

.. cpp:function:: VectorF Camera::getAngularVelocity()

	Get the angular velocity for a Newton mode camera.

	:return: The angular velocity in the form of "x y z". 

.. cpp:function:: Camera::CameraMotionMode  Camera::getMode()

	Returns the current camera control mode.

.. cpp:function:: Point3F Camera::getOffset()

	Get the camera's offset from its orbit or tracking point. The offset is added to the camera's position when set to CameraMode::OrbitObject.

	:return: The offset in the form of "x y z". 

.. cpp:function:: Point3F Camera::getPosition()

	Get the camera's position in the world. Reimplemented from SceneObject .

	:return: The position in the form of "x y z". 

.. cpp:function:: Point3F Camera::getRotation()

	Get the camera's Euler rotation in radians.

	:return: The rotation in radians in the form of "x y z". 

.. cpp:function:: VectorF Camera::getVelocity()

	Get the velocity for the camera. Reimplemented from ShapeBase .

	:return: The camera's velocity in the form of "x y z".

.. cpp:function:: bool Camera::isEditOrbitMode()

	Is the camera in edit orbit mode?

	:return: true if the camera is in edit orbit mode. 

.. cpp:function:: bool Camera::isRotationDamped()

	Is this a Newton Fly mode camera with damped rotation?

	:return:  is set to true. 

.. cpp:function:: void Camera::lookAt(Point3F point)

	Point the camera at the specified position. Does not work in Orbit or Track modes.

	:param point: The position to point the camera at.

.. cpp:function:: void Camera::setAngularDrag(float drag)

	Set the angular drag for a Newton mode camera.

	:param drag: The angular drag applied while the camera is rotating.

.. cpp:function:: void Camera::setAngularForce(float force)

	Set the angular force for a Newton mode camera.

	:param force: The angular force applied when attempting to rotate the camera.

.. cpp:function:: void Camera::setAngularVelocity(VectorF velocity)

	Set the angular velocity for a Newton mode camera.

	:param velocity: The angular velocity infor form of "x y z".

.. cpp:function:: void Camera::setBrakeMultiplier(float multiplier)

	Set the Newton mode camera brake multiplier when trigger[1] is active.

	:param multiplier: The brake multiplier to apply.

.. cpp:function:: void Camera::setDrag(float drag)

	Set the drag for a Newton mode camera.

	:param drag: The drag applied to the camera while moving.

.. cpp:function:: void Camera::setEditOrbitMode()

	Set the editor camera to orbit around a point set with Camera::setEditOrbitPoint() .

.. cpp:function:: void Camera::setEditOrbitPoint(Point3F point)

	Set the editor camera's orbit point.

	:param point: The point the camera will orbit in the form of "x y z".

.. cpp:function:: void Camera::setFlyForce(float force)

	Set the force applied to a Newton mode camera while moving.

	:param force: The force applied to the camera while attempting to move.

.. cpp:function:: void Camera::setFlyMode()

	Set the camera to fly freely. Allows the camera to have 6 degrees of freedom. Provides for instantaneous motion and rotation unless one of the Newton fields has been set to true. See Camera::newtonMode and Camera::newtonRotation .

.. cpp:function:: void Camera::setMass(float mass)

	Set the mass for a Newton mode camera.

	:param mass: The mass used during ease-in and ease-out calculations.

.. cpp:function:: void Camera::setNewtonFlyMode()

	Set the camera to fly freely, but with ease-in and ease-out. This method allows for the same 6 degrees of freedom as Camera::setFlyMode() but activates the ease-in and ease-out on the camera's movement. To also activate Newton mode for the camera's rotation, set Camera::newtonRotation to true.

.. cpp:function:: void Camera::setOffset(Point3F offset)

	Set the camera's offset. The offset is added to the camera's position when set to CameraMode::OrbitObject.

	:param offset: The distance to offset the camera by in the form of "x y z".

.. cpp:function:: void Camera::setOrbitMode(GameBase orbitObject, TransformF orbitPoint, float minDistance, float maxDistance, float initDistance, bool ownClientObj, Point3F offset, bool locked)

	Set the camera to orbit around the given object, or if none is given, around the given point.

	:param orbitObject: The object to orbit around. If no object is given (0 or blank string is passed in) use the orbitPoint instead
	:param orbitPoint: The point to orbit around when no object is given. In the form of "x y z ax ay az aa" such as returned by SceneObject::getTransform().
	:param minDistance: The minimum distance allowed to the orbit object or point.
	:param maxDistance: The maximum distance allowed from the orbit object or point.
	:param initDistance: The initial distance from the orbit object or point.
	:param ownClientObj: [optional] Are we orbiting an object that is owned by us? Default is false.
	:param offset: [optional] An offset added to the camera's position. Default is no offset.
	:param locked: [optional] Indicates the camera does not receive input from the player. Default is false.

.. cpp:function:: bool Camera::setOrbitObject(GameBase orbitObject, VectorF rotation, float minDistance, float maxDistance, float initDistance, bool ownClientObject, Point3F offset, bool locked)

	Set the camera to orbit around a given object.

	:param orbitObject: The object to orbit around.
	:param rotation: The initial camera rotation about the object in radians in the form of "x y z".
	:param minDistance: The minimum distance allowed to the orbit object or point.
	:param maxDistance: The maximum distance allowed from the orbit object or point.
	:param initDistance: The initial distance from the orbit object or point.
	:param ownClientObject: [optional] Are we orbiting an object that is owned by us? Default is false.
	:param offset: [optional] An offset added to the camera's position. Default is no offset.
	:param locked: [optional] Indicates the camera does not receive input from the player. Default is false.

	:return: false if the given object could not be found. 

.. cpp:function:: void Camera::setOrbitPoint(TransformF orbitPoint, float minDistance, float maxDistance, float initDistance, Point3F offset, bool locked)

	Set the camera to orbit around a given point.

	:param orbitPoint: The point to orbit around. In the form of "x y z ax ay az aa" such as returned by SceneObject::getTransform().
	:param minDistance: The minimum distance allowed to the orbit object or point.
	:param maxDistance: The maximum distance allowed from the orbit object or point.
	:param initDistance: The initial distance from the orbit object or point.
	:param offset: [optional] An offset added to the camera's position. Default is no offset.
	:param locked: [optional] Indicates the camera does not receive input from the player. Default is false.

.. cpp:function:: void Camera::setRotation(Point3F rot)

	Set the camera's Euler rotation in radians.

	:param rot: The rotation in radians in the form of "x y z".

.. cpp:function:: void Camera::setSpeedMultiplier(float multiplier)

	Set the Newton mode camera speed multiplier when trigger[0] is active.

	:param multiplier: The speed multiplier to apply.

.. cpp:function:: bool Camera::setTrackObject(GameBase trackObject, Point3F offset)

	Set the camera to track a given object.

	:param trackObject: The object to track.
	:param offset: [optional] An offset added to the camera's position. Default is no offset.

	:return: false if the given object could not be found. 

.. cpp:function:: void Camera::setValidEditOrbitPoint(bool validPoint)

	Set if there is a valid editor camera orbit point. When validPoint is set to false the Camera operates as if it is in Fly mode rather than an Orbit mode.

	:param validPoint: Indicates the validity of the orbit point.

.. cpp:function:: void Camera::setVelocity(VectorF velocity)

	Set the velocity for the camera.

	:param velocity: The camera's velocity in the form of "x y z".

Fields
------

.. cpp:member:: float  Camera::angularDrag

	Drag on camera when rotating (Newton mode only). Default value is 2.

.. cpp:member:: float  Camera::angularForce

	Force applied on camera when asked to rotate (Newton mode only). Default value is 100.

.. cpp:member:: float  Camera::brakeMultiplier

	Speed multiplier when triggering the brake (Newton mode only). Default value is 2.

.. cpp:member:: CameraMotionMode Camera::controlMode

	The current camera control mode.

.. cpp:member:: float  Camera::drag

	Drag on camera when moving (Newton mode only). Default value is 2.

.. cpp:member:: float  Camera::force

	Force applied on camera when asked to move (Newton mode only). Default value is 500.

.. cpp:member:: float  Camera::mass

	The camera's mass (Newton mode only). Default value is 10.

.. cpp:member:: bool  Camera::newtonMode

	Apply smoothing (acceleration and damping) to camera movements.

.. cpp:member:: bool  Camera::newtonRotation

	Apply smoothing (acceleration and damping) to camera rotations.

.. cpp:member:: float  Camera::speedMultiplier

	Speed multiplier when triggering the accelerator (Newton mode only). Default value is 2.
