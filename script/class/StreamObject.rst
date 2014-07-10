StreamObject
============

Base class for working with streams.

Inherit:
	:doc:`SimObject`

Description
-----------

You do not instantiate a StreamObject directly. Instead, it is used as part of a FileStreamObject and ZipObject to support working with uncompressed and compressed files respectively.

Example::

	// You cannot actually declare a StreamObject
	// Instead, use the derived class "FileStreamObject"
	%fsObject = FileStreamObject();


Methods
-------

.. cpp:function:: bool StreamObject::copyFrom(SimObject other)

	Copy from another StreamObject into this StreamObject .

	:param other: The StreamObject to copy from.

	:return: True if the copy was successful. 

.. cpp:function:: int StreamObject::getPosition()

	Gets the position in the stream. The easiest way to visualize this is to think of a cursor in a text file. If you have moved the cursor by five characters, the current position is 5. If you move ahead 10 more characters, the position is now 15. For StreamObject , when you read in the line the position is increased by the number of characters parsed, the null terminator, and a newline.

	:return: Number of bytes which stream has parsed so far, null terminators and newlines are included 

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		// This file contains two lines of text repeated:
		// Hello World
		// Hello World
		%fsObject.open("./test.txt", "read");
		
		// Read in the first line
		%line = %fsObject.readLine();
		
		// Get the position of the stream
		%position = %fsObject.getPosition();
		
		// Print the current position
		// Should be 13, 10 for the words, 1 for the space, 
		// 1 for the null terminator, and 1 for the newline
		echo(%position);
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: string StreamObject::getStatus()

	Gets a printable string form of the stream's status. OK - Stream is active and no file errors IOError - Something went wrong during read or writing the stream EOS - End of Stream reached (mostly for reads) IllegalCall - An unsupported operation used. Always w/ accompanied by AssertWarn Closed - Tried to operate on a closed stream (or detached filter) UnknownError - Catch all for an error of some kind Invalid - Entire stream is invalid

	:return: String containing status constant, one of the following:

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		%fsObject.open("./test.txt", "read");
		
		// Get the status and print it
		%status = %fsObject.getStatus();
		echo(%status);
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: int StreamObject::getStreamSize()

	Gets the size of the stream. The size is dependent on the type of stream being used. If it is a file stream, returned value will be the size of the file. If it is a memory stream, it will be the size of the allocated buffer.

	:return: Size of stream, in bytes 

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		// This file contains the following two lines:
		// HelloWorld
		// HelloWorld
		%fsObject.open("./test.txt", "read");
		
		// Found out how large the file stream is
		// Then print it to the console
		// Should be 22
		%streamSize = %fsObject.getStreamSize();
		echo(%streamSize);
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: bool StreamObject::isEOF()

	Tests if the stream has reached the end of the file. This is an alternative name for isEOS. Both functions are interchangeable. This simply exists for those familiar with some C++ file I/O standards.

	:return: True if the parser has reached the end of the file, false otherwise 

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		%fsObject.open("./test.txt", "read");
		
		// Keep reading until we reach the end of the file
		while(!%fsObject.isEOF())
		{
		   %line = %fsObject.readLine();
		   echo(%line);
		}
		// Made it to the end
		echo("Finished reading file");
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: bool StreamObject::isEOS()

	Tests if the stream has reached the end of the file. This is an alternative name for isEOF. Both functions are interchangeable. This simply exists for those familiar with some C++ file I/O standards.

	:return: True if the parser has reached the end of the file, false otherwise 

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		%fsObject.open("./test.txt", "read");
		
		// Keep reading until we reach the end of the file
		while(!%fsObject.isEOS())
		{
		   %line = %fsObject.readLine();
		   echo(%line);
		}
		// Made it to the end
		echo("Finished reading file");
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: string StreamObject::readLine()

	Read a line from the stream. Emphasis on *line*, as in you cannot parse individual characters or chunks of data. There is no limitation as to what kind of data you can read.

	:return: String containing the line of data that was just read 

	Example::

		// Create a file stream object for reading
		// This file contains the following two lines:
		// HelloWorld
		// HelloWorld
		%fsObject = newFileStreamObject();
		
		%fsObject.open("./test.txt", "read");
		
		// Read in the first line
		%line = %fsObject.readLine();
		
		// Print the line we just read
		echo(%line);
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: String StreamObject::readLongString(int maxLength)

	Read in a string up to the given maximum number of characters.

	:param maxLength: The maximum number of characters to read in.

	:return: The string that was read from the stream. 

.. cpp:function:: String StreamObject::readString()

	Read a string up to a maximum of 256 characters.

	:return: The string that was read from the stream. 

.. cpp:function:: String StreamObject::readSTString(bool caseSensitive)

	Read in a string and place it on the string table.

	:param caseSensitive: If false then case will not be taken into account when attempting to match the read in string with what is already in the string table.

	:return: The string that was read from the stream. 

.. cpp:function:: bool StreamObject::setPosition(int newPosition)

	Gets the position in the stream. The easiest way to visualize this is to think of a cursor in a text file. If you have moved the cursor by five characters, the current position is 5. If you move ahead 10 more characters, the position is now 15. For StreamObject , when you read in the line the position is increased by the number of characters parsed, the null terminator, and a newline. Using setPosition allows you to skip to specific points of the file.

	:return: Number of bytes which stream has parsed so far, null terminators and newlines are included 

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		// This file contains the following two lines:
		// 11111111111
		// Hello World
		%fsObject.open("./test.txt", "read");
		
		// Skip ahead by 12, which will bypass the first line entirely
		%fsObject.setPosition(12);
		
		// Read in the next line
		%line = %fsObject.readLine();
		
		// Print the line just read in, should be "Hello World"
		echo(%line);
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: void StreamObject::writeLine(string line)

	Write a line to the stream, if it was opened for writing. There is no limit as to what kind of data you can write. Any format and data is allowable, not just text. Be careful of what you write, as whitespace, current values, and literals will be preserved.

	:param line: The data we are writing out to file.

	Example::

		// Create a file stream
		%fsObject = newFileStreamObject();
		
		// Open the file for writing
		// If it does not exist, it is created. 
		// If it does exist, the file is cleared
		%fsObject.open("./test.txt", "write");
		
		// Write a line to the file
		%fsObject.writeLine("Hello World");
		
		// Write another line to the file
		%fsObject.writeLine("Documentation Rocks!");
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: void StreamObject::writeLongString(int maxLength, string string)

	Write out a string up to the maximum number of characters.

	:param maxLength: The maximum number of characters that will be written.
	:param string: The string to write out to the stream.

.. cpp:function:: void StreamObject::writeString(string string, int maxLength)

	Write out a string with a default maximum length of 256 characters.

	:param string: The string to write out to the stream
	:param maxLength: The maximum string length to write out with a default of 256 characters. This value should not be larger than 256 as it is written to the stream as a single byte.
