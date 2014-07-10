Basic Syntax
============

Like other languages, TorqueScript has certain syntactical rules you need to follow. The language is very forgiving, easy to debug, and is not as strict as a low level language like C++. Observe the following line in a script::

	// Create test variable with a temporary variable
	%testVariable = 3;

The three most simple rules obeyed in the above code are:

#. Ending a line with a semi-colon ``;``
#. Proper use of white space.
#. Commenting.

The engine will parse code line by line, stopping whenever it reaches a semi-colon. This is referred to as a statement terminator, common to other programming languages such as C++, JavaScript, etc. The following code will produce an error that may cause your entire script to fail::

	%testVariable = 3
	%anotherVariable = 4;

To the human eye, you are able to discern two separate lines of code with different actions. Here is how the script compiler will read it::

	%testVariable = 3%anotherVariable = 4;

This is obviously not what the original code was meant to do. There are exemptions to this rule, but they come into play when multiple lines of code are supposed to work together for a single action::

	if(%testVariable == 4)
		echo("Variable equals 4");

We have not covered conditional operators or echo commands yet, but you should notice that the first line does not have a semi-colon. The easiest explanation is that the code is telling the compiler: "Read the first line, do the second line if we meet the requirements." In other words, perform operations between semi-colons. Complex operations require multiple lines of code working together.

The second rule, proper use of whitespace, is just as easy to remember. Whitespace refers to how your script code is separated between operations. Let's look at the first example again::

	%testVariable = 3;

The code is storing a value ``3`` in a local variable ``%testVariable``. It is doing so by using a common mathematical operator, the equal sign. TorqueScript recognizes the equal sign and performs the action just as expected. It does not care if there are spaces in the operation::

	%testVariable=3;

The above code works just as well, even without the spaces between the variable, the equal sign, and the ``3``. The whitespace rule makes a lot more sense when combined with the semi-colon rule and multiple lines of code working together. The following will compile and run without error::

	if(%testVariable == 4) echo("Variable equals 4");

Comments
--------

The last rule is optional, but should be used as often as possible if you want to create clean code. Whenever you write code, you should try to use comments. Comments are a way for you to leave notes in code which are not compiled into the game. The compiler will essentially skip over these lines.

There are two different comment syntax styles. The first one uses the two slashes, ``//``. This is used for single line comments::

	// This comment line will be ignored
	// This second line will also be ignored
	%testVariable = 3;
	// This third line will also be ignored

In the last example, the only line of code that will be executed has to do with ``%testVariable``. If you need to comment large chunks of code, or leave a very detailed message, you can use the ``/*comment*/`` syntax. The ``/*`` starts the commenting, the ``*/`` ends the commenting, and anything in between will be considered a comment::

	/*
	While attending school, an instructor taught a mantra I still use:

	"Read. Read Code. Code."

	Applying this to Torque 3D development is easy: 

	READ the documentation first. 

	READ CODE written by other Torque developers.

	CODE your own prototypes based on what you have learned.
	*/

As you can see, the comment makes full use of whitespace and multiple lines. While it is important to comment what the code does, you can also use this to temporarily remove unwanted code until a better solution is found::

	// Why are you using multiple if statements. Why not use a switch$?
	/*
	if(%testVariable == "Mich")
	  echo("User name: ", %testVariable);

	if(%testVariable == "Heather")
	  echo("User Name: ", %testVariable);

	if(%testVariable == "Nikki")
	  echo("User Name: ", %testVariable);
	*/
