Syntax Guide
**************

The Basics
===========

Main Rules
^^^^^^^^^^^

Like other languages, TorqueScript has certain syntactical rules you need to follow. The language is very forgiving, easy to debug, and is not as strict as a low level language like C++. Observe the following line in a script::

	// Create test variable with a temporary variable
	%testVariable = 3;

The three most simple rules obeyed in the above code are:

#. Ending a line with a semi-colon ``;``
#. Proper use of white space.
#. Commenting.

The engine will parse code line by line, stopping whenever it reaches a semi-colon. This is referred to as a **statement terminator**, common to other programming languages such as C++, JavaScript, etc. The following code will produce an error that may cause your entire script to fail::

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
^^^^^^^^^

The last rule is optional, but should be used as often as possible if you want to create clean code. Whenever you write code, you should try to use **comments**. Comments are a way for you to leave notes in code which are not compiled into the game. The compiler will essentially skip over these lines.

There are two different comment syntax styles. The first one uses the two slashes, ``//``. This is used for single line comments:

Example::

	// This comment line will be ignored
	// This second line will also be ignored
	%testVariable = 3;
	// This third line will also be ignored

In the last example, the only line of code that will be executed has to do with ``%testVariable``. If you need to comment large chunks of code, or leave a very detailed message, you can use the ``/*comment*/`` syntax. The ``/*`` starts the commenting, the ``*/`` ends the commenting, and anything in between will be considered a comment:

Example::

	/*
	While attending school, an instructor taught a mantra I still use:

	"Read. Read Code. Code."

	Applying this to Torque 3D development is easy: 

	READ the documentation first. 

	READ CODE written by other Torque developers.

	CODE your own prototypes based on what you have learned.
	*/

As you can see, the comment makes full use of whitespace and multiple lines. While it is important to comment what the code does, you can also use this to temporarily remove unwanted code until a better solution is found::

Example::

	// Why are you using multiple if statements. Why not use a switch$?
	/*
	if(%testVariable == "Mich")
	  echo("User name: ", %testVariable);

	if(%testVariable == "Heather")
	  echo("User Name: ", %testVariable);

	if(%testVariable == "Nikki")
	  echo("User Name: ", %testVariable);
	*/

Variables
===========

Usage
^^^^^^

A variable is a letter, word, or phrase linked to a value stored in your game's memory and used during operations. Creating a variable is a one line process. The following code creates a variable by naming it and assigning a value::

	%localVariable = 3;

You can assign any type value to the variable you want. This is referred to as a language being **type-insensitive**. TorqueScript does not care (insensitive) what you put in a variable, even after you have created it. The following code is completely valid::

	%localVariable = 27;
	%localVariable = "Heather";
	%localVariable = "7 7 7";

The main purpose of the code is to show that TorqueScript treats all data types the same way. It will interpret and convert the values internally, so you do not have to worry about typecasting. That may seem a little confusing. After all, when would you want a variable that can store a number, a string, or a vector?

You will rarely need to, which is why you want to start practicing good programming habits. An important practice is proper variable naming. The following code will make a lot more sense, considering how the variables are named::

	%userName = "Heather";
	%userAge = 27;
	%userScores = "7 7 7";

TorqueScript is more forgiving than low level programming languages. While it expects you to obey the basic syntax rules, it will allow you to get away with small mistakes or inconsistency. The best example is variable **case sensitivity**. With variables, TorqueScript is not case sensitive. You can create a variable and refer to it during operations without adhering to case rules::

	%userName = "Heather";
	echo(%Username);

In the above code, ``%userName`` and ``%Username``	 are the same variable, even though they are using different capitalization. You should still try to remain consistent in your variable naming and usage, but you will not be punished if you slip up occasionally.

Variable Types
^^^^^^^^^^^^^^^

There are two types of variables you can declare and use in TorqueScript: *local* and *global.* Both are created and referenced similarly::

	%localVariable = 1;
	$globalVariable = 2;

As you can see, local variable names are preceded by the percent sign ``%``. Global variables are preceded by the dollar sign ``$``. Both types can be used in the same manner: operations, functions, equations, etc. The main difference has to do with how they are **scoped**.

In programming, scoping refers to where in memory a variable exists during its life. A local variable is meant to only exist in specific blocks of code, and its value is discarded when you leave that block. Global variables are meant to exist and hold their value during your entire programs execution. Look at the following code to see an example of a local variable::

	function test()
	{
	   %userName = "Heather";
	   echo(%userName);
	}

We will cover functions a little later, but you should know that functions are blocks of code that only execute when you call them by name. This means the variable, ``%userName``, does not exist until the ``test()`` function is called. When the function has finished all of its logic, the ``%userName`` variable will no longer exist. If you were to try to access the ``%userName`` variable outside of the function, you will get nothing.

Most variables you will work with are local, but you will eventually want a variables that last for your entire game. These are extremely important values used throughout the project. This is when global variables become useful. For the most part, you can declare global variables whenever you want::

	$PlayerName = "Heather";

	function printPlayerName()
	{
	   echo($PlayerName);
	}

	function setPlayerName()
	{
	   $PlayerName = "Nikki";
	}

The above code makes full use of a global variable that holds a player's name. The first declaration of the variable happens outside of the functions, written anywhere in your script. Because it is global, you can reference it in other locations, including separate script files. Once declared, your game will hold on to the variable until shutdown.

Data Types
===========
TorqueScript implicitly supports several variable data-types: numbers, strings, booleans, arrays and vectors. If you wish to test the various data types, you can use the **echo(...)** command. For example::

   %meaningOfLife = 42;
   echo(%meaningOfLife);
   
   $name = "Heather";
   echo($name);

The echo will post the results in the console, which can be accessed by pressing the tilde key (~) while in game.

Numbers
^^^^^^^^
TorqueScript handles standard numeric types::

   123     (Integer)
   1.234   (floating point)
   1234e-3 (scientific notation)
   0xc001  (hexadecimal)

Strings
^^^^^^^^
Text, such as names or phrases, are supported as strings. Numbers can also be stored in string format. Standard strings are stored in double-quotes:: 

   "abcd"    (string)

Example::

   $UserName = "Heather";
   
Strings with single quotes are called "tagged strings"::

   'abcd'  (tagged string)


Tagged strings are special in that they contain string data, but also have a special numeric tag associated with them. Tagged strings are used for sending string data across a network. The value of a tagged string is only sent once, regardless of how many times you actually do the sending.

On subsequent sends, only the tag value is sent. Tagged values must be de-tagged when printing. You will not need to use a tagged string often unless you are in need of sending strings across a network often, like a chat system. 

Example::

   $a = 'This is a tagged string';
   echo("  Tagged string: ", $a);
   echo("Detagged string: ", detag($a));

The output will be similar to this::

   Tagged string: 24
   Detagged string:

The second echo will be **blank** unless the string has been passed to you over a network.

String Operators
^^^^^^^^^^^^^^^^^^

There are special values you can use to concatenate strings and variables. Concatenation refers to the joining of multiple values into a single variable. The following is the basic syntax::

   "string 1" operation "string 2"

You can use string operators similarly to how you use mathematical operators (=, +, -, *). You have four operators at your disposal:

========  ===============  ============= ===========
Operator  Name             Example       Explanation
========  ===============  ============= ===========
``@``     String           ``$c @ $d``   Concatenates strings ``$c`` and ``$d``
                                         into a single string. Numeric 
                                         literals/variables convert to strings. 
``NL``    New Line         ``$c NL $d``  Concatenates strings ``$c`` and ``$d``
                                         into a single string separated by new-line.
                                         **Note:** such a string can be decomposed with getRecord() 
``TAB``   Tab              ``$c TAB $d`` Concatenates strings ``$c`` and ``$d``
                                         into a single string separated by tab.
                                         **Note:** such a string can be decomposed with getField() 
``SPC``   Space            ``$c SCP $d`` Concatenates strings ``$c`` and ``$d``
                                         into a single string separated by space.
                                         **Note:** such a string can be decomposed with getWord() 

========  ===============  ============= ===========


The @ symbol will concatenate two strings together exactly how you specify, without adding any additional whitespace:

*Note: Do not type in OUPUT: ___. This is placed in the sample code to show you what the console would display.*

Example::

   %newString = "Hello" @ "World";
   echo(%newString);
   
   OUPUT: 
   HelloWorld
   
Notice how the two strings are joined without any spaces. If you include whitespace, it will be concatenated along with the values: 

Example::

   %newString = "Hello " @ "World";
   echo(%newString);
   
   OUTPUT: 
   Hello World
   
Example::

   %hello = "Hello ";
   %world = "World";
   
   echo(%hello @ %world);
   
   OUTPUT: 
   Hello World
   
The rest of the operators will apply whitespace for you, so you do not have to include it in your values. Example::

   echo("Hello" @ "World");
   echo("Hello" TAB "World");
   echo("Hello" SPC "World");
   echo("Hello" NL "World");
   
   OUTPUT:
   HelloWorld
   Hello   World
   Hello World
   Hello
   World

Booleans
^^^^^^^^^
Like most programming languages, TorqueScript also supports Booleans. Boolean numbers have only two values- true or false::

   true    (1)
   false   (0)


Again, as in many programming languages the constant "true" evaluates to the number 1 in TorqueScript, and the constant "false" evaluates to the number 0. However, non-zero values are also considered true. Think of booleans as "on/off" switches, often used in conditional statements. Example::

   $lightsOn = true;
   
   if($lightsOn)
      echo("Lights are turned on");

  
Arrays
^^^^^^^

Arrays are data structures used to store consecutive values of the same data type:: 

   $TestArray[n]   (Single-dimension)
   $TestArray[m,n] (Multidimensional)
   $TestArray[m_n] (Multidimensional)


If you have a list of similar variables you wish to store together, try using an array to save time and create cleaner code. The syntax displayed above uses the letters 'n' and 'm' to represent where you will input the number of elements in an array. The following example shows code that could benefit from an array. Example::

   $firstUser = "Heather";
   $secondUser = "Nikki";
   $thirdUser = "Mich";
   
   echo($firstUser);
   echo($secondUser);
   echo($thirdUser);

Instead of using a global variable for each user name, we can put those values into a single array. Example::

   $userNames[0] = "Heather";
   $userNames[1] = "Nikki";
   $userNames[2] = "Mich";
   
   echo($userNames[0]);
   echo($userNames[1]);
   echo($userNames[2]);

Now, let's break the code down. Like any other variable declaration, you can create an array by giving it a name and value::

   $userNames[0] = "Heather";

What separates an array declaration from a standard variable is the use of brackets []. The number you put between the brackets is called the **index**. The index will access a specific element in an array, allowing you to view or manipulate the data. All the array values are stored in consecutive order.

If you were able to see an array on paper, it would look something like this::

   [0] [1] [2]
   
In our example, the data looks like this::

   ["Heather"] ["Nikki"] ["Mich"]
   
Like other programming languages, the index is always a numerical value and the starting index is always 0. Just remember, index 0 is always the first element in an array. As you can see in the above example, we create the array by assigning the first index (0) a string value ("Heather").

The next two lines continue filling out the array, progressing through the index consecutively:: 

   $userNames[1] = "Nikki";
   $userNames[2] = "Mich";
   
The second array element (index 1) is assigned a different string value ("Nikki"), as is the third (index 2). At this point, we still have a single array structure, but it is holding three separate values we can access. Excellent for organization.

The last section of code shows how you can access the data that has been stored in the array. Again, you use a numerical index to point to an element in the array. If you want to access the first element, use 0::   

   echo($userNames[0]);

In a later section, you will learn about looping structures that make using arrays a lot simpler. Before moving on, you should know that an array does not have to be a single, ordered list. TorqueScript also support multidimensional arrays.


An single-dimensional array contains a single row of values. A multidimensional array is essentially an array of arrays, which introduces columns as well. The following is a visual of what a multidimensional looks like with three rows and three columns::

   [x] [x] [x]
   [x] [x] [x]
   [x] [x] [x]
   
Defining this kind of array in TorqueScript is simple. The following creates an array with 3 rows and 3 columns:: 

   $testArray[0,0] = "a";
   $testArray[0,1] = "b";
   $testArray[0,2] = "c";
   
   $testArray[1,0] = "d";
   $testArray[1,1] = "e";
   $testArray[1,2] = "f";
   
   $testArray[2,0] = "g";
   $testArray[2,1] = "h";
   $testArray[2,2] = "i";

Notice that we are are now using two indices, both starting at 0 and stopping at 2. We can use these as coordinates to determine which array element we are accessing:: 

   [0,0] [0,1] [0,2]
   [1,0] [1,1] [1,2]
   [2,0] [2,1] [2,2]

In our example, which progresses through the alphabet, you can visualize the data in the same way::

   [a] [b] [c]
   [d] [e] [f]
   [g] [h] [i]

The first element [0,0] points to the letter 'a'. The last element [2,2] points to the letter 'i'. 
   
Vectors
^^^^^^^^

"Vectors" are a helpful data-type which are used throughout Torque 3D. For example, many fields in the World Editor take numeric values in sets of 3 or 4. These are stored as strings and interpreted as "vectors"::

   "1.0 1.0 1.0"   (3 element vector)

The most common example of a vector would be a world position. Like most 3D coordinate systems, an object's position is stored as (X Y Z). You can use a three element vector to hold this data::

   %position = "25.0 32 42.5";

You can separate the values using spaces or tabs (both are acceptable whitespace). Another example is storing color data in a four element vector. The values that make up a color are "Red Blue Green Alpha," which are all numbers. You can create a vector for color using hard numbers, or variables::

   %firstColor = "100 100 100 255";
   echo(%firstColor);
   
   %red = 128;
   %blue = 255;
   %green = 64;
   %alpha = 255;
   
   %secondColor = %red SPC %blue SPC %green SPC %alpha;
   echo(%secondColor);


Operators
===========

Operators in TorqueScript behave very similarly to operators in real world math and other programming languages. You should recognize quite a few of these from math classes you took in school, but with small syntactical changes. The rest of this section will explain the syntax and show a brief example, but we will cover these in depth in later guides.


Arithmetic Operators
^^^^^^^^^^^^^^^^^^^^^^

These are your basic math ops. 

========  ===============  ===========  ===========
Operator  Name             Example      Explanation
========  ===============  ===========  ===========
``*``     multiplication   ``$a * $b``  Multiply ``$a`` and ``$b``.
``/``     division         ``$a / $b``  Divide ``$a`` by ``$b``.
``%``     modulo           ``$a % $b``  Remainder of ``$a`` divided by ``$b``.
``+``     addition         ``$a + $b``  Add ``$a`` and ``$b``.
``-``     subtraction      ``$a - $b``  Subtract ``$b`` from ``$a``.
``++``    auto-increment   ``$a++``     Increment ``$a``. 

          (post-fix only)

``--``    auto-decrement   ``$b--``     Decrement ``$b``.

          (post-fix only)

========  ===============  ===========  ===========

.. note:: 
	
	``++$a`` is illegal. The value of ``$a++`` is that of the incremented variable: auto-increment is post-fix in syntax, but pre-increment in sematics (the variable is incremented, *before* the return value is calculated). This behavior is unlike that of C and C++.

.. note::
	
	``--$b`` is illegal. The value of ``$a--`` is that of the decremented variable: auto-decrement is post-fix in syntax, but pre-decrement in sematics (the variable is decremented, *before* the return value is calculated). This behavior is unlike that of C and C++.

Relational Operators
^^^^^^^^^^^^^^^^^^^^^^
Used in comparing values and variables against each other. 

**Relations (Arithmetic, Logical, and String)**

========  =====================  =============  ===========
Operator  Name                   Example        Explanation
========  =====================  =============  ===========
``<``     Less than              ``$a < $b``    1 if ``$a`` is less than ``$b``
``>``     More than              ``$a > $b``    1 if ``$a`` is greater than ``$b``
``<=``    Less than or Equal to  ``$a <= $b``   1 if ``$a`` is less than or equal to ``$b``
``>=``    More than or Equal to  ``$a >= $b``   1 if ``$a`` is greater than or equal to ``$b``
``==``    Equal to               ``$a == $b``   1 if ``$a`` is equal to ``$b``
``!=``    Not equal to           ``$a != $b``   1 if ``$a`` is not equal to ``$b``
``!``     Logical NOT            ``!$a``        1 if ``$a`` is 0
``&&``    Logical AND            ``$a && $b``   1 if ``$a`` and ``$b`` are both non-zero
``||``    Logical OR             ``$a || $b``   1 if either ``$a`` or ``$b`` is non-zero
``$=``    String equal to        ``$c $= $d``   1 if ``$c`` equal to ``$d``.
``!$=``    String not equal to   ``$c !$= $d``  1 if ``$c`` not equal to ``$d``.
========  =====================  =============  ===========

Bitwise Operators
^^^^^^^^^^^^^^^^^^
Used for comparing and shifting bits.

========  ==================  ===========  ===========
Operator  Name                Example      Explanation
========  ==================  ===========  ===========
``~``     Bitwise complement  ``~$a``      flip bits 1 to 0 and 0 to 1
``&``     Bitwise AND         ``$a & $b``  composite of elements where bits in same position are 1
``|``     Bitwise OR          ``$a | $b``  composite of elements where bits 1 in either of the two elements
``^``     Bitwise XOR         ``$a ^ $b``  composite of elements where bits in same position are opposite
``<<``    Left Shift          ``$a << 3``  element shifted left by 3 and padded with zeros
``>>``    Right Shift         ``$a >> 3``  element shifted right by 3 and padded with zeros
========  ==================  ===========  ===========

*References: You might find these two guides useful for learning about bitwise operations:*


#. https://en.wikipedia.org/wiki/Bitwise_operation
#. http://www.cprogramming.com/tutorial/bitwise_operators.html

Assignment Operators
^^^^^^^^^^^^^^^^^^^^^^
Used for setting the value of variables. 

**Assignment and Assignment Operators**

========  ====================  ==============  ===========
Operator  Name                  Example         Explanation
========  ====================  ==============  ===========
``=``     Assignment            ``$a = $b;``    Assign value of ``$b`` to ``$a``
                                                **Note:**  the value of an assignment is the value being assigned, so $a = $b = $c is legal.
``op=``   Assignment Operators  ``$a op= $b;``  Equivalent to ``$a = $a op $b``, where op can be any of:  * / % + - & | ^ << >>
========  ====================  ==============  ===========
 
Miscellaneous Operators
^^^^^^^^^^^^^^^^^^^^^^^^^

General programming operators.

=========  ======================  ============================  ===========
Operator   Name                    Example                       Explanation
=========  ======================  ============================  ===========
``? :``    Conditional             ``x ? y : z``                 Evaluates to ``y`` if ``x`` equal to 1, else evaluates to ``z``
``[]``     Array element           ``$a[5]``                     Synonymous with ``$a5``
``( )``    Delimiting, Grouping    ``t2dGetMin(%a, %b)``         Argument list for function call

                                   ``if ( $a == $b )``           Used with if, for, while, switch keywords

                                   ``($a+$b)*($c-$d)``           Control associativity in expressions

``{}``     Compound statement      ``if (1) {$a = 1; $b = 2;}``  Delimit multiple statements, optional for if, else, for, while

                                   ``function foo() {$a = 1;}``  Required for switch, datablock, new, function

``,``      Listing                 ``t2dGetMin(%a, %b)``         Delimiter for arguments.
                                                                 **Note:** there is no "comma operator", as defined in C/C++; $a = 1, $b = 2; is a parse error
                                   ``%M[1,2]``

``::``     Namespace               ``Item::onCollision()``       This definition of the ``onCollision()`` function is in the ``Item`` namespace
``.``      Field/Method selection  ``%obj.field``                Select a console method or field

                                   ``%obj.method()``

``//``     Single-line comment     ``// This is a comment``      Used to comment out a single line of code
``/* */``  Multi-line comment      ``/*This is a a``             Used to comment out multiple consecutive lines

                                   ``multi-line``                ``/*`` opens the comment, and ``*/`` closes it

                                   ``comment*/``
=========  ======================  ============================  ===========


Control Statements
=====================

TorqueScript provides basic branching structures that will be familiar to programmers that have used other languages. If you are completely new to programming, you use branching structures to control your game's flow and logic. This section builds on everything you have learned about TorqueScript so far. 

if, else
^^^^^^^^^
This type of structure is used to test a condition, then perform certain actions if the condition passes or fails. You do not always have to use the full structure, but the following syntax shows the extent of the conditional::

   if(<boolean expression>) 
   {
      pass logic
   }
   else
   {
      alternative logic
   }

Remember how boolean values work? Essentially, a bool can either be true (1) or false (0). The condition (boolean) is always typed into the parenthesis after the "if" syntax. Your logic will be typed within the brackets {}. The following example uses specific variable names and conditions to show how this can be used: 

Example::

   // Global variable that controls lighting
   $lightsShouldBeOn = true;
   
   // Check to see if lights should be on or off
   if($lightsShouldBeOn)
   {
      // True. Call turn on lights function
      turnOnLights();
   
      echo("Lights have been turned on");
   }
   else
   {
      // False. Turn off the lights
      turnOffLights();
   
      echo("Lights have been turned off");
   }

Brackets for single line statements are optional. If you are thinking about adding additional logic to the code, then you should use the brackets anyway. If you know you will only use one logic statement, you can use the following syntax:

Example::

   // Global variable that controls lighting
   $lightsShouldBeOn = true;
   
   // Check to see if lights should be on or off
   if($lightsShouldBeOn)
      turnOnLights();   // True. Call turn on lights function
   else
      turnOffLights(); // False. Turn off the lights


switch and switch$
^^^^^^^^^^^^^^^^^^^

If your code is using several cascading if-then-else statements based on a single value, you might want to use a **switch** statement instead. Switch statements are easier to manage and read. There are two types of switch statements, based on data type: numeric (switch) and string (switch$). 

Switch Syntax::

   switch(<numeric expression>) 
   {
      case value0:
         statements;
      case value1:
         statements;
      case value3:
         statements;
      default:
         statements;
   }

As the above code demonstrates, start by declaring the switch statement by passing in a value to the switch(...) line. Inside of the brackets {}, you will list out all the possible cases that will execute based on what value being tested. It is wise to always use the default case, anticipating rogue values being passed in.

Example::

   switch($ammoCount)
   {
      case 0:
         echo("Out of ammo, time to reload");
         reloadWeapon();
      case 1:
         echo("Almost out of ammo, warn user");
         lowAmmoWarning();
      case 100:
         echo("Full ammo count");
         playFullAmmoSound();
      default:
         doNothing();
   }

switch only properly evaluates numerical values. If you need a switch statement to handle a string value, you will want to use **switch$**. The switch$ syntax is similar to what you just learned:

Switch$ Syntax::

   switch$ (<string expression>) 
   {
      case "string value 0":
                  statements;
      case "string value 1":
                  statements;
   ...
      case "string value N":
                  statements;
      default:
                  statements;
               }

Appending the $ sign to switch will immediately cause the parameter passed in to be parsed as a string. The following code applies this logic: 


Example::

   // Print out specialties
   switch($userName)
   {
      case "Heather":
         echo("Sniper");
      case "Nikki":
         echo("Demolition");
      case Mich:
         echo("Meat shield");
      default:
         echo("Unknown user");
   }


Loops
======
As the name implies, this structure type is used to repeat logic in a loop based on an expression. The expression is usually a set of variables that increase by count, or a constant variable changed once a loop has hit a specific point. 

For Loop
^^^^^^^^^

for Loop Syntax::

   for(expression0; expression1; expression2) 
   {
      statement(s);
   }

One way to label the expressions in this syntax are (startExpression; testExpression; countExpression). Each expression is separated by a semi-colon.

Example::

   for(%count = 0; %count < 3; %count++) 
   {
      echo(%count);
   }
   
   OUTPUT:
   0
   1
   2


The first expression creates the local variable %count and initializing it to 0. In the second expression determines when to stop looping, which is when the %count is no longer less than 3. Finally, the third expression increases the count the loop relies on. 
   

While Loop
^^^^^^^^^^^
A while loop is a much simpler looping structure compared to a for loop. 

while Loop Syntax::

   while(expression) 
   {
      statements;
   }

As soon as the expression is met, the while loop will terminate:

Example::

   %countLimit = 0;
   
   while(%countLimit <= 5)
   {
      echo("Still in loop");
      %count++;
   }
   echo("Loop was terminated");

Functions
==========

Much of your TorqueScript experience will come down to calling existing functions and writing your own. Functions are a blocks of code that only execute when you call them by name. Basic functions in TorqueScript are defined as follows:: 

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

The **function** keyword, like other TorqueScript keywords, is case sensitive. You must type it exactly as shown above. The following is an example of a custom function that takes in two parameters, then executes code based on those arguments.

TorqueScript can take any number of arguments, as long as they are comma separated. If you call a function and pass fewer parameters than the function's definition specifies, the un-passed parameters will be given an empty string as their default value.

Example::

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

Console Methods
================

Console Methods are C++ functions that have been exposed to TorqueScript, which are attached to specific objects. 

Console Functions
==================

Console Functions are written in C++, then exposed to TorqueScript. These are global functions you can call at any time, and are usually very helpful or important. Throughout this document, I have been using a ConsoleFunction: echo(...). The echo function definition exists in C++:


C++ echo::

   ConsoleFunction(echo, void, 2, 0, "echo(text [, ... ])")
   {
      U32 len = 0;
      S32 i;
      for(i = 1; i < argc; i++)
         len += dStrlen(argv[i]);
   
      char *ret = Con::getReturnBuffer(len + 1);
      ret[0] = 0;
      for(i = 1; i < argc; i++)
         dStrcat(ret, argv[i]);
   
      Con::printf("%s", ret);
      ret[0] = 0;
   }


Instead of having to write that out every time, or create a TorqueScript equivalent, the ConsoleFunction macro in C++ exposes the command for you. This is much cleaner, and more convenient. We will cover all the ConsoleFunctions later. 

Objects
=========

The most complex aspect of TorqueScript involves dealing with game objects. Much of your object creation will be performed in the World Editor, but you should still know how to manipulate objects at a script level. One thing to remember is that everything in TorqueScript is an object: players, vehicles, items, etc.


Every object added in the level is saved to a mission file, which is written entirely in TorqueScript. This also means every game object is accessible from script. First, we will study the syntax of object creation. 

Syntax
^^^^^^^^

Even though objects are originally created in C++, they are exposed to script in a way that allows them to be declared using the following syntax: 

Object Definition::

   // In TorqueScript
   %objectID = new ObjectType(Name : CopySource, arg0, ..., argn) 
   {
      <datablock = DatablockIdentifier;>
      
      [existing_field0 = InitialValue0;]
      ...
      [existing_fieldN = InitialValueN;]
   
      [dynamic_field0 = InitialValue0;]
      ...
      [dynamic_fieldN = InitialValueN;]
   };

**Syntax Breakdown:**

* **%objectID** - Is the variable where the object's handle will be stored.
* **new** - Is a key word telling the engine to create an instance of the following ObjectType.
* **ObjectType** - Is any class declared in the engine or in script that has been derived from SimObject or a subclass of SimObject. SimObject-derived objects are what we were calling "game world objects" above.
* **Name** (optional) - Is any expression evaluating to a string, which will be used as the object's name.
* **CopySource** (optional) - The name of an object which is previously defined somewhere in script. Existing field values will be copied from CopySource to the new object being created. Any dynamic fields defined in CopySource will also be defined in the new object, and their values will be copied. Note: If CopySource is of a different ObjectType than the object being created, only CopySource's dynamic fields will be copied.
* **arg0, ..., argn** (optional) - Is a comma separated list of arguments to the class constructor (if it takes any).
* **datablock** - Many objects (those derived from GameBase, or children of GameBase) require datablocks to initialize specific attributes of the new object. Datablocks are discussed below.
* **existing_fieldN** - In addition to initializing values with a datablock, you may also initialize existing class members (fields) here. Note: In order to modify a member of a C++-defined class, the member must be exposed to the Console. This concept is discussed in detail later.
* **dynamic_fieldN** - Lastly, you may create new fields (which will exist only in Script) for your new object. These will show up as dynamic fields in the World Editor Inspector.

The main object variants you can create are SimObjects without a datablock, and game objects which require a datablock. The most basic SimObject can be created in a single line of code: 

Example::

   // Create a SimObject without any name, argument, or fields.
   $exampleSimObject = new SimObject();

The ``$exampleSimObject`` variable now has access to all the properties and functions of a basic SimObject. Usually, when you are creating a SimObject you will want custom fields to define features

Example::

   // Create a SimObject with a custom field
   $exampleSimObject = new SimObject() 
   {
      catchPhrase = "Hello world!";
   };

As with the previous example, the above code creates a SimObject without a name which can be referenced by the global variable $exampleSimObject. This time, we have added a user defined field called "catchPhrase." There is not a single stock Torque 3D object that has a field called "catchPhrase." However, by adding this field to the SimObject it is now stored as long as that object exists.

The other game object variant mentioned previously involves the usage of datablocks. Datablocks contain static information used by a game object with a similar purpose. Datablocks are transmitted from a server to client, which means they cannot be modified while the game is running.

We will cover datablocks in more detail later, but the following syntax shows how to create a game object using a datablock.

Example::

   // create a StaticShape using a datablock
   datablock StaticShapeData(ceiling_fan)
   {
      category = "Misc";
      shapeFile = "art/shapes/undercity/cfan.dts";
      isInvincible = true;
   };
   
   new StaticShape(CistFan) 
   {
      dataBlock = "ceiling_fan";
      position = "12.5693 35.5857 59.5747";
      rotation = "1 0 0 0";
      scale = "1 1 1";
   };

Once you have learned about datablocks, the process is quite simple: 

#. Create a datablock in script, or using the datablock editor
#. Add a shape to the scene from script or using the World Editor
#. Assign the new object a datablock

Handles vs Names
^^^^^^^^^^^^^^^^^^

Every game object added to a level can be accessed by two parameters:

* **Handle** - A unique numeric ID generated when the object is created
* **Name** - This is an optional parameter given to an object when it is created. You can assign a name to an object from the World Editor, or do so in TorqueScript using the following syntax:

Example::

   // In this example, CistFan is the name of the object
   new StaticShape(CistFan) 
   {
      dataBlock = "ceiling_fan";
      position = "12.5693 35.5857 59.5747";
      rotation = "1 0 0 0";
      scale = "1 1 1";
   };

While in the World Editor, you will not be allowed to assign the same name to multiple, separate objects. The editor will ignore the attempt. If you manually name two objects the same thing in script, the game will only load the first object and ignore the second. 

Singletons
^^^^^^^^^^^

If you need a global script object with only a single instance, you can use the singleton keyword. Singletons, in TorqueScript, are mostly used for unique shaders, materials, and other client-side only objects.

For example, SSAO (screen space ambient occlusion) is a post-processing effect. The game will only ever need a single instance of the shader, but it needs to be globally accessible on the client. The declaration of the SSAO shader in TorqueScript can be shown below::

   singleton ShaderData( SSAOShader )
   {   
      DXVertexShaderFile 	= "shaders/common/postFx/postFxV.hlsl";
      DXPixelShaderFile 	= "shaders/common/postFx/ssao/SSAO_P.hlsl";            
      pixVersion = 3.0;
   };

Object Fields
^^^^^^^^^^^^^^

Objects instantiated via script may have data members (referred to as Fields) 

Methods
^^^^^^^^

In addition to the creation of stand-alone functions, TorqueScript allows you to create and call methods attached to objects. Some of the more important ConsoleMethods are already written in C++, then exposed to script. You can call these methods by using the dot (.) notation. 

Syntax::

   objHandle.function_name();
   
   objName.function_name();

Example::

   new StaticShape(CistFan) 
   {
      dataBlock = "ceiling_fan";
      position = "12.5693 35.5857 59.5747";
      rotation = "1 0 0 0";
      scale = "1 1 1";
   };
   
   // Write all the objects methods to the console log
   CistFan.dump();
   
   // Get the ID of an object, using the object's name
   $objID = CistFan.getID();
   
   // Print the ID to the console
   echo("Object ID: ", $objID);
   
   // Get the object's position, using the object's handle
   %position = $objID.getPosition();
   
   // Print the position to the console
   echo("Object Position: ", %position);

The above example shows how you can call an object's method by using its name or a variable containing its handle (unique ID number). Additionally, TorqueScript supports the creation of methods that have no associated C++ counterpart.    

Syntax::
   
   // function - Is a keyword telling TorqueScript we are defining a new function.
   // ClassName::- Is the class type this function is supposed to work with.
   // function_name - Is the name of the function we are creating.
   // ... - Is any number of additional arguments.
   // statements - Your custom logic executed when function is called
   // %this- Is a variable that will contain the handle of the 'calling object'.
   // return val - The value the function will give back after it has completed. Optional.
   
   function Classname::func_name(%this, [arg0],...,[argn]) 
   {
      statements;
      [return val;]
   }

At a minimum, Console Methods require that you pass them an object handle. You will often see the first argument named %this. People use this as a hint, but you can name it anything you want. As with Console functions any number of additional arguments can be specified separated by commas.


As a simple example, let's say there is an object called Samurai, derived from the Player class. It is likely that a specific appearance and play style will be given to the samurai, so custom ConsoleMethods can be written. Here is a sample: 

Example::

   function Samurai::sheatheSword(%this)
   {
      echo("Katana sheathed");
   }

When you add a Samurai object to your level via the World Editor, it will be given an ID. Let's pretend the handle (ID number) is 1042. We can call its ConsoleMethod once it is defined, using the period syntax:

Example::

   1042.sheatheSword();
   
   OUTPUT: "Katana sheathed"


Notice that no parameters were passed into the function. The %this parameter is inherent, and the original function did not require any other parameters. 

Conclusion
============

This guide covered the basics of TorqueScript syntax. Compared to other languages, such as C++, it is easier to learn and work with. However, no one is expected to become a TorqueScript master over night, or even in a week. You will most likely need to refer back to this documentation several times for reminders. 

**Option 1:** Take some time to read through the **Torque 3D Script Manual**. This manual contains the most valuable information you can find about TorqueScript and Torque 3D's API. This will be your "go to" source for documentation on functions, variables, and classes that make up Torque 3D.

**Option 2:** Move on to the **Simple Tutorials** section, which will continue walking you through the basics of TorqueScript. These tutorials will provide you with sample code to read over. You will also get sample scripts at the end of each tutorial to test out.