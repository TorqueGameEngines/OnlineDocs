NetConnection
=============

Provides the basis for implementing a multiplayer game protocol.

Inherit:
	:doc:`SimGroup`

Description
-----------

NetConnection combines a low-level notify protocol implemented in ConnectionProtocol with a SimGroup, and implements several distinct subsystems:

Event Manager
	This is responsible for transmitting NetEvents over the wire. It deals with ensuring that the various types of NetEvents are delivered appropriately, and with notifying the event of its delivery status.

Move Manager
	This is responsible for transferring a Move to the server 32 times a second (on the client) and applying it to the control object (on the server).

Ghost Manager
	This is responsible for doing scoping calculations (on the server side) and transmitting most-recent ghost information to the client.

File Transfer
	It is often the case that clients will lack important files when connecting to a server which is running a mod or new map. This subsystem allows the server to transfer such files to the client.

Networked String Table 
	String data can easily soak up network bandwidth, so for efficiency, we implement a networked string table. We can then notify the connection of strings we will reference often, such as player names, and transmit only a tag, instead of the whole string.

Demo Recording 
	A demo in Torque is a log of the network traffic between client and server; when a NetConnection records a demo, it simply logs this data to a file. When it plays a demo back, it replays the logged data.

Connection Database 
	This is used to keep track of all the NetConnections; it can be iterated over (for instance, to send an event to all active connections), or queried by address.

The NetConnection is a SimGroup. On the client side, it contains all the objects which have been ghosted to that client. On the server side, it is empty; it can be used (typically in script) to hold objects related to the connection. For instance, you might place an observation camera in the NetConnnection. In both cases, when the connection is destroyed, so are the contained objects.

The NetConnection also has the concept of local connections. These are used when the client and server reside in the same process. A local connection is typically required to use the standard Torque world building tools. A local connection is also required when building a single player game.

Methods
-------

.. cpp:function:: void NetConnection::checkMaxRate()

	Ensures that all configured packet rates and sizes meet minimum requirements. This method is normally only called when a NetConnection class is first constructed. It need only be manually called if the global variables that set the packet rate or size have changed.

.. cpp:function:: void NetConnection::clearPaths()

	On the server, resets the connection to indicate that motion spline paths have not been transmitted. Typically when a mission has ended on the server, all connected clients are informed of this change and their connections are reset back to a starting state. This method resets a connection on the server to indicate that motion spline paths have not been transmitted.

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

.. cpp:function:: void NetConnection::connect(string remoteAddress)

	Connects to the remote address. Attempts to connect with another NetConnection on the given address. Typically once connected, a game's information is passed along from the server to the client, followed by the player entering the game world. The actual procedure is dependent on the NetConnection subclass that is used. i.e. GameConnection .

	:param remoteAddress: The address to connect to in the form of IP:<address>:<port although the IP: portion is optional. The address portion may be in the form of w.x.y.z or as a host name, in which case a DNS lookup will be performed. You may also substitue the word broadcast for the address to broadcast the connect request over the local subnet.

.. cpp:function:: string NetConnection::connectLocal()

	Connects with the server that is running within the same process as the client.

	:return: An error text message upon failure, or an empty string when successful.

.. cpp:function:: string NetConnection::getAddress()

	Returns the far end network address for the connection. The address will be in one of the following forms: 
	
	* IP:Broadcast:<port> for broadcast type addresses
	* IP:<address>:<port> for IP addresses
	* local when connected locally (server and client running in same process 

.. cpp:function:: int NetConnection::getGhostID(int realID)

	On server or client, convert a real id to the ghost id for this connection. Torque's network ghosting system only exchanges ghost ID's between the server and client. Use this method on the server or client to discover an object's ghost ID based on its real SimObject ID.

	:param realID: The real SimObject ID of the object.

	:return: The ghost ID of the object for this connection, or -1 if it could not be resolved.

.. cpp:function:: int NetConnection::getGhostsActive()

	Provides the number of active ghosts on the connection.

	:return: The number of active ghosts. 

.. cpp:function:: int NetConnection::getPacketLoss()

	Returns the percentage of packets lost per tick.

.. cpp:function:: int NetConnection::getPing()

	Returns the average round trip time (in ms) for the connection. The round trip time is recalculated every time a notify packet is received. Notify packets are used to information the connection that the far end successfully received the sent packet.

.. cpp:function:: int NetConnection::resolveGhostID(int ghostID)

	On the client, convert a ghost ID from this connection to a real SimObject ID. Torque's network ghosting system only exchanges ghost ID's between the server and client. Use this method on the client to discover an object's local SimObject ID when you only have a ghost ID.

	:param ghostID: The ghost ID of the object as sent by the server.

	:return:  ID of the object, or 0 if it could not be resolved.

	Example::

		%object = ServerConnection.resolveGhostID( %ghostId );

.. cpp:function:: int NetConnection::resolveObjectFromGhostIndex(int ghostID)

	On the server, convert a ghost ID from this connection to a real SimObject ID. Torque's network ghosting system only exchanges ghost ID's between the server and client. Use this method on the server to discover an object's local SimObject ID when you only have a ghost ID.

	:param ghostID: The ghost ID of the object as sent by the server.

	:return:  ID of the object, or 0 if it could not be resolved.

	Example::

		%object = %client.resolveObjectFromGhostIndex( %ghostId );

.. cpp:function:: void NetConnection::setSimulatedNetParams(float packetLoss, int delay)

	Simulate network issues on the connection for testing.

	:param packetLoss: The fraction of packets that will be lost. Ranges from 0.0 (no loss) to 1.0 (complete loss)
	:param delay: Delays packets being transmitted by simulating a particular ping. This is an absolute integer, measured in ms.

.. cpp:function:: void NetConnection::transmitPaths()

	Sent by the server during phase 2 of the mission download to update motion spline paths. The server transmits all spline motion paths that are within the mission ( Path ) separate from other objects. This is due to the potentially large number of nodes within each path, which may saturate a packet sent to the client. By managing this step separately, Torque has finer control over how packets are organised vs. doing it during the ghosting stage. Internally a PathManager is used to track all paths defined within a mission on the server, and each one is transmitted using a PathManagerEvent. The client side collects these events and builds the given paths within its own PathManager. This is typically done during the standard mission start phase 2 when following Torque's example mission startup sequence. When a mission is ended, all paths need to be cleared from their respective path managers.

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
		
		   // Update mission paths (SimPath), this needs to get there before the objects.
		   %client.transmitPaths();
		
		   // Start ghosting objects to the client
		   %client.activateGhosting();
		}
