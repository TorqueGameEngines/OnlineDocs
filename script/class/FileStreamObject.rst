FileStreamObject
================

A wrapper around StreamObject for parsing text and data from files.

Inherit:
	:doc:`StreamObject`

Description
-----------

FileStreamObject inherits from StreamObject and provides some unique methods for working with strings. If you're looking for general file handling, you may want to use FileObject.

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


Methods
-------

.. cpp:function:: void FileStreamObject::close()

	Close the file. You can no longer read or write to it unless you open it again.

	Example::

		// Create a file stream object for reading
		%fsObject = newFileStreamObject();
		
		// Open a file for reading
		%fsObject.open("./test.txt", "read");
		
		// Always remember to close a file stream when finished
		%fsObject.close();

.. cpp:function:: bool FileStreamObject::open(string filename, string openMode)

	Open a file for reading, writing, reading and writing, or appending. Using "Read" for the open mode allows you to parse the contents of file, but not making modifications. "Write" will create a new file if it does not exist, or erase the contents of an existing file when opened. Write also allows you to modify the contents of the file. "ReadWrite" will provide the ability to parse data (read it in) and manipulate data (write it out) interchangeably. Keep in mind the stream can move during each operation. Finally, "WriteAppend" will open a file if it exists, but will not clear the contents. You can write new data starting at the end of the files existing contents.

	:param filename: Name of file to open
	:param openMode: One of "Read", "Write", "ReadWrite" or "WriteAppend"

	:return: True if the file was successfully opened, false if something went wrong

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
