Console
=======

The basis of the TorqueScript system and command execution.

Functions
---------

.. cpp:function:: void cls()

	Clears the console output.

.. cpp:function:: void debugEnumInstances(string className, string functionName)

	Call the given function for each instance of the given class.

	:param className: Name of the class for which to enumerate instances.
	:param functionName: Name of function to call and pass each instance of the given class.

.. cpp:function:: bool dumpEngineDocs(string outputFile)

	Dumps the engine scripting documentation to the specified file overwriting any existing content.

	:param outputFile: The relative or absolute output file path and name.

	:return: Returns true if successful. 

.. cpp:function:: SimXMLDocument  exportEngineAPIToXML()

	Create a XML document containing a dump of the entire exported engine API.

	:return:  containing a dump of the engine's export information or NULL if the operation failed. 

.. cpp:function:: string getCategoryOfClass(string className)

	Returns the category of the given class.

	:param className: The name of the class.

.. cpp:function:: string getDescriptionOfClass(string className)

	Returns the description string for the named class.

	:param className: The name of the class.

	:return: The class description in string format. 

.. cpp:function:: bool isClass(string identifier)

	Returns true if the passed identifier is the name of a declared class.

.. cpp:function:: bool isMemberOfClass(string className, string superClassName)

	Returns true if the class is derived from the super class. If either class doesn't exist this returns false.

	:param className: The class name.
	:param superClassName: The super class to look for.

.. cpp:function:: bool isValidObjectName(string name)

	Return true if the given name makes for a valid object name.

	:param name: Name of object

	:return: True if name is allowed, false if denied (usually because it starts with a number, _, or invalid character 

.. cpp:function:: SimObject  loadObject(string filename)

	Loads a serialized object from a file.

	:param Name: and path to text file containing the object

.. cpp:function:: bool saveObject(SimObject object, string filename)

	Serialize the object to a file.

	:param object: The object to serialize.
	:param filename: The file name and path.

.. cpp:function:: void unitTest_runTests()

	Run unit tests, or just the tests that prefix match against the searchString.

Variables
---------

.. cpp:member:: string $instantGroup

	The group that objects will be added to when they are created.

.. cpp:member:: bool $Con::alwaysUseDebugOutput

	Determines whether to send output to the platform's "debug" system.

.. cpp:member:: bool $Con::logBufferEnabled

	If true, the log buffer will be enabled.

.. cpp:member:: int $Con::objectCopyFailures

	If greater than zero then it counts the number of object creation failures based on a missing copy object and does not report an error..

.. cpp:member:: int $Con::printLevel

	This is deprecated. It is no longer in use and does nothing.

.. cpp:member:: bool $Con::useTimestamp

	If true a timestamp is prepended to every console message.

.. cpp:member:: bool $Con::warnUndefinedVariables

	If true, a warning will be displayed in the console whenever a undefined variable is used in script.

Debugging
---------

Functionality to help spot program errors. Also provides profiler functions, helpful in determining performance bottlenecks.

Functions
~~~~~~~~~

.. cpp:function:: void backtrace()

	Prints the scripting call stack to the console log. Used to trace functions called from within functions. Can help discover what functions were called (and not yet exited) before the current point in scripts.

.. cpp:function:: void debug()

	Drops the engine into the native C++ debugger. This function triggers a debug break and drops the process into the IDE's debugger. If the process is not running with a debugger attached it will generate a runtime error on most platforms.

.. cpp:function:: void debugDumpAllObjects()

	Dumps all current EngineObject instances to the console.

.. cpp:function:: void debugv(string variableName)

	Logs the value of the given variable to the console. Prints a string of the form " lt variableName gt = lt variable value gt " to the console.

	:param variableName: Name of the local or global variable to print.

	Example::

		%var = 1;
		debugv( "%var" ); // Prints "%var = 1"

.. cpp:function:: void dumpAlloc(int allocNum)

	Dumps information about the given allocated memory block.

	:param allocNum: Memory block to dump information about.

.. cpp:function:: void dumpMemSnapshot(string fileName)

	Dumps a snapshot of current memory to a file. The total memory used will also be output to the console. This function will attempt to create the file if it does not already exist.

	:param fileName: Name and path of file to save profiling stats to. Must use forward slashes (/)

	Example::

		dumpMemSnapshot( "C:/Torque/ProfilerLogs/profilerlog1.txt" );

.. cpp:function:: void dumpUnflaggedAllocs(string fileName)

	Dumps all unflagged memory allocations. Dumps all memory allocations that were made after a call to flagCurrentAllocs() . Helpful when used with flagCurrentAllocs() for detecting memory leaks and analyzing general memory usage.

	:param fileName: Optional file path and location to dump all memory allocations not flagged by flagCurrentAllocs(). If left blank, data will be dumped to the console.

	Example::

		dumpMemSnapshot(); // dumps info to console
		dumpMemSnapshot( "C:/Torque/profilerlog1.txt" ); // dumps info to file

.. cpp:function:: void flagCurrentAllocs()

	Flags all current memory allocations. Flags all current memory allocations for exclusion in subsequent calls to dumpUnflaggedAllocs() . Helpful in detecting memory leaks and analyzing memory usage.

.. cpp:function:: void freeMemoryDump()

	Dumps some useful statistics regarding free memory. Dumps an analysis of 'free chunks' of memory. Does not print how much memory is free.

.. cpp:function:: void profilerDump()

	Dumps current profiling stats to the console window.

.. cpp:function:: void profilerDumpToFile(string fileName)

	Dumps current profiling stats to a file.

	:param fileName: Name and path of file to save profiling stats to. Must use forward slashes (/). Will attempt to create the file if it does not already exist.

	Example::

		profilerDumpToFile( "C:/Torque/log1.txt" );

.. cpp:function:: void profilerEnable(bool enable)

	Enables or disables the profiler. Data is only gathered while the profiler is enabled.

.. cpp:function:: void profilerMarkerEnable(string markerName, bool enable)

	Enable or disable a specific profile.

	:param enable: Optional paramater to enable or disable the profile.
	:param markerName: Name of a specific marker to enable or disable.

.. cpp:function:: void profilerReset()

	Resets the profiler, clearing it of all its data. If the profiler is currently running, it will first be disabled. All markers will retain their current enabled/disabled status.

.. cpp:function:: int sizeof(string objectOrClass)

	Determines the memory consumption of a class or object.

	:param objectOrClass: The object or class being measured.

	:return: Returns the total size of an object in bytes. 

.. cpp:function:: void telnetSetParameters(int port, string consolePass, string listenPass, bool remoteEcho)

	Initializes and open the telnet console.

	:param port: Port to listen on for console connections (0 will shut down listening).
	:param consolePass: Password for read/write access to console.
	:param listenPass: Password for read access to console.
	:param remoteEcho: [optional] Enable echoing back to the client, off by default.

.. cpp:function:: void trace(bool enable)

	Enable or disable tracing in the script code VM. When enabled, the script code runtime will trace the invocation and returns from all functions that are called and log them to the console. This is helpful in observing the flow of the script program.

	:param enable: New setting for script trace execution, on by default.

.. cpp:function:: void validateMemory()

	Used to validate memory space for the game.

Variables
~~~~~~~~~

.. cpp:member:: int  getAppVersionNumber

	Get the version of the application build, as a string.

.. cpp:member:: string  getAppVersionString

	Get the version of the aplication, as a human readable string.

.. cpp:member:: string  getBuildString

	Get the type of build, "Debug" or "Release".

.. cpp:member:: string  getCompileTimeString

	Get the time of compilation.

.. cpp:member:: string  getEngineName

	Get the name of the engine product that this is running from, as a string.

.. cpp:member:: int  getVersionNumber

	Get the version of the engine build, as a string.

.. cpp:member:: string  getVersionString

	Get the version of the engine build, as a human readable string.

Logging
-------

Functions for logging messages, warnings, and errors to the console.

Classes
~~~~~~~

.. toctree::
	:maxdepth: 1

	class/ConsoleLogger

Enumeration
~~~~~~~~~~~

.. cpp:member:: enum  LogLevel

	Priority levels for logging entries.

	:param normal: Lowest priority level, no highlighting.
	:param warning: Mid level priority, tags and highlights possible issues in blue.
	:param error: Highest priority level, extreme emphasis on this entry. Highlighted in red.

Functions
~~~~~~~~~

.. cpp:function:: void dumpConsoleClasses(bool dumpScript, bool dumpEngine)

	Dumps all declared console classes to the console.

	:param dumpScript: Optional parameter specifying whether or not classes defined in script should be dumped.
	:param dumpEngine: Optional parameter specifying whether or not classes defined in the engine should be dumped.

.. cpp:function:: void dumpConsoleFunctions(bool dumpScript, bool dumpEngine)

	Dumps all declared console functions to the console.

	:param dumpScript: Optional parameter specifying whether or not functions defined in script should be dumped.
	:param dumpEngine: Optional parameter specitying whether or not functions defined in the engine should be dumped.

.. cpp:function:: void echo(string message, ...)

	Logs a message to the console. Concatenates all given arguments to a single string and prints the string to the console. A newline is added automatically after the text.

	:param message: Any number of string arguments.

.. cpp:function:: void error(string message, ...)

	Logs an error message to the console. Concatenates all given arguments to a single string and prints the string to the console as an error message (in the in-game console, these will show up using a red font by default). A newline is added automatically after the text.

	:param message: Any number of string arguments.

.. cpp:function:: void log(string message)

	Logs a message to the console.

	:param message: The message text.

.. cpp:function:: void logError(string message)

	Logs an error message to the console.

	:param message: The message text.

.. cpp:function:: void logWarning(string message)

	Logs a warning message to the console.

	:param message: The message text.

.. cpp:function:: void setLogMode(int mode)

	Determines how log files are written. Sets the operational mode of the console logging system. Additionally, when changing the log mode and thus opening a new log file, either of the two mode values may be combined by binary OR with 0x4 to cause the logging system to flush all console log messages that had already been issued to the console system into the newly created log file.

	:param mode: Parameter specifying the logging mode. This can be:1: Open and close the console log file for each seperate string of output. This will ensure that all parts get written out to disk and that no parts remain in intermediate buffers even if the process crashes.2: Keep the log file open and write to it continuously. This will make the system operate faster but if the process crashes, parts of the output may not have been written to disk yet and will be missing from the log.

.. cpp:function:: void warn(string message, ...)

	Logs a warning message to the console. Concatenates all given arguments to a single string and prints the string to the console as a warning message (in the in-game console, these will show up using a turquoise font by default). A newline is added automatically after the text.

	:param message: Any number of string arguments.

Messaging
---------

Script classes and functions used for passing messages and events between classes. 

Classes
~~~~~~~

.. toctree::
	:maxdepth: 1

	class/EventManager
	class/Message
	class/MessageForwarder
	class/ScriptMsgListener

Functions
~~~~~~~~~

.. cpp:function:: bool dispatchMessage(string queueName, string message, string data)

	Dispatch a message to a queue.

	:param queueName: Queue to dispatch the message to
	:param message: Message to dispatch
	:param data: Data for message

	:return: True for success, false for failure 

.. cpp:function:: bool dispatchMessageObject(string queueName, string message)

	Dispatch a message object to a queue.

	:param queueName: Queue to dispatch the message to
	:param message: Message to dispatch

	:return: true for success, false for failure 

.. cpp:function:: bool isQueueRegistered(string queueName)

	Determines if a dispatcher queue exists.

	:param queueName: String containing the name of queue

.. cpp:function:: bool registerMessageListener(string queueName, string listener)

	Registers an event message.

	:param queueName: String containing the name of queue to attach listener to
	:param listener: Name of event messenger

.. cpp:function:: void registerMessageQueue(string queueName)

	Registeres a dispatcher queue.

	:param queueName: String containing the name of queue

.. cpp:function:: void unregisterMessageListener(string queueName, string listener)

	Unregisters an event message.

	:param queueName: String containing the name of queue
	:param listener: Name of event messenger

.. cpp:function:: void unregisterMessageQueue(string queueName)

	Unregisters a dispatcher queue.

	:param queueName: String containing the name of queue

Packages
--------

Functions relating to the control of packages. 

Functions
~~~~~~~~~

.. cpp:function:: void activatePackage(string packageName)

	Activates an existing package. The activation occurs by updating the namespace linkage of existing functions and methods. If the package is already activated the function does nothing.

.. cpp:function:: void deactivatePackage(string packageName)

	Deactivates a previously activated package. The package is deactivated by removing its namespace linkages to any function or method. If there are any packages above this one in the stack they are deactivated as well. If the package is not on the stack this function does nothing.

.. cpp:function:: string getFunctionPackage(string funcName)

	Provides the name of the package the function belongs to.

	:param funcName: String containing name of the function

	:return: The name of the function's package 

.. cpp:function:: string getMethodPackage(string namespace, string method)

	Provides the name of the package the method belongs to.

	:param namespace: Class or namespace, such as Player
	:param method: Name of the funciton to search for

	:return: The name of the method's package 

.. cpp:function:: string getPackageList()

	Returns a space delimited list of the active packages in stack order.

.. cpp:function:: bool isPackage(string identifier)

	Returns true if the identifier is the name of a declared package.

Scripting
---------

Functions for working with script code.

Classes
~~~~~~~

.. toctree::
	:maxdepth: 1

	class/ArrayObject
	class/ScriptGroup
	class/ScriptObject
	class/ScriptTickObject

Functions
~~~~~~~~~

.. cpp:function:: string call(string functionName, string args, ...)

	Apply the given arguments to the specified global function and return the result of the call.

	:param functionName: The name of the function to call. This function must be in the global namespace, i.e. you cannot call a function in a namespace through call. Use eval() for that.

	:return: The result of the function call.

	Example::

		function myFunction( %arg )
		{
		  return ( %arg SPC "World!" );
		}
		
		echo( call( "myFunction", "Hello" ) ); 
		// Prints "Hello World!" to the console.

.. cpp:function:: bool compile(string fileName, bool overrideNoDSO)

	Compile a file to bytecode. This function will read the TorqueScript code in the specified file, compile it to internal bytecode, and, if DSO generation is enabled or overrideNoDDSO is true, will store the compiled code in a .dso file in the current DSO path mirrorring the path of fileName .

	:param fileName: Path to the file to compile to bytecode.
	:param overrideNoDSO: If true, force generation of DSOs even if the engine is compiled to not generate write compiled code to DSO files.

	:return: True if the file was successfully compiled, false if not.

.. cpp:function:: void deleteVariables(string pattern)

	Undefine all global variables matching the given name pattern .

	:param pattern: A global variable name pattern. Must begin with '$'.

	Example::

		// Define a global variable in the "My" namespace.
		$My::Variable = "value";
		
		// Undefine all variable in the "My" namespace.
		deleteVariables( "$My::*" );

.. cpp:function:: bool exec(string fileName, bool noCalls, bool journalScript)

	Execute the given script file.

	:param fileName: Path to the file to execute
	:param noCalls: Deprecated
	:param journalScript: Deprecated

	:return: True if the script was successfully executed, false if not.

	Example::

		// Execute the init.cs script file found in the 
		// same directory as the current script file.
		exec( "./init.cs" );

.. cpp:function:: bool execPrefs(string relativeFileName, bool noCalls, bool journalScript)

	Manually execute a special script file that contains game or editor preferences.

	:param relativeFileName: Name and path to file from project folder
	:param noCalls: Deprecated
	:param journalScript: Deprecated

	:return: True if script was successfully executed 

.. cpp:function:: void export(string pattern, string filename, bool append)

	Write out the definitions of all global variables matching the given name pattern . If fileName is not "", the variable definitions are written to the specified file. Otherwise the definitions will be printed to the console. The output are valid TorqueScript statements that can be executed to restore the global variable values.

	:param pattern: A global variable name pattern. Must begin with '$'.
	:param filename: Path of the file to which to write the definitions or "" to write the definitions to the console.
	:param append: If true and fileName is not "", then the definitions are appended to the specified file. Otherwise existing contents of the file (if any) will be overwritten.

	Example::

		// Write out all preference variables to a prefs.cs file.
		export( "$prefs::*", "prefs.cs" );

.. cpp:function:: string getDSOPath(string scriptFileName)

	Get the absolute path to the file in which the compiled code for the given script file will be stored.

	:param scriptFileName: Path to the .cs script file.

	:return: The absolute path to the .dso file for the given script file.

.. cpp:function:: string getVariable(string varName)

	Returns the value of the named variable or an empty string if not found. Name of the variable to search for

	:return: Value contained by varName, "" if the variable does not exist 

.. cpp:function:: bool isDefined(string varName)

	Determines if a variable exists and contains a value.

	:param varName: Name of the variable to search for

	:return: True if the variable was defined in script, false if not 

	Example::

		isDefined( "$myVar" );

.. cpp:function:: bool isFunction(string funcName)

	Determines if a function exists or not.

	:param funcName: String containing name of the function

	:return: True if the function exists, false if not 

.. cpp:function:: bool isMethod(string namespace, string method)

	Determines if a class/namespace method exists.

	:param namespace: Class or namespace, such as Player
	:param method: Name of the function to search for

	:return: True if the method exists, false if not 

.. cpp:function:: void setVariable(string varName, string value)

	Sets the value of the named variable.

	:param varName: Name of the variable to locate
	:param value: New value of the variable

	:return: True if variable was successfully found and set 
