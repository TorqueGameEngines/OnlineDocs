TCPObject
=========

Allows communications between the game and a server using TCP/IP protocols.

Inherit:
	:doc:`SimObject`

Description
-----------

To use TCPObject you set up a connection to a server, send data to the server, and handle each line of the server's response using a callback. Once you are done communicating with the server, you disconnect.

TCPObject is intended to be used with text based protocols which means you'll need to delineate the server's response with an end-of-line character. i.e. the newline character \n. You may optionally include the carriage return character \r prior to the newline and TCPObject will strip it out before sending the line to the callback. If a newline character is not included in the server's output, the received data will not be processed until you disconnect from the server (which flushes the internal buffer).

TCPObject may also be set up to listen to a specific port, making Torque into a TCP server. When used in this manner, a callback is received when a client connection is made. Following the outside connection, text may be sent and lines are processed in the usual manner.

If you want to work with HTTP you may wish to use HTTPObject instead as it handles all of the HTTP header setup and parsing.

Example::

	// In this example well retrieve the new forum threads RSS
	// feed from garagegames.com.  As were using TCPObject, the
	// raw text response will be received from the server, including
	// the HTTP header.

	// Define callbacks for our specific TCPObject using our instances
	// name (RSSFeed) as the namespace.

	// Handle an issue with resolving the servers name
	function RSSFeed::onDNSFailed(%this)
	{
	   // Store this state
	   %this.lastState = "DNSFailed";
	
	   // Handle DNS failure
	}
	
	function RSSFeed::onConnectFailed(%this)
	{
	   // Store this state
	   %this.lastState = "ConnectFailed";
	
	   // Handle connection failure
	}
	
	function RSSFeed::onDNSResolved(%this)
	{
	   // Store this state
	   %this.lastState = "DNSResolved";
	
	}
	
	function RSSFeed::onConnected(%this)
	{
	   // Store this state
	   %this.lastState = "Connected";
	
	}
	
	function RSSFeed::onDisconnect(%this)
	{
	   // Store this state
	   %this.lastState = "Disconnected";
	
	}
	
	// Handle a line from the server
	function RSSFeed::onLine(%this, %line)
	{
	   // Print the line to the consoleecho( %line );
	}
	
	// Create the TCPObject
	%rss = newTCPObject(RSSFeed);
	
	// Define a dynamic field to store the last connection state
	%rss.lastState = "None";
	
	// Connect to the server
	%rss.connect("www.garagegames.com:80");
	
	// Send the RSS feed request to the server.  Response will be// handled in onLine() callback above
	%rss.send("GET /feeds/rss/threads HTTP/1.1\r\nHost: www.garagegames.com\r\n\r\n");


Methods
-------

.. cpp:function:: void TCPObject::connect(string address)

	Connect to the given address.

	:param address: Server address (including port) to connect to.

	Example::

		// Set the address.
		%address = "www.garagegames.com:80";
		
		// Inform this TCPObject to connect to the specified address.
		%thisTCPObj.connect(%address);

.. cpp:function:: void TCPObject::disconnect()

	Disconnect from whatever this TCPObject is currently connected to, if anything.

	Example::

		// Inform this TCPObject to disconnect from anything it is currently connected to.
		%thisTCPObj.disconnect();

.. cpp:function:: void TCPObject::listen(int port)

	Start listening on the specified port for connections. This method starts a listener which looks for incoming TCP connections to a port. You must overload the onConnectionRequest callback to create a new TCPObject to read, write, or reject the new connection.

	:param port: Port for this TCPObject to start listening for connections on.

	Example::

		// Create a listener on port 8080.
		newTCPObject( TCPListener );
		TCPListener.listen( 8080 );
		
		function TCPListener::onConnectionRequest( %this, %address, %id )
		{
		   // Create a new object to manage the connection.newTCPObject( TCPClient, %id );
		}
		
		function TCPClient::onLine( %this, %line )
		{
		   // Print the line of text from client.echo( %line );
		}

.. cpp:function:: void TCPObject::onConnected()

	Called whenever a connection is established with a server.

.. cpp:function:: void TCPObject::onConnectFailed()

	Called whenever a connection has failed to be established with a server.

.. cpp:function:: void TCPObject::onConnectionRequest(string address, string ID)

	Called whenever a connection request is made. This callback is used when the TCPObject is listening to a port and a client is attempting to connect.

	:param address: Server address connecting from.
	:param ID: Connection ID

.. cpp:function:: void TCPObject::onDisconnect()

	Called whenever the TCPObject disconnects from whatever it is currently connected to.

.. cpp:function:: void TCPObject::onDNSFailed()

	Called whenever the DNS has failed to resolve.

.. cpp:function:: void TCPObject::onDNSResolved()

	Called whenever the DNS has been resolved.

.. cpp:function:: void TCPObject::onLine(string line)

	Called whenever a line of data is sent to this TCPObject . This callback is called when the received data contains a newline \n character, or the connection has been disconnected and the TCPObject's buffer is flushed.

	:param line: Data sent from the server.

.. cpp:function:: void TCPObject::send(string data)

	Transmits the data string to the connected computer. This method is used to send text data to the connected computer regardless if we initiated the connection using connect() , or listening to a port using listen() .

	:param data: The data string to send.

	Example::

		// Set the command data
		%data = "GET " @ $RSSFeed::serverURL @ " HTTP/1.0\r\n";
		%data = %data @ "Host: " @ $RSSFeed::serverName @ "\r\n";
		%data = %data @ "User-Agent: " @ $RSSFeed::userAgent @ "\r\n\r\n"
		// Send the command to the connected server.
		%thisTCPObj.send(%data);
