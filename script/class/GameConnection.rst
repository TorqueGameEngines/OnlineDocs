GameConnection
==============

The game-specific subclass of NetConnection.

Inherit:
	:doc:`NetConnection`

Description
-----------

The GameConnection introduces the concept of the control object. The control object is simply the object that the client is associated with that network connection controls. By default the control object is an instance of the Player class, but can also be an instance of Camera (when editing the mission, for example), or any other ShapeBase derived class as appropriate for the game.

Torque uses a model in which the server is the authoritative master of the simulation. To prevent clients from cheating, the server simulates all player moves and then tells the client where his player is in the world. This model, while secure, can have problems. If the network latency is high, this round-trip time can give the player a very noticeable sense of movement lag. To correct this problem, the game uses a form of prediction - it simulates the movement of the control object on the client and on the server both. This way the client doesn't need to wait for round-trip verification of his moves. Only in the case of a force acting on the control object on the server that doesn't exist on the client does the client's position need to be forcefully changed.

To support this, all control objects (derivative of ShapeBase) must supply a writePacketData() and readPacketData() function that send enough data to accurately simulate the object on the client. These functions are only called for the current control object, and only when the server can determine that the client's simulation is somehow out of sync with the server. This occurs usually if the client is affected by a force not present on the server (like an interpolating object) or if the server object is affected by a server only force (such as the impulse from an explosion).

The Move structure is a 32 millisecond snapshot of player input, containing x, y, and z positional and rotational changes as well as trigger state changes. When time passes in the simulation moves are collected (depending on how much time passes), and applied to the current control object on the client. The same moves are then packed over to the server in GameConnection::writePacket(), for processing on the server's version of the control object.


Methods
-------

.. cpp:function:: void GameConnection::activateGhosting()

	Called by the server during phase 2 of the mission download to start sending ghosts to the client. Ghosts represent objects on the server that are in scope for the client. These need to be synchronized with the client in order for the client to see and interact with them. This is typically done during the standard mission start phase 2 when following Torque's example mission startup sequence.

	Example::

		function serverCmdMissionStartPhase2Ack(%client, %seq, %playerDB)
		{
		   // Make sure to ignore calls from a previous mission load
		   if (%seq != $missionSequence || !$MissionRunning)
		      return;
		   if (%client.currentPhase != 1.5)
		      return;
		   %client.currentPhase = 2;
		
		   // Set the player datablock choice
		   %client.playerDB = %playerDB;
		
		   // Update mod paths, this needs to get there before the objects.
		   %client.transmitPaths();
		
		   // Start ghosting objects to the client
		   %client.activateGhosting();
		}

.. cpp:function:: bool GameConnection::chaseCam(int size)

	Sets the size of the chase camera's matrix queue.

.. cpp:function:: void GameConnection::clearCameraObject()

	Clear the connection's camera object reference.

.. cpp:function:: void GameConnection::clearDisplayDevice()

	Clear any display device. A display device may define a number of properties that are used during rendering.

.. cpp:function:: void GameConnection::delete(string reason)

	On the server, disconnect a client and pass along an optional reason why. This method performs two operations: it disconnects a client connection from the server, and it deletes the connection object. The optional reason is sent in the disconnect packet and is often displayed to the user so they know why they've been disconnected.

	:param reason: [optional] The reason why the user has been disconnected from the server.

	Example::

		function kick(%client)
		{
		   messageAll( MsgAdminForce, \c2The Admin has kicked %1., %client.playerName);
		
		   if (!%client.isAIControlled())
		      BanList::add(%client.guid, %client.getAddress(), $Pref::Server::KickBanTime);
		   %client.delete("You have been kicked from this server");
		}

.. cpp:function:: SimObject  GameConnection::getCameraObject()

	Returns the connection's camera object used when not viewing through the control object.

.. cpp:function:: float GameConnection::getControlCameraDefaultFov()

	Returns the default field of view as used by the control object's camera.

.. cpp:function:: float GameConnection::getControlCameraFov()

	Returns the field of view as used by the control object's camera.

.. cpp:function:: GameBase  GameConnection::getControlObject()

	On the server, returns the object that the client is controlling.By default the control object is an instance of the Player class, but can also be an instance of Camera (when editing the mission, for example), or any other ShapeBase derived class as appropriate for the game.

.. cpp:function:: bool GameConnection::getControlSchemeAbsoluteRotation()

	Get the connection's control scheme absolute rotation property.

	:return: True if the connection's control object should use an absolute rotation control scheme.

.. cpp:function:: float GameConnection::getDamageFlash()

	On the client, get the control object's damage flash level.

	:return: flash level 

.. cpp:function:: static int GameConnection::getServerConnection()

	On the client, this static mehtod will return the connection to the server, if any.

	:return:  ID of the server connection, or -1 if none is found. 

.. cpp:function:: float GameConnection::getWhiteOut()

	On the client, get the control object's white-out level.

	:return: white-out level 

.. cpp:function:: void GameConnection::initialControlSet()

	Called on the client when the first control object has been set by the server and we are now ready to go. A common action to perform when this callback is called is to switch the GUI canvas from the loading screen and over to the 3D game GUI.

.. cpp:function:: bool GameConnection::isAIControlled()

	Returns true if this connection is AI controlled.

.. cpp:function:: bool GameConnection::isControlObjectRotDampedCamera()

	Returns true if the object being controlled by the client is making use of a rotation damped camera.

.. cpp:function:: bool GameConnection::isDemoPlaying()

	Returns true if a previously recorded demo file is now playing.

.. cpp:function:: bool GameConnection::isDemoRecording()

	Returns true if a demo file is now being recorded.

.. cpp:function:: bool GameConnection::isFirstPerson()

	Returns true if this connection is in first person mode.

.. cpp:function:: void GameConnection::listClassIDs()

	List all of the classes that this connection knows about, and what their IDs are. Useful for debugging network problems.

.. cpp:function:: void GameConnection::onConnectionAccepted()

	Called on the client when the connection to the server has been established.

.. cpp:function:: void GameConnection::onConnectionDropped(string reason)

	Called on the client when the connection to the server has been dropped.

	:param reason: The reason why the connection was dropped.

.. cpp:function:: void GameConnection::onConnectionError(string errorString)

	Called on the client when there is an error with the connection to the server.

	:param errorString: The connection error text.

.. cpp:function:: void GameConnection::onConnectionTimedOut()

	Called on the client when the connection to the server times out.

.. cpp:function:: void GameConnection::onConnectRequestRejected(string reason)

	Called on the client when the connection to the server has been rejected.

	:param reason: The reason why the connection request was rejected.

.. cpp:function:: void GameConnection::onConnectRequestTimedOut()

	Called when connection attempts have timed out.

.. cpp:function:: void GameConnection::onControlObjectChange()

	Called on the client when the control object has been changed by the server.

.. cpp:function:: void GameConnection::onDataBlocksDone(int sequence)

	Called on the server when all datablocks has been sent to the client. During phase 1 of the mission download, all datablocks are sent from the server to the client. Once all datablocks have been sent, this callback is called and the mission download procedure may move on to the next phase.

	:param sequence: The sequence is common between the server and client and ensures that the client is acting on the most recent mission start process. If an errant network packet (one that was lost but has now been found) is received by the client with an incorrect sequence, it is just ignored. This sequence number is updated on the server every time a mission is loaded.

.. cpp:function:: void GameConnection::onDrop(string disconnectReason)

	Called on the server when the client's connection has been dropped.

	:param disconnectReason: The reason why the connection was dropped.

.. cpp:function:: void GameConnection::onFlash(bool state)

	Called on the client when the damage flash or white out states change. When the server changes the damage flash or white out values, this callback is called either is on or both are off. Typically this is used to enable the flash postFx.

	:param state: Set to true if either the damage flash or white out conditions are active.

.. cpp:function:: bool GameConnection::play2D(SFXProfile profile)

	Used on the server to play a 2D sound that is not attached to any object.

	:param profile: The SFXProfile that defines the sound to play.

	Example::

		function ServerPlay2D(%profile)
		{
		   // Play the given sound profile on every client.
		   // The sounds will be transmitted as an event, not attached to any object.
		   for(%idx = 0; %idx < ClientGroup.getCount(); %idx++)
		      ClientGroup.getObject(%idx).play2D(%profile);
		}

.. cpp:function:: bool GameConnection::play3D(SFXProfile profile, TransformF location)

	Used on the server to play a 3D sound that is not attached to any object.

	:param profile: The SFXProfile that defines the sound to play.
	:param location: The position and orientation of the 3D sound given in the form of "x y z ax ay az aa".

	Example::

		function ServerPlay3D(%profile,%transform)
		{
		   // Play the given sound profile at the given position on every client
		   // The sound will be transmitted as an event, not attached to any object.
		   for(%idx = 0; %idx < ClientGroup.getCount(); %idx++)
		      ClientGroup.getObject(%idx).play3D(%profile,%transform);
		}

.. cpp:function:: bool GameConnection::playDemo(string demoFileName)

	On the client, play back a previously recorded game session. It is often useful to play back a game session. This could be for producing a demo of the game that will be shown at a later time, or for debugging a game. By recording the entire network stream it is possible to later play game the game exactly as it unfolded during the actual play session. This is because all user control and server results pass through the connection.

	:return: True if the playback was successful. False if there was an issue, such as not being able to open the demo file for playback.

.. cpp:function:: void GameConnection::resetGhosting()

	On the server, resets the connection to indicate that ghosting has been disabled. Typically when a mission has ended on the server, all connected clients are informed of this change and their connections are reset back to a starting state. This method resets a connection on the server to indicate that ghosts are no longer being transmitted. On the client end, all ghost information will be deleted.

	Example::

		// Inform the clients
		for (%clientIndex = 0; %clientIndex < ClientGroup.getCount(); %clientIndex++)
		   {
		      // clear ghosts and paths from all clients
		      %cl = ClientGroup.getObject(%clientIndex);
		      %cl.endMission();
		      %cl.resetGhosting();
		      %cl.clearPaths();
		   }

.. cpp:function:: void GameConnection::setBlackOut(bool doFade, int timeMS)

	On the server, sets the client's 3D display to fade to black.

	:param doFade: Set to true to fade to black, and false to fade from black.
	:param timeMS: Time it takes to perform the fade as measured in ms.

.. cpp:function:: bool GameConnection::setCameraObject(GameBase camera)

	On the server, set the connection's camera object used when not viewing through the control object.

.. cpp:function:: void GameConnection::setConnectArgs(const char * args)

	On the client, pass along a variable set of parameters to the server. Once the connection is established with the server, the server calls its onConnect() method with the client's passed in parameters as aruments.

.. cpp:function:: void GameConnection::setControlCameraFov(float newFOV)

	On the server, sets the control object's camera's field of view.

	:param newFOV: New field of view (in degrees) to force the control object's camera to use. This value is clamped to be within the range of 1 to 179 degrees.

.. cpp:function:: bool GameConnection::setControlObject(GameBase ctrlObj)

	On the server, sets the object that the client will control. By default the control object is an instance of the Player class, but can also be an instance of Camera (when editing the mission, for example), or any other ShapeBase derived class as appropriate for the game.

	:param ctrlObj: The GameBase object on the server to control.

.. cpp:function:: void GameConnection::setControlSchemeParameters(bool absoluteRotation, bool addYawToAbsRot, bool addPitchToAbsRot)

	Set the control scheme that may be used by a connection's control object.

	:param absoluteRotation: Use absolute rotation values from client, likely through ExtendedMove.
	:param addYawToAbsRot: Add relative yaw control to the absolute rotation calculation. Only useful when absoluteRotation is true.

.. cpp:function:: void GameConnection::setFirstPerson(bool firstPerson)

	On the server, sets this connection into or out of first person mode.

	:param firstPerson: Set to true to put the connection into first person mode.

.. cpp:function:: void GameConnection::setJoinPassword(string password)

	On the client, set the password that will be passed to the server. On the server, this password is compared with what is stored in pref::Server::Password is empty then the client's sent password is ignored. Otherwise, if the passed in client password and the server password do not match, the CHR_PASSWORD error string is sent back to the client and the connection is immediately terminated. This password checking is performed quite early on in the connection request process so as to minimize the impact of multiple failed attempts -- also known as hacking.

.. cpp:function:: void GameConnection::setLagIcon(bool state)

	Called on the client to display the lag icon. When the connection with the server is lagging, this callback is called to allow the game GUI to display some indicator to the player.

	:param state: Set to true if the lag icon should be displayed.

.. cpp:function:: void GameConnection::setMissionCRC(int CRC)

	On the server, transmits the mission file's CRC value to the client. Typically, during the standard mission start phase 1, the mission file's CRC value on the server is send to the client. This allows the client to determine if the mission has changed since the last time it downloaded this mission and act appropriately, such as rebuilt cached lightmaps.

	:param CRC: The mission file's CRC value on the server.

	Example::

		function serverCmdMissionStartPhase1Ack(%client, %seq)
		{
		   // Make sure to ignore calls from a previous mission loadif (%seq != $missionSequence || !$MissionRunning)
		      return;
		   if (%client.currentPhase != 0)
		      return;
		   %client.currentPhase = 1;
		
		   // Start with the CRC
		   %client.setMissionCRC( $missionCRC );
		
		   // Send over the datablocks...
		   // OnDataBlocksDone will get called when have confirmation
		   // that theyve all been received.
		   %client.transmitDataBlocks($missionSequence);
		}

.. cpp:function:: void GameConnection::startRecording(string fileName)

	On the client, starts recording the network connection's traffic to a demo file. It is often useful to play back a game session. This could be for producing a demo of the game that will be shown at a later time, or for debugging a game. By recording the entire network stream it is possible to later play game the game exactly as it unfolded during the actual play session. This is because all user control and server results pass through the connection.

	:param fileName: The file name to use for the demo recording.

.. cpp:function:: void GameConnection::stopRecording()

	On the client, stops the recording of a connection's network traffic to a file.

.. cpp:function:: void GameConnection::transmitDataBlocks(int sequence)

	Sent by the server during phase 1 of the mission download to send the datablocks to the client. SimDataBlocks, also known as just datablocks, need to be transmitted to the client prior to the client entering the game world. These represent the static data that most objects in the world reference. This is typically done during the standard mission start phase 1 when following Torque's example mission startup sequence. When the datablocks have all been transmitted, onDataBlocksDone() is called to move the mission start process to the next phase.

	:param sequence: The sequence is common between the server and client and ensures that the client is acting on the most recent mission start process. If an errant network packet (one that was lost but has now been found) is received by the client with an incorrect sequence, it is just ignored. This sequence number is updated on the server every time a mission is loaded.

	Example::

		function serverCmdMissionStartPhase1Ack(%client, %seq)
		{
		   // Make sure to ignore calls from a previous mission load
		   if (%seq != $missionSequence || !$MissionRunning)
		      return;
		   if (%client.currentPhase != 0)
		      return;
		   %client.currentPhase = 1;
		
		   // Start with the CRC
		   %client.setMissionCRC( $missionCRC );
		
		   // Send over the datablocks...
		   // OnDataBlocksDone will get called when have confirmation
		   // that theyve all been received.
		   %client.transmitDataBlocks($missionSequence);
		}
