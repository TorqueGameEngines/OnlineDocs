FileObject
==========

This class is responsible opening, reading, creating, and saving file contents.

Inherit:
	:doc:`SimObject`

Description
-----------

FileObject acts as the interface with OS level files. You create a new FileObject and pass into it a file's path and name. The FileObject class supports three distinct operations for working with files:

Before you may work with a file you need to use one of the three above methods on the FileObject.

Example::

	// Create a file object for writing
	%fileWrite = newFileObject();
	
	// Open a file to write to, if it does not exist it will be created
	%result = %fileWrite.OpenForWrite("./test.txt");
	
	if ( %result )
	{
	   // Write a line to the text files
	   %fileWrite.writeLine("READ. READ CODE. CODE");
	}
	
	// Close the file when finished
	%fileWrite.close();
	
	// Cleanup the file object
	%fileWrite.delete();
	
	
	// Create a file object for reading
	%fileRead = newFileObject();
	
	// Open a text file, if it exists
	%result = %fileRead.OpenForRead("./test.txt");
	
	if ( %result )
	{
	   // Read in the first line
	   %line = %fileRead.readline();
	
	   // Print the line we just readecho(%line);
	}
	
	// Close the file when finished
	%fileRead.close();
	
	// Cleanup the file object
	%fileRead.delete();


Methods
-------


.. cpp:function:: void FileObject::close()

	Close the file. It is EXTREMELY important that you call this function when you are finished reading or writing to a file. Failing to do so is not only a bad programming practice, but could result in bad data or corrupt files. Remember: Open, Read/Write, Close, Delete...in that order!

	Example::

		// Create a file object for reading
		%fileRead = newFileObject();
		
		// Open a text file, if it exists
		%fileRead.OpenForRead("./test.txt");
		
		// Peek the first line
		%line = %fileRead.peekLine();
		
		// Print the line we just peekedecho(%line);
		// If we peek again...
		%line = %fileRead.peekLine();
		
		// We will get the same output as the first time
		// since the stream did not move forwardecho(%line);
		
		// Close the file when finished
		%fileWrite.close();
		
		// Cleanup the file object
		%fileWrite.delete();

.. cpp:function:: bool FileObject::isEOF()

	Determines if the parser for this FileObject has reached the end of the file.

	:return: True if the parser has reached the end of the file, false otherwise 

	Example::

		// Create a file object for reading
		%fileRead = newFileObject();
		
		// Open a text file, if it exists
		%fileRead.OpenForRead("./test.txt");
		
		// Keep reading until we reach the end of the file
		while(!%fileRead.isEOF())
		{
		   %line = %fileRead.readline();
		   echo(%line);
		}
		
		// Made it to the endecho("Finished reading file");

.. cpp:function:: bool FileObject::openForAppend(string filename)

	Open a specified file for writing, adding data to the end of the file. There is no limit as to what kind of file you can write. Any format and data is allowable, not just text. Unlike openForWrite() , which will erase an existing file if it is opened, openForAppend() preserves data in an existing file and adds to it.

	:param filename: Path, name, and extension of file to append to

	:return: True if file was successfully opened, false otherwise 

	Example::

		// Create a file object for writing
		%fileWrite = newFileObject();
		
		// Open a file to write to, if it does not exist it will be created
		// If it does exist, whatever we write will be added to the end
		%result = %fileWrite.OpenForAppend("./test.txt");

.. cpp:function:: bool FileObject::openForRead(string filename)

	Open a specified file for reading. There is no limit as to what kind of file you can read. Any format and data contained within is accessible, not just text

	:param filename: Path, name, and extension of file to be read

	:return: True if file was successfully opened, false otherwise 

	Example::

		// Create a file object for reading
		%fileRead = newFileObject();
		
		// Open a text file, if it exists
		%result = %fileRead.OpenForRead("./test.txt");

.. cpp:function:: bool FileObject::openForWrite(string filename)

	Open a specified file for writing. There is no limit as to what kind of file you can write. Any format and data is allowable, not just text

	:param filename: Path, name, and extension of file to write to

	:return: True if file was successfully opened, false otherwise 

	Example::

		// Create a file object for writing
		%fileWrite = newFileObject();
		
		// Open a file to write to, if it does not exist it will be created
		%result = %fileWrite.OpenForWrite("./test.txt");

.. cpp:function:: string FileObject::peekLine()

	Read a line from the file without moving the stream position. Emphasis on *line*, as in you cannot parse individual characters or chunks of data. There is no limitation as to what kind of data you can read. Unlike readLine, the parser does not move forward after reading.

	:param filename: Path, name, and extension of file to be read

	:return: String containing the line of data that was just peeked 

	Example::

		// Create a file object for reading
		%fileRead = newFileObject();
		
		// Open a text file, if it exists
		%fileRead.OpenForRead("./test.txt");
		
		// Peek the first line
		%line = %fileRead.peekLine();
		
		// Print the line we just peekedecho(%line);
		// If we peek again...
		%line = %fileRead.peekLine();
		
		// We will get the same output as the first time
		// since the stream did not move forward
		echo(%line);

.. cpp:function:: string FileObject::readLine()

	Read a line from file. Emphasis on *line*, as in you cannot parse individual characters or chunks of data. There is no limitation as to what kind of data you can read.

	:return: String containing the line of data that was just read 

	Example::

		// Create a file object for reading
		%fileRead = newFileObject();
		
		// Open a text file, if it exists
		%fileRead.OpenForRead("./test.txt");
		
		// Read in the first line
		%line = %fileRead.readline();
		
		// Print the line we just read
		echo(%line);

.. cpp:function:: void FileObject::writeLine(string text)

	Write a line to the file, if it was opened for writing. There is no limit as to what kind of text you can write. Any format and data is allowable, not just text. Be careful of what you write, as whitespace, current values, and literals will be preserved.

	:param text: The data we are writing out to file.

	:return: True if file was successfully opened, false otherwise 

	Example::

		// Create a file object for writing
		%fileWrite = newFileObject();
		
		// Open a file to write to, if it does not exist it will be created
		%fileWrite.OpenForWrite("./test.txt");
		
		// Write a line to the text files
		%fileWrite.writeLine("READ. READ CODE. CODE");

.. cpp:function:: void FileObject::writeObject(SimObject object)

	Write an object to a text file. Unlike a simple writeLine using specified strings, this function writes an entire object to file, preserving its type, name, and properties. This is similar to the save() functionality of the SimObject class, but with a bit more control.

	:param object: The SimObject being written to file, properties, name, and all.

	Example::

		// Lets assume this SpawnSphere was created and currently
		// exists in the running level
		newSpawnSphere(TestSphere)
		{
		   spawnClass = "Player";
		   spawnDatablock = "DefaultPlayerData";
		   autoSpawn = "1";
		   radius = "5";
		   sphereWeight = "1";
		   indoorWeight = "1";
		   outdoorWeight = "1";
		   dataBlock = "SpawnSphereMarker";
		   position = "-42.222 1.4845 4.80334";
		   rotation = "0 0 -1 108";
		   scale = "1 1 1";
		   canSaveDynamicFields = "1";
		};
		
		// Create a file object for writing
		%fileWrite = newFileObject();
		
		// Open a file to write to, if it does not exist it will be created
		%fileWrite.OpenForWrite("./spawnSphers.txt");
		
		// Write out the TestSphere
		%fileWrite.writeObject(TestSphere);
		
		// Close the text file
		%fileWrite.close();
		
		// Cleanup
		%fileWrite.delete();

.. cpp:function:: void FileObject::writeObject(SimObject object, string prepend)

	Write an object to a text file, with some data added first. Unlike a simple writeLine using specified strings, this function writes an entire object to file, preserving its type, name, and properties. This is similar to the save() functionality of the SimObject class, but with a bit more control.

	:param object: The SimObject being written to file, properties, name, and all.
	:param prepend: Data or text that is written out before the SimObject.

	Example::

		// Lets assume this SpawnSphere was created and currently
		// exists in the running level
		newSpawnSphere(TestSphere)
		{
		   spawnClass = "Player";
		   spawnDatablock = "DefaultPlayerData";
		   autoSpawn = "1";
		   radius = "5";
		   sphereWeight = "1";
		   indoorWeight = "1";
		   outdoorWeight = "1";
		   dataBlock = "SpawnSphereMarker";
		   position = "-42.222 1.4845 4.80334";
		   rotation = "0 0 -1 108";
		   scale = "1 1 1";
		   canSaveDynamicFields = "1";
		};
		
		// Create a file object for writing
		%fileWrite = newFileObject();
		
		// Open a file to write to, if it does not exist it will be created
		%fileWrite.OpenForWrite("./spawnSphers.txt");
		
		// Write out the TestSphere, with a prefix
		%fileWrite.writeObject(TestSphere, "$mySphere = ");
		
		// Close the text file
		%fileWrite.close();
		
		// Cleanup
		%fileWrite.delete();
