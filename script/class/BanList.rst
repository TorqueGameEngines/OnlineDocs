BanList
=======

Used for kicking and banning players from a server.

Description
-----------

There is only a single instance of BanList. It is very important to note that you do not ever create this object in script like you would other game play objects. You simply reference it via namespace.

For this to be used effectively, make sure you are hooking up other functions to BanList. For example, functions like GameConnection::onConnectRequestRejected( this, msg ) and function GameConnection::onConnectRequest are excellent places to make use of the BanList. Other systems can be used in conjunction for strict control over a server

Methods
-------

.. cpp:function:: static void BanList::add(int uniqueId, string transportAddress, int banLength)

	Ban a user for banLength seconds.

	:param uniqueId: Unique ID of the player.
	:param transportAddress: Address from which the player connected.
	:param banLength: Time period over which to ban the player.

	Example::

		// Kick someone off the server
		// %client - This is the connection to the person we are kicking
		function kick(%client)
		{
		      // Let the server know what happened
		      messageAll( MsgAdminForce, \c2The Admin has kicked %1., %client.playerName);
		
		      // If it is not an AI Player, execute the ban.
		      if (!%client.isAIControlled())
		         BanList::add(%client.guid, %client.getAddress(), $pref::Server::KickBanTime);
		
		      // Let the player know they messed up
		      %client.delete("You have been kicked from this server");
		}

.. cpp:function:: static void BanList::addAbsolute(int uniqueId, string transportAddress, int banTime)

	Ban a user until a given time.

	:param uniqueId: Unique ID of the player.
	:param transportAddress: Address from which the player connected.
	:param banTime: Time at which they will be allowed back in.

	Example::

		// Kick someone off the server
		// %client - This is the connection to the person we are kicking
		function kick(%client)
		{
		      // Let the server know what happened
		      messageAll( MsgAdminForce, \c2The Admin has kicked %1., %client.playerName);
		
		      // If it is not an AI Player, execute the ban.
		      if (!%client.isAIControlled())
		         BanList::addAbsolute(%client.guid, %client.getAddress(), $pref::Server::KickBanTime);
		
		      // Let the player know they messed up
		      %client.delete("You have been kicked from this server");
		}

.. cpp:function:: static void BanList::export(string filename)

	Dump the banlist to a file.

	:param filename: Path of the file to write the list to.

	Example::

		BanList::Export("./server/banlist.cs");

.. cpp:function:: static bool BanList::isBanned(int uniqueId, string transportAddress)

	Is someone banned?

	:param uniqueId: Unique ID of the player.
	:param transportAddress: Address from which the player connected.

	Example::

		// This script function is called before a client connection
		// is accepted.  Returning  will accept the connection,
		// anything else will be sent back as an error to the client.
		// All the connect args are passed also to onConnectRequest
		function GameConnection::onConnectRequest( %client, %netAddress, %name )
		{
		     // Find out who is trying to connect
		     echo("Connect request from: " @ %netAddress);
		
		     // Are they allowed in?
		     if(BanList::isBanned(%client.guid, %netAddress))
		        return"CR_YOUAREBANNED";
		
		     // Is there room for an unbanned player?
		     if($Server::PlayerCount >= $pref::Server::MaxPlayers)
		        return"CR_SERVERFULL";
		     return ;
		}

.. cpp:function:: static void BanList::removeBan(int uniqueId, string transportAddress)

	Unban someone.

	:param uniqueId: Unique ID of the player.
	:param transportAddress: Address from which the player connected.

	Example::

		BanList::removeBan(%userID, %ipAddress);
