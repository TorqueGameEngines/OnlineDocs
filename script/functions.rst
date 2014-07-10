Functions
=========

Much of your TorqueScript experience will come down to calling existing Console Functions and writing your own. Functions are a blocks of code that only execute when you call them by name. Basic functions in TorqueScript are defined as follows::

	// function - Is a keyword telling TorqueScript we are defining a new function.
	// function_name - Is the name of the function we are creating.
	// ... - Is any number of additional arguments.
	// statements - Your custom logic executed when function is called
	// return val - The value the function will give back after it has completed. Optional.

	function function_name([arg0],...,[argn]) 
	{
	    statements;
	    [return val;]
	}

The function keyword, like other TorqueScript keywords, is case sensitive. You must type it exactly as shown above. The following is an example of a custom function that takes in two parameters, then executes code based on those arguments.

TorqueScript can take any number of arguments, as long as they are comma separated. If you call a function and pass fewer parameters than the function's definition specifies, the un-passed parameters will be given an empty string as their default value::

	function echoRepeat (%echoString, %repeatCount) 
	{
	   for (%count = 0; %count < %repeatCount; %count++)
	   {
	      echo(%echoString);
	   }
	}

You can cause this function to execute by calling it in the console, or in another function::

	echoRepeat("hello!", 5);

	OUTPUT:
	"hello!"
	"hello!"
	"hello!"
	"hello!"
	"hello!"

If you define a function and give it the same name as a previously defined function, TorqueScript will completely override the old function. This still applies even if you change the number of parameters used; the older function will still be overridden.

Torque 3D also contain Console Functions written in C++, then exposed to TorqueScript. These are global functions you can call at any time, and are usually very helpful or important. E.g. throughout this document, we have been using the Console Function ``echo(...)``.
