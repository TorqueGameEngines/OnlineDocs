File I/O
========

Functions allowing you to search for files, read them, write them, and access their properties.

Classes
-------

.. toctree::
	:maxdepth: 1

	class/FileDialog
	class/FileObject
	class/FileStreamObject
	class/OpenFileDialog
	class/OpenFolderDialog
	class/SaveFileDialog
	class/SimXMLDocument
	class/StreamObject
	class/ZipObject

Functions
---------

.. cpp:function:: bool createPath(string path)

	Create the given directory or the path leading to the given filename. If path ends in a trailing slash, then all components in the given path will be created as directories (if not already in place). If path , does not end in a trailing slash, then the last component of the path is taken to be a file name and only the directory components of the path will be created.

	:param path: The path to create.

.. cpp:function:: string expandFilename(string filename)

	Grabs the full path of a specified file.

	:param filename: Name of the local file to locate

	:return: String containing the full filepath on disk 

.. cpp:function:: string expandOldFilename(string filename)

	Retrofits a filepath that uses old Torque style.

	:return: String containing filepath with new formatting 

.. cpp:function:: String fileBase(string fileName)

	Get the base of a file name (removes extension).

	:param fileName: Name and path of file to check

	:return: String containing the file name, minus extension 

.. cpp:function:: String fileCreatedTime(string fileName)

	Returns a platform specific formatted string with the creation time for the file.

	:param fileName: Name and path of file to check

	:return: Formatted string (OS specific) containing created time, "9/3/2010 12:33:47 PM" for example 

.. cpp:function:: bool fileDelete(string path)

	Delete a file from the hard drive.

	:param path: Name and path of the file to delete

	:return: True if file was successfully deleted 

.. cpp:function:: String fileExt(string fileName)

	Get the extension of a file.

	:param fileName: Name and path of file

	:return: String containing the extension, such as ".exe" or ".cs" 

.. cpp:function:: String fileModifiedTime(string fileName)

	Returns a platform specific formatted string with the last modified time for the file.

	:param fileName: Name and path of file to check

	:return: Formatted string (OS specific) containing modified time, "9/3/2010 12:33:47 PM" for example 

.. cpp:function:: String fileName(string fileName)

	Get the file name of a file (removes extension and path).

	:param fileName: Name and path of file to check

	:return: String containing the file name, minus extension and path 

.. cpp:function:: String filePath(string fileName)

	Get the path of a file (removes name and extension).

	:param fileName: Name and path of file to check

	:return: String containing the path, minus name and extension 

.. cpp:function:: int fileSize(string fileName)

	Determines the size of a file on disk.

	:param fileName: Name and path of the file to check

	:return: Returns filesize in KB, or -1 if no file 

.. cpp:function:: String getCurrentDirectory()

	Return the current working directory.

	:return: The absolute path of the current working directory.

.. cpp:function:: String getDirectoryList(string path, int depth)

	Gathers a list of directories starting at the given path.

	:param path: String containing the path of the directory
	:param depth: Depth of search, as in how many subdirectories to parse through

	:return: Tab delimited string containing list of directories found during search, "" if no files were found 

.. cpp:function:: String getExecutableName()

	Gets the name of the game's executable.

	:return: String containing this game's executable name 

.. cpp:function:: int getFileCRC(string fileName)

	Provides the CRC checksum of the given file.

	:param fileName: The path to the file.

	:return: The calculated CRC checksum of the file, or -1 if the file could not be found. 

.. cpp:function:: String getMainDotCsDir()

	Get the absolute path to the directory that contains the main.cs script from which the engine was started. This directory will usually contain all the game assets and, in a user-side game installation, will usually be read-only.

	:return: The path to the main game assets. 

.. cpp:function:: String getWorkingDirectory()

	Reports the current directory.

	:return: String containing full file path of working directory 

.. cpp:function:: bool IsDirectory(string directory)

	Determines if a specified directory exists or not.

	:param directory: String containing path in the form of "foo/bar"

	:return: Returns true if the directory was found. 

.. cpp:function:: bool isFile(string fileName)

	Determines if the specified file exists or not.

	:param fileName: The path to the file.

	:return: Returns true if the file was found. 

.. cpp:function:: bool isWriteableFileName(string fileName)

	Determines if a file name can be written to using File I/O.

	:param fileName: Name and path of file to check

	:return: Returns true if the file can be written to. 

.. cpp:function:: String makeFullPath(string path, string cwd)

	Converts a relative file path to a full path. For example, "./console.log" becomes "C:/Torque/t3d/examples/FPS Example/game/console.log"

	:param path: Name of file or path to check
	:param cwd: Optional current working directory from which to build the full path.

	:return: String containing non-relative directory of path 

.. cpp:function:: String makeRelativePath(string path, string to)

	Turns a full or local path to a relative one. For example, "./game/art" becomes "game/art"

	:param path: Full path (may include a file) to convert
	:param to: Optional base path used for the conversion. If not supplied the current working directory is used.

	:return: String containing relative path 

.. cpp:function:: void openFile(string file)

	Open the given file through the system. This will usually open the file in its associated application.

	:param file: Path of the file to open.

.. cpp:function:: void openFolder(string path)

	Open the given folder in the system's file manager.

	:param path: full path to a directory.

.. cpp:function:: String pathConcat(string path, string file)

	Combines two separate strings containing a file path and file name together into a single string.

	:param path: String containing file path
	:param file: String containing file name

	:return: String containing concatenated file name and path 

.. cpp:function:: bool pathCopy(string fromFile, string toFile, bool noOverwrite)

	Copy a file to a new location.

	:param fromFile: Path of the file to copy.
	:param toFile: Path where to copy fromFile to.
	:param noOverwrite: If true, then fromFile will not overwrite a file that may already exist at toFile.

	:return: True if the file was successfully copied, false otherwise. 

.. cpp:function:: bool setCurrentDirectory(string path)

	Set the current working directory.

	:param path: The absolute or relative (to the current working directory) path of the directory which should be made the new working directory.

	:return: , false otherwise.

.. cpp:function:: void startFileChangeNotifications()

	Start watching resources for file changes. Typically this is called during initializeCore().

.. cpp:function:: void stopFileChangeNotifications()

	Stop watching resources for file changes. Typically this is called during shutdownCore().

Variables
---------

.. cpp:member:: string $Con::File

	The currently executing script file.

.. cpp:member:: string $Con::Root

	The mod folder for the currently executing script file.

File Searching
--------------

Functions for searching files by name patterns. 

Functions
~~~~~~~~~

.. cpp:function:: String findFirstFile(string pattern, bool recurse)

	Returns the first file in the directory system matching the given pattern. Use the corresponding findNextFile() to step through the results. If you're only interested in the number of files returned by the pattern match, use getFileCount() . This function differs from findFirstFileMultiExpr() in that it supports a single search pattern being passed in.

	:param pattern: The path and file name pattern to match against.
	:param recurse: If true, the search will exhaustively recurse into subdirectories of the given path and match the given filename pattern.

	:return: The path of the first file matched by the search or an empty string if no matching file could be found.

	Example::

		// Execute all .cs files in a subdirectory and its subdirectories.
		for( %file = findFirstFile( "subdirectory/*.cs" ); %file !$= ""; %file = findNextFile() )
		   exec( %file );

.. cpp:function:: String findFirstFileMultiExpr(string pattern, bool recurse)

	Returns the first file in the directory system matching the given patterns. Use the corresponding findNextFileMultiExpr() to step through the results. If you're only interested in the number of files returned by the pattern match, use getFileCountMultiExpr() . This function differs from findFirstFile() in that it supports multiple search patterns to be passed in.

	:param pattern: The path and file name pattern to match against, such as .cs. Separate multiple patterns with TABs. For example: ".cs" TAB ".dso"
	:param recurse: If true, the search will exhaustively recurse into subdirectories of the given path and match the given filename patterns.

	:return: String of the first matching file path, or an empty string if no matching files were found.

	Example::

		// Find all DTS or Collada models
		%filePatterns = "*.dts" TAB "*.dae";
		%fullPath = findFirstFileMultiExpr( %filePatterns );
		while ( %fullPath !$= "" )
		{
		   echo( %fullPath );
		   %fullPath = findNextFileMultiExpr( %filePatterns );
		}

.. cpp:function:: String findNextFile(string pattern)

	Returns the next file matching a search begun in findFirstFile() .

	:param pattern: The path and file name pattern to match against. This is optional and may be left out as it is not used by the code. It is here for legacy reasons.

	:return: The path of the next filename matched by the search or an empty string if no more files match.

	Example::

		// Execute all .cs files in a subdirectory and its subdirectories.
		for( %file = findFirstFile( "subdirectory/*.cs" ); %file !$= ""; %file = findNextFile() )
		   exec( %file );

.. cpp:function:: String findNextFileMultiExpr(string pattern)

	Returns the next file matching a search begun in findFirstFileMultiExpr() .

	:param pattern: The path and file name pattern to match against. This is optional and may be left out as it is not used by the code. It is here for legacy reasons.

	:return: String of the next matching file path, or an empty string if no matching files were found.

	Example::

		// Find all DTS or Collada models
		%filePatterns = "*.dts" TAB "*.dae";
		%fullPath = findFirstFileMultiExpr( %filePatterns );
		while ( %fullPath !$= "" )
		{
		   echo( %fullPath );
		   %fullPath = findNextFileMultiExpr( %filePatterns );
		}

.. cpp:function:: int getFileCount(string pattern, bool recurse)

	Returns the number of files in the directory tree that match the given patterns. This function differs from getFileCountMultiExpr() in that it supports a single search pattern being passed in. If you're interested in a list of files that match the given pattern and not just the number of files, use findFirstFile() and findNextFile() .

	:param pattern: The path and file name pattern to match against.
	:param recurse: If true, the search will exhaustively recurse into subdirectories of the given path and match the given filename pattern counting files in subdirectories.

	:return: Number of files located using the pattern

	Example::

		// Count the number of .cs files in a subdirectory and its subdirectories.
		getFileCount( "subdirectory/*.cs" );

.. cpp:function:: int getFileCountMultiExpr(string pattern, bool recurse)

	Returns the number of files in the directory tree that match the given patterns. If you're interested in a list of files that match the given patterns and not just the number of files, use findFirstFileMultiExpr() and findNextFileMultiExpr() .

	:param pattern: The path and file name pattern to match against, such as .cs. Separate multiple patterns with TABs. For example: ".cs" TAB ".dso"
	:param recurse: If true, the search will exhaustively recurse into subdirectories of the given path and match the given filename pattern.

	:return: Number of files located using the patterns

	Example::

		// Count all DTS or Collada models
		%filePatterns = "*.dts" TAB "*.dae";
		echo( "Nunmer of shape files:" SPC getFileCountMultiExpr( %filePatterns ) );
