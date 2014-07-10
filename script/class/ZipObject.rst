ZipObject
=========

Provides access to a zip file.

Inherit:
	:doc:`SimObject`

Description
-----------

A ZipObject add, delete and extract files that are within a zip archive. You may also read and write directly to the files within the archive by obtaining a StreamObject for the file.

Example::

	// Open a zip archive, creating it if it doesn't exist
	%archive = newZipObject();
	%archive.openArchive("testArchive.zip", Write);
	
	// Add a file to the archive with the given name
	%archive.addFile("./water.png", "water.png");
	
	// Close the archive to save the changes
	%archive.closeArchive();


Methods
-------

.. cpp:function:: bool ZipObject::addFile(string filename, string pathInZip, bool replace)

	Add a file to the zip archive.

	:param filename: The path and name of the file to add to the zip archive.
	:param pathInZip: The path and name to be given to the file within the zip archive.
	:param replace: If a file already exists within the zip archive at the same location as this new file, this parameter indicates if it should be replaced. By default, it will be replaced.

	:return: True if the file was successfully added to the zip archive. 

.. cpp:function:: void ZipObject::closeArchive()

	Close an already opened zip archive.

.. cpp:function:: void ZipObject::closeFile(SimObject stream)

	Close a previously opened file within the zip archive.

	:param stream: The StreamObject of a previously opened file within the zip archive.

.. cpp:function:: bool ZipObject::deleteFile(string pathInZip)

	Deleted the given file from the zip archive.

	:param pathInZip: The path and name of the file to be deleted from the zip archive.

	:return: True of the file was successfully deleted. 

.. cpp:function:: bool ZipObject::extractFile(string pathInZip, string filename)

	Extact a file from the zip archive and save it to the requested location.

	:param pathInZip: The path and name of the file to be extracted within the zip archive.
	:param filename: The path and name to give the extracted file.

	:return: True if the file was successfully extracted. 

.. cpp:function:: String ZipObject::getFileEntry(int index)

	Get information on the requested file within the zip archive. This methods provides five different pieces of information for the requested file: 
	
	* filename - The path and name of the file within the zip archive
	* uncompressed size
	* compressed size
	* compression method
	* CRC32

	Use getFileEntryCount() to obtain the total number of files within the archive.

	:param index: The index of the file within the zip archive. Use getFileEntryCount() to determine the number of files.

	:return: A tab delimited list of information on the requested file, or an empty string if the file could not be found. 

.. cpp:function:: int ZipObject::getFileEntryCount()

	Get the number of files within the zip archive. Use getFileEntry() to retrive information on each file within the archive.

	:return: The number of files within the zip archive. 

.. cpp:function:: bool ZipObject::openArchive(string filename, string accessMode)

	Open a zip archive for manipulation. Once a zip archive is opened use the various ZipObject methods for working with the files within the archive. Be sure to close the archive when you are done with it.

	:param filename: The path and file name of the zip archive to open.
	:param accessMode: One of read, write or readwrite

	:return: True is the archive was successfully opened. 

.. cpp:function:: SimObject  ZipObject::openFileForRead(string filename)

	Open a file within the zip archive for reading. Be sure to close the file when you are done with it.

	:param filename: The path and name of the file to open within the zip archive.

	:return:  is returned for working with the file. 

.. cpp:function:: SimObject  ZipObject::openFileForWrite(string filename)

	Open a file within the zip archive for writing to. Be sure to close the file when you are done with it.

	:param filename: The path and name of the file to open within the zip archive.

	:return:  is returned for working with the file. 
