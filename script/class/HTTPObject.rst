HTTPObject
==========

Allows communications between the game and a server using HTTP.

Inherit:
	:doc:`TCPObject`

Description
-----------

HTTPObject is derrived from TCPObject and makes use of the same callbacks for dealing with connections and received data. However, the way in which you use HTTPObject to connect with a server is different than TCPObject. Rather than opening a connection, sending data, waiting to receive data, and then closing the connection, you issue a get() or post() and handle the response. The connection is automatically created and destroyed for you.

Example::

	// In this example well retrieve the weather in Las Vegas using
	// Googles API.  The response is in XML which could be processed
	// and used by the game using SimXMLDocument, but well just output
	// the results to the console in this example.

	// Define callbacks for our specific HTTPObject using our instances
	// name (WeatherFeed) as the namespace.

	// Handle an issue with resolving the servers name
	function WeatherFeed::onDNSFailed(%this)
	{
	   // Store this state
	   %this.lastState = "DNSFailed";
	
	   // Handle DNS failure
	}
	
	function WeatherFeed::onConnectFailed(%this)
	{
	   // Store this state
	   %this.lastState = "ConnectFailed";
	
	   // Handle connection failure
	}
	
	function WeatherFeed::onDNSResolved(%this)
	{
	   // Store this state
	   %this.lastState = "DNSResolved";
	
	}
	
	function WeatherFeed::onConnected(%this)
	{
	   // Store this state
	   %this.lastState = "Connected";
	
	   // Clear our buffer
	   %this.buffer = "";
	}
	
	function WeatherFeed::onDisconnect(%this)
	{
	   // Store this state
	   %this.lastState = "Disconnected";
	
	   // Output the buffer to the consoleecho("Google Weather Results:");
	   echo(%this.buffer);
	}
	
	// Handle a line from the server
	function WeatherFeed::onLine(%this, %line)
	{
	   // Store this line in out buffer
	   %this.buffer = %this.buffer @ %line;
	}
	
	// Create the HTTPObject
	%feed = newHTTPObject(WeatherFeed);
	
	// Define a dynamic field to store the last connection state
	%feed.lastState = "None";
	
	// Send the GET command
	%feed.get("www.google.com:80", "/ig/api", "weather=Las-Vegas,US");


Methods
-------

.. cpp:function:: void HTTPObject::get(string Address, string requirstURI, string query)

	Send a GET command to a server to send or retrieve data.

	:param Address: HTTP web address to send this get call to. Be sure to include the port at the end (IE: "www.garagegames.com:80").
	:param requirstURI: Specific location on the server to access (IE: "index.php".)
	:param query: Optional. Actual data to transmit to the server. Can be anything required providing it sticks with limitations of the HTTP protocol. If you were building the URL manually, this is the text that follows the question mark. For example: http://www.google.com/ig/api?weather=Las-Vegas,US

	Example::

		// Create an HTTP object for communications
		%httpObj = newHTTPObject();
		
		// Specify a URL to transmit to
		%url = "www.garagegames.com:80";
		
		// Specify a URI to communicate with
		%URI = "/index.php";
		
		// Specify a query to send.
		%query = "";
		
		// Send the GET command to the server
		%httpObj.get(%url,%URI,%query);

.. cpp:function:: void HTTPObject::post(string Address, string requirstURI, string query, string post)

	Send POST command to a server to send or retrieve data.

	:param Address: HTTP web address to send this get call to. Be sure to include the port at the end (IE: "www.garagegames.com:80").
	:param requirstURI: Specific location on the server to access (IE: "index.php".)
	:param query: Actual data to transmit to the server. Can be anything required providing it sticks with limitations of the HTTP protocol.
	:param post: Submission data to be processed.

	Example::

		// Create an HTTP object for communications
		%httpObj = newHTTPObject();
		
		// Specify a URL to transmit to
		%url = "www.garagegames.com:80";
		
		// Specify a URI to communicate with
		%URI = "/index.php";
		
		// Specify a query to send.
		%query = "";
		
		// Specify the submission data.
		%post = "";
		
		// Send the POST command to the server
		%httpObj.POST(%url,%URI,%query,%post);
