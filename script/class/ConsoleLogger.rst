ConsoleLogger
=============

Inherit:
	:doc:`SimObject`

Description
-----------

A class designed to be used as a console consumer and log the data it receives to a file.

Methods
-------

.. cpp:function:: bool ConsoleLogger::attach()

	Attaches the logger to the console and begins writing to file.

	Example::

		// Create the logger
		// Will automatically start writing to testLogging.txt with normal priority
		newConsoleLogger(logger, "testLogging.txt", false);
		
		// Send something to the console, with the logger consumes and writes file
		echo("This is logged to the file");
		
		// Stop logging, but do not delete the logger
		logger.detach();
		
		echo("This is not logged to the file");
		
		// Attach the logger to the console again
		logger.attach();
		
		// Logging has resumedecho("Logging has resumed");

.. cpp:function:: bool ConsoleLogger::detach()

	Detaches the logger from the console and stops writing to file.

	Example::

		// Create the logger
		// Will automatically start writing to testLogging.txt with normal priority
		newConsoleLogger(logger, "testLogging.txt", false);
		
		// Send something to the console, with the logger consumes and writes to file
		echo("This is logged to the file");
		
		// Stop logging, but do not delete the logger
		logger.detach();
		
		echo("This is not logged to the file");
		
		// Attach the logger to the console again
		logger.attach();
		
		// Logging has resumedecho("Logging has resumed");

Fields
------

.. cpp:member:: LogLevel ConsoleLogger::level

	Determines the priority level and attention the logged entry gets when recorded.
