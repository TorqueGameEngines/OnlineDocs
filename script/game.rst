Game
====

Classes
-------

.. toctree::
	:maxdepth: 1

	class/SimObject
	class/SimSet
	class/SimGroup
	class/SimDataBlock

Functions
---------

.. cpp:function:: bool addBadWord(string badWord)

	Add a string to the bad word filter. The bad word filter is a table containing words which will not be displayed in chat windows. Instead, a designated replacement string will be displayed. There are already a number of bad words automatically defined.

	:param badWord: Exact text of the word to restrict.

	:return: True if word was successfully added, false if the word or a subset of it already exists in the table 

	Example::

		// In this game, "Foobar" is banned
		%badWord = "Foobar";
		
		// Returns true, word was successfully added
		addBadWord(%badWord);
		
		// Returns false, word has already been added
		addBadWord("Foobar");

.. cpp:function:: bool containerBoxEmpty(int mask, Point3F center, float xRadius, float yRadius, float zRadius, bool useClientContainer)

	See if any objects of the given types are present in box of given extent.

	:param mask: Indicates the type of objects we are checking against.
	:param center: Center of box.
	:param xRadius: Search radius in the x-axis. See note above.
	:param yRadius: Search radius in the y-axis. See note above.
	:param zRadius: Search radius in the z-axis. See note above.
	:param useClientContainer: Optionally indicates the search should be within the client container.

	:return: true if the box is empty, false if any object is found. 

.. cpp:function:: string containerFindFirst(int mask, Point3F point, float x, float y, float z)

	Find objects matching the bitmask type within a box centered at point, with extents x, y, z.

	:return: .

.. cpp:function:: string containerFindNext()

	Get more results from a previous call to containerFindFirst() .

	:return: The next object found, or an empty string if nothing else was found. 

.. cpp:function:: string containerRayCast(Point3F start, Point3F end, int mask, SceneObject pExempt, bool useClientContainer)

	Cast a ray from start to end, checking for collision against items matching mask. If pExempt is specified, then it is temporarily excluded from collision checks (For instance, you might want to exclude the player if said player was firing a weapon.)

	:param start: An XYZ vector containing the tail position of the ray.
	:param end: An XYZ vector containing the head position of the ray
	:param mask: A bitmask corresponding to the type of objects to check for
	:param pExempt: An optional ID for a single object that ignored for this raycast
	:param useClientContainer: Optionally indicates the search should be within the client container.

	:return: The distance between the start point and the position we hit.

.. cpp:function:: float containerSearchCurrDist(bool useClientContainer)

	Get distance of the center of the current item from the center of the current initContainerRadiusSearch.

	:param useClientContainer: Optionally indicates the search should be within the client container.

	:return: distance from the center of the current object to the center of the search 

.. cpp:function:: float containerSearchCurrRadiusDist(bool useClientContainer)

	Get the distance of the closest point of the current item from the center of the current initContainerRadiusSearch.

	:param useClientContainer: Optionally indicates the search should be within the client container.

	:return: distance from the closest point of the current object to the center of the search 

.. cpp:function:: SceneObject  containerSearchNext(bool useClientContainer)

	Get next item from a search started with initContainerRadiusSearch() or initContainerTypeSearch() .

	:param useClientContainer: Optionally indicates the search should be within the client container.

	:return: the next object found in the search, or null if no more 

	Example::

		// print the names of all nearby ShapeBase derived objects
		%position = %obj.getPosition;
		%radius = 20;
		%mask = $TypeMasks::ShapeBaseObjectType;
		initContainerRadiusSearch( %position, %radius, %mask );
		while ( (%targetObject = containerSearchNext()) != 0 )
		{
		   echo( "Found: " @ %targetObject.getName() );
		}

.. cpp:function:: bool containsBadWords(string text)

	Checks to see if text is a bad word. The text is considered to be a bad word if it has been added to the bad word filter.

	:param text: Text to scan for bad words

	:return: True if the text has bad word(s), false if it is clean 

	Example::

		// In this game, "Foobar" is banned
		%badWord = "Foobar";
		
		// Add a banned word to the bad word filteraddBadWord(%badWord);
		
		// Create the base string, can come from anywhere like user chat
		%userText = "Foobar";
		
		// Create a string of random letters
		%replacementChars = "knqwrtlzs";
		
		// If the text contains a bad word, filter it before printing
		// Otherwise print the original text
		if(containsBadWords(%userText))
		{
		   // Filter the string
		   %filteredText = filterString(%userText, %replacementChars);
		
		   // Print filtered text
		   echo(%filteredText);
		}
		elseecho(%userText);

.. cpp:function:: string filterString(string baseString, string replacementChars)

	Replaces the characters in a string with designated text. Uses the bad word filter to determine which characters within the string will be replaced.

	:param baseString: The original string to filter.
	:param replacementChars: A string containing letters you wish to swap in the baseString.

	:return: The new scrambled string 

	Example::

		// Create the base string, can come from anywhere
		%baseString = "Foobar";
		
		// Create a string of random letters
		%replacementChars = "knqwrtlzs";
		
		// Filter the string
		%newString = filterString(%baseString, %replacementChars);
		
		// Print the new string to consoleecho(%newString);

.. cpp:function:: String getOVRHMDChromaticAbCorrection(int index)

	Provides the OVR HMD chromatic aberration correction values.

	:param index: The HMD index.

	:return: A four component string with the chromatic aberration correction values. 

.. cpp:function:: int getOVRHMDCount()

	Get the number of HMD devices that are currently connected.

	:return: The number of Oculus VR HMD devices that are currently connected. 

.. cpp:function:: float getOVRHMDCurrentIPD(int index)

	Physical distance between the user's eye centers.

	:param index: The HMD index.

	:return: The current IPD. 

.. cpp:function:: Point2I getOVRHMDDisplayDesktopPos(int index)

	Desktop coordinate position of the screen (can be negative; may not be present on all platforms).

	:param index: The HMD index.

	:return: Position of the screen. 

.. cpp:function:: int getOVRHMDDisplayDeviceId(int index)

	MacOS display ID.

	:param index: The HMD index.

	:return: The ID of the HMD display device, if any. 

.. cpp:function:: string getOVRHMDDisplayDeviceName(int index)

	Windows display device name used in EnumDisplaySettings/CreateDC.

	:param index: The HMD index.

	:return: The name of the HMD display device, if any. 

.. cpp:function:: String getOVRHMDDistortionCoefficients(int index)

	Provides the OVR HMD distortion coefficients.

	:param index: The HMD index.

	:return: A four component string with the distortion coefficients. 

.. cpp:function:: float getOVRHMDDistortionScale(int index)

	Provides the OVR HMD calculated distortion scale.

	:param index: The HMD index.

	:return: The calculated distortion scale. 

.. cpp:function:: Point2F getOVRHMDEyeXOffsets(int index)

	Provides the OVR HMD eye x offsets in uv coordinates.

	:param index: The HMD index.

	:return: A two component string with the left and right eye x offsets. 

.. cpp:function:: string getOVRHMDManufacturer(int index)

	Retrieves the HMD manufacturer name.

	:param index: The HMD index.

	:return: The manufacturer of the HMD product. 

.. cpp:function:: string getOVRHMDProductName(int index)

	Retrieves the HMD product name.

	:param index: The HMD index.

	:return: The name of the HMD product. 

.. cpp:function:: float getOVRHMDProfileIPD(int index)

	Physical distance between the user's eye centers as defined by the current profile.

	:param index: The HMD index.

	:return: The profile IPD. 

.. cpp:function:: Point2I getOVRHMDResolution(int index)

	Provides the OVR HMD screen resolution.

	:param index: The HMD index.

	:return: A two component string with the screen's resolution. 

.. cpp:function:: int getOVRHMDVersion(int index)

	Retrieves the HMD version number.

	:param index: The HMD index.

	:return: The version number of the HMD product. 

.. cpp:function:: float getOVRHMDXCenterOffset(int index)

	Provides the OVR HMD calculated XCenterOffset.

	:param index: The HMD index.

	:return: The calculated XCenterOffset. 

.. cpp:function:: float getOVRHMDYFOV(int index)

	Provides the OVR HMD calculated Y FOV.

	:param index: The HMD index.

	:return: The calculated Y FOV. 

.. cpp:function:: Point3F getOVRSensorAcceleration(int index)

	Get the acceleration values for the given sensor index.

	:param index: The sensor index.

	:return: The acceleration values of the Oculus VR sensor, in m/s^2. 

.. cpp:function:: Point3F getOVRSensorAngVelocity(int index)

	Get the angular velocity values for the given sensor index.

	:param index: The sensor index.

	:return: The angular velocity values of the Oculus VR sensor, in degrees/s. 

.. cpp:function:: int getOVRSensorCount()

	Get the number of sensor devices that are currently connected.

	:return: The number of Oculus VR sensor devices that are currently connected. 

.. cpp:function:: Point3F getOVRSensorEulerRotation(int index)

	Get the Euler rotation values for the given sensor index.

	:param index: The sensor index.

	:return: The Euler rotation values of the Oculus VR sensor, in degrees. 

.. cpp:function:: bool getOVRSensorGravityCorrection(int index)

	Get the gravity correction state for the given sensor index.

	:param index: The sensor index.

	:return: True if gravity correction (for pitch and roll) is active. 

.. cpp:function:: Point3F getOVRSensorMagnetometer(int index)

	Get the magnetometer reading (direction and field strength) for the given sensor index.

	:param index: The sensor index.

	:return: The magnetometer reading (direction and field strength) of the Oculus VR sensor, in Gauss. 

.. cpp:function:: bool getOVRSensorMagnetometerCalibrated(int index)

	Get the magnetometer calibrated data state for the given sensor index.

	:param index: The sensor index.

	:return: True if magnetometer calibration data is available. 

.. cpp:function:: float getOVRSensorPredictionTime(int index)

	Get the prediction time set for the given sensor index.

	:param index: The sensor index.

	:return: The prediction time of the Oculus VR sensor, given in seconds. 

.. cpp:function:: bool getOVRSensorYawCorrection(int index)

	Get the yaw correction state for the given sensor index.

	:param index: The sensor index.

	:return: True if yaw correction (using magnetometer calibration data) is active. 

.. cpp:function:: Point3F getRazerHydraControllerPos(int controller)

	Get the given Razer Hydra controller's last position.

	:param controller: Controller number to check.

	:return: A Point3F containing the last known position. 

.. cpp:function:: AngAxisF getRazerHydraControllerRot(int controller)

	Get the given Razer Hydra controller's last rotation.

	:param controller: Controller number to check.

	:return: A AngAxisF containing the last known rotation. 

.. cpp:function:: TransformF getRazerHydraControllerTransform(int controller)

	Get the given Razer Hydra controller's last transform.

	:param controller: Controller number to check.

	:return: A TransformF containing the last known transform. 

.. cpp:function:: void initContainerRadiusSearch(Point3F pos, float radius, int mask, bool useClientContainer)

	Start a search for items at the given position and within the given radius, filtering by mask.

	:param pos: Center position for the search
	:param radius: Search radius
	:param mask: Bitmask of object types to include in the search
	:param useClientContainer: Optionally indicates the search should be within the client container.

.. cpp:function:: void initContainerTypeSearch(int mask, bool useClientContainer)

	Start a search for all items of the types specified by the bitset mask.

	:param mask: Bitmask of object types to include in the search
	:param useClientContainer: Optionally indicates the search should be within the client container.

.. cpp:function:: bool isLeapMotionActive()

	Used to determine if the Leap Motion input device is active. The Leap Motion input device is considered active when the support library has been loaded and the device has been found.

	:return: True if the Leap Motion input device is active. 

.. cpp:function:: bool isOculusVRDeviceActive()

	Used to determine if the Oculus VR input device is active. The Oculus VR device is considered active when the library has been initialized and either a real of simulated HMD is present.

	:return: True if the Oculus VR input device is active. 

.. cpp:function:: bool isOVRHMDSimulated(int index)

	Determines if the requested OVR HMD is simulated or real.

	:param index: The HMD index.

	:return: True if the HMD is simulated. 

.. cpp:function:: bool isRazerHydraActive()

	Used to determine if the Razer Hydra input device active. The Razer Hydra input device is considered active when the support library has been loaded and the controller has been found.

	:return: True if the Razer Hydra input device is active. 

.. cpp:function:: bool isRazerHydraControllerDocked(int controller)

	Used to determine if the given Razer Hydra controller is docked.

	:param controller: Controller number to check.

	:return: True if the given Razer Hydra controller is docked. Also returns true if the input device is not found or active. 

.. cpp:function:: void ovrResetAllSensors()

	Resets all Oculus VR sensors. This resets all sensor orientations such that their 'normal' rotation is defined when this function is called. This defines an HMD's forwards and up direction, for example.

.. cpp:function:: void resetFPSTracker()

	Reset FPS stats (fps::).

.. cpp:function:: void sceneDumpZoneStates(bool updateFirst)

	Dump the current zoning states of all zone spaces in the scene to the console.

	:param updateFirst: If true, zoning states are brought up to date first; if false, the zoning states are dumped as is.

.. cpp:function:: SceneObject  sceneGetZoneOwner(int zoneId)

	Return the SceneObject that contains the given zone.

	:param zoneId: ID of zone.

	:return:  is invalid.

.. cpp:function:: void setAllSensorPredictionTime(float dt)

	Set the prediction time set for all sensors.

	:param dt: The prediction time to set given in seconds. Setting to 0 disables prediction.

.. cpp:function:: bool setOVRHMDAsGameConnectionDisplayDevice(GameConnection conn)

	Sets the first HMD to be a GameConnection's display device.

	:param conn: The GameConnection to set.

	:return:  display device was set. 

.. cpp:function:: void setOVRHMDCurrentIPD(int index, float ipd)

	Set the physical distance between the user's eye centers.

	:param index: The HMD index.
	:param ipd: The IPD to use.

.. cpp:function:: void setOVRSensorGravityCorrection(int index, bool state)

	Set the gravity correction state for the given sensor index.

	:param index: The sensor index.
	:param state: The gravity correction state to change to.

.. cpp:function:: void setOVRSensorYawCorrection(int index, bool state)

	Set the yaw correction state for the given sensor index.

	:param index: The sensor index.
	:param state: The yaw correction state to change to.

.. cpp:function:: void setSensorPredictionTime(int index, float dt)

	Set the prediction time set for the given sensor index.

	:param index: The sensor index.
	:param dt: The prediction time to set given in seconds. Setting to 0 disables prediction.

.. cpp:function:: bool spawnObject(class [, dataBlock, name, properties, script])

	Global function used for spawning any type of object. Note: This is separate from SpawnSphere::spawnObject() . This function is not called off any other class and uses different parameters than the SpawnSphere's function. In the source, SpawnSphere::spawnObject() actually calls this function and passes its properties (spawnClass, spawnDatablock, etc).

	:param class: Mandatory field specifying the object class, such as Player or TSStatic.
	:param datablock: Field specifying the object's datablock, optional for objects such as TSStatic, mandatory for game objects like Player.
	:param name: Optional field specifying a name for this instance of the object.
	:param properties: Optional set of parameters applied to the spawn object during creation.
	:param script: Optional command(s) to execute when spawning an object.

	Example::

		// Set the parameters for the spawn function
		%objectClass = "Player";
		%objectDatablock = "DefaultPlayerData";
		%objectName = "PlayerName";
		%additionalProperties = "health = \"0\";"; // Note the escape sequence \ in front of quotes
		%spawnScript = "echo(\"Player Spawned\");"// Note the escape sequence \ in front of quotes// Spawn with the engines Sim::spawnObject() function
		%player = spawnObject(%objectClass, %objectDatablock, %objectName, %additionalProperties, %spawnScript);

Variables
---------

.. cpp:member:: float $cameraFov

	The camera's Field of View.

.. cpp:member:: float $mvBackwardAction

	Backwards movement speed for the active player.

.. cpp:member:: bool $mvDeviceIsKeyboardMouse

	Boolean state for it the system is using a keyboard and mouse or not.

.. cpp:member:: float $mvDownAction

	Downwards movement speed for the active player.

.. cpp:member:: float $mvForwardAction

	Forwards movement speed for the active player.

.. cpp:member:: bool $mvFreeLook

	Boolean state for if freelook is active or not.

.. cpp:member:: float $mvLeftAction

	Left movement speed for the active player.

.. cpp:member:: float $mvPitch

	Current pitch value, typically applied through input devices, such as a mouse.

.. cpp:member:: float $mvPitchDownSpeed

	Downwards pitch speed.

.. cpp:member:: float $mvPitchUpSpeed

	Upwards pitch speed.

.. cpp:member:: float $mvRightAction

	Right movement speed for the active player.

.. cpp:member:: float $mvRoll

	Current roll value, typically applied through input devices, such as a mouse.

.. cpp:member:: float $mvRollLeftSpeed

	Left roll speed.

.. cpp:member:: float $mvRollRightSpeed

	Right roll speed.

.. cpp:member:: int $mvTriggerCount0

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: int $mvTriggerCount1

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: int $mvTriggerCount2

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: int $mvTriggerCount3

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: int $mvTriggerCount4

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: int $mvTriggerCount5

	Used to determine the trigger counts of buttons. Namely used for input actions such as jumping and weapons firing.

.. cpp:member:: float $mvUpAction

	Upwards movement speed for the active player.

.. cpp:member:: float $mvXAxis_L

	Left thumbstick X axis position on a dual-analog gamepad.

.. cpp:member:: float $mvXAxis_R

	Right thumbstick X axis position on a dual-analog gamepad.

.. cpp:member:: float $mvYaw

	Current yaw value, typically applied through input devices, such as a mouse.

.. cpp:member:: float $mvYawLeftSpeed

	Left Yaw speed.

.. cpp:member:: float $mvYawRightSpeed

	Right Yaw speed.

.. cpp:member:: float $mvYAxis_L

	Left thumbstick Y axis position on a dual-analog gamepad.

.. cpp:member:: float $mvYAxis_R

	Right thumbstick Y axis position on a dual-analog gamepad.

.. cpp:member:: int $Ease::Back

	Backwards ease for curve movement.

.. cpp:member:: int $Ease::Bounce

	Bounce ease for curve movement.

.. cpp:member:: int $Ease::Circular

	Circular ease for curve movement.

.. cpp:member:: bool $RazerHydra::CombinedPositionEvents

	If true, one position event will be sent that includes one component per argument.

.. cpp:member:: int $Ease::Cubic

	Cubic ease for curve movement.

.. cpp:member:: float $pref::Camera::distanceScale

	A scale to apply to the normal visible distance, typically used for tuning performance.

.. cpp:member:: int $Ease::Elastic

	Elastic ease for curve movement.

.. cpp:member:: bool $pref::enableBadWordFilter

	If true, the bad word filter will be enabled.

.. cpp:member:: bool $pref::LeapMotion::EnableDevice

	If true, the Leap Motion device will be enabled, if present.

.. cpp:member:: bool $pref::OculusVR::EnableDevice

	If true, the Oculus VR device will be enabled, if present.

.. cpp:member:: bool $pref::RazerHydra::EnableDevice

	If true, the Razer Hydra device will be enabled, if present.

.. cpp:member:: bool $pref::enablePostEffects

	If true, post effects will be eanbled.

.. cpp:member:: int $Ease::Exponential

	Exponential ease for curve movement.

.. cpp:member:: bool $OculusVR::GenerateAngleAxisRotationEvents

	If true, broadcast sensor rotation events as angled axis.

.. cpp:member:: bool $OculusVR::GenerateEulerRotationEvents

	If true, broadcast sensor rotation events as Euler angles about the X, Y and Z axis.

.. cpp:member:: bool $LeapMotion::GenerateIndividualEvents

	Indicates that events for each hand and pointable will be created.

.. cpp:member:: bool $OculusVR::GenerateRotationAsAxisEvents

	If true, broadcast sensor rotation as axis events.

.. cpp:member:: bool $OculusVR::GenerateSensorRawEvents

	If ture, broadcast sensor raw data: acceleration, angular velocity, magnetometer reading.

.. cpp:member:: bool $LeapMotion::GenerateSingleHandRotationAsAxisEvents

	If true, broadcast single hand rotation as axis events.

.. cpp:member:: bool $LeapMotion::GenerateWholeFrameEvents

	Indicates that a whole frame event should be generated and frames should be buffered.

.. cpp:member:: bool $OculusVR::GenerateWholeFrameEvents

	Indicates that a whole frame event should be generated and frames should be buffered.

.. cpp:member:: bool $RazerHydra::GenerateWholeFrameEvents

	Indicates that a whole frame event should be generated and frames should be buffered.

.. cpp:member:: int $Ease::In

	In ease for curve movement.

.. cpp:member:: int $Ease::InOut

	InOut ease for curve movement.

.. cpp:member:: bool $pref::Input::JoystickEnabled

	If true, the joystick is currently enabled.

.. cpp:member:: bool $LeapMotion::KeepHandIndexPersistent

	Indicates that we track hand IDs and will ensure that the same hand will remain at the same index between frames.

.. cpp:member:: bool $LeapMotion::KeepPointableIndexPersistent

	Indicates that we track pointable IDs and will ensure that the same pointable will remain at the same index between frames.

.. cpp:member:: int $Ease::Linear

	Linear ease for curve movement.

.. cpp:member:: float $OculusVR::MaximumAxisAngle

	The maximum sensor angle when used as an axis event as measured from a vector pointing straight up (in degrees). Should range from 0 to 90 degrees.

.. cpp:member:: float $RazerHydra::MaximumAxisAngle

	The maximum controller angle when used as an axis event as measured from a vector pointing straight up (in degrees). Shoud range from 0 to 90 degrees.

.. cpp:member:: int $LeapMotion::MaximumFramesStored

	The maximum number of frames to keep when $LeapMotion::GenerateWholeFrameEvents is true.

.. cpp:member:: int $RazerHydra::MaximumFramesStored

	The maximum number of frames to keep when $RazerHydra::GenerateWholeFrameEvents is true.

.. cpp:member:: float $LeapMotion::MaximumHandAxisAngle

	The maximum hand angle when used as an axis event as measured from a vector pointing straight up (in degrees). Shoud range from 0 to 90 degrees.

.. cpp:member:: int $Ease::Out

	Out ease for curve movement.

.. cpp:member:: bool $RazerHydra::ProcessWhenDocked

	If true, events will still be sent when a controller is docked.

.. cpp:member:: int $Ease::Quadratic

	Quadratic ease for curve movement.

.. cpp:member:: int $Ease::Quartic

	Quartic ease for curve movement.

.. cpp:member:: int $Ease::Quintic

	Quintic ease for curve movement.

.. cpp:member:: bool $RazerHydra::RotationAsAxisEvents

	If true, broadcast controller rotation as axis events.

.. cpp:member:: bool $RazerHydra::SeparatePositionEvents

	If true, separate position events will be sent for each component.

.. cpp:member:: int $Ease::Sinusoidal

	Sinusoidal ease for curve movement.

.. cpp:member:: bool $pref::OculusVR::UseChromaticAberrationCorrection

	If true, Use the chromatic aberration correction version of the Oculus VR barrel distortion shader.
