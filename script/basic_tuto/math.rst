Math Examples
**************

Syntax Review
===============

Variable Types
-----------------
There are two types of variables you can declare and use in TorqueScript: local and global. Both are created and referenced similarly::

	%localVariable = 1;
	$globalVariable = 2;

As you can see, local variable names are preceded by the percent sign (%). Global variables are preceded by the dollar sign ($). Both types can be used in the same manner: operations, functions, equations, etc. The main difference has to do with how they are **scoped**.

In programming, scoping refers to where in memory a variable exists during its life. A local variable is meant to only exist in specific blocks of code, and its value is discarded when you leave that block. Global variables are meant to exist and hold their value during your entire programs execution. 

Operators
-----------

**Arithmetic Operators**

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

**Assignment and Assignment Operators**

========  ====================  ==============  ===========
Operator  Name                  Example         Explanation
========  ====================  ==============  ===========
``=``     Assignment            ``$a = $b;``    Assign value of ``$b`` to ``$a``
                                                **Note:**  the value of an assignment is the value being assigned, so $a = $b = $c is legal.
``op=``   Assignment Operators  ``$a op= $b;``  Equivalent to ``$a = $a op $b``, where op can be any of:  * / % + - & | ^ << >>
												**For example:** ``$a *= $b;`` is the same as ``$a = $a * $b;`` 
========  ====================  ==============  ===========

Creating the Script
=====================

First, we need to create a new script:

#. Navigate to your project's **game/scripts/client** directory.
#. Create a new script file called "maths". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs.
#. Open your new script using a text editor or Torsion.


Before writing any actual script code, we should go ahead and tell the game it should load the script. Open **game/scripts/client/init.cs**. Scroll down to the **initClient** function. Under the // Client scripts section, add the following:


**Execute our new script**::

	exec("./maths.cs");


Standard arithmetic operators are the easiest to script. Start by adding this function to your new script::

	// Print the sum of %a and %b
	function addValues(%a, %b)
	{ 
	   %sum = %a + %b;
	   
	   echo("Sum of " @ %a @ " + " @ %b @ ": ", %sum);
	}


This simple function takes in two numerical arguments. A new variable, %sum, holds the result of adding the two arguments together. Finally, an echo(...) statement is formatted to print the original values (%a and %b) and the sum (%sum of the two).

To test your new script:

#. Save the script
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, pressing enter after each line::

	addValues(1,1);
	addValues(2,3);
	addValues(-3,2);
	

Your console output should look like this::

	Sum of 1 + 1: 2
	Sum of 2 + 3: 5
	Sum of -3 + 2: -1
	
As you can see, you can use positive or negative numbers. You can also use floating point (decimal) values if you wish. Add the following script code to test the other basic arithmetic operations::

	// Print the difference between %a and %b
	function subtractValues(%a, %b)
	{
	   %difference = %a - %b;
	   
	   echo("Difference between " @ %a @ " - " @ %b @ ": ", %difference);
	}
	
	// Print the product of %a and %b
	function multiplyValues(%a, %b)
	{
	   %product = %a * %b;
	   
	   echo("Product of " @ %a @ " * " @ %b @ ": ", %product);
	}
	
	// Print the quotient of %a and %b
	function divideValues(%a, %b)
	{
	   %quotient = %a / %b;
	   
	   echo("Quotient of " @ %a @ " / " @ %b @ ": ", %quotient);
	}
	
	// Print remainder of %a divided by %b
	function moduloValue(%a, %b)
	{
	   %remainder = %a % %b;
	   
	   echo("Remainder of " @ %a @ " % " @ %b @ ": ", %remainder);
	}


You will use the same process of scripting, saving, running the game, and calling the functions via the console that has been previously discussed above. Another way of manipulating values involves more complex operators. Standard additions, subtraction, etc, use two operators: assignment (=) and arithmetic (+,-,*,etc).

You can increase or decrease the value of a variable by using the auto-increment and auto-decrement operators. As soon as the operation completes, the variable is permanently changed. You do not need to use an assignment operator in this case. Use the following script code to test it out::

	// Print the increment of %a
	function incrementValue(%a)
	{
	   %original = %a;
	   %a++;
	   
	   echo("Single increment of " @ %original @ ": ", %a);
	}
	
	// Print the decrement of %a
	function decrementValue(%a)
	{
	   %original = %a;
	   %a--;
	   
	   echo("Single decrement of " @ %original @ ": ", %a);
	}


As you can see, the original value of %a had to be stored before the increment/decrement operation was applied. The ++ and -- automatically adjust the variable for you. Another non-basic manipulation involves combining the assignment operator with an arithmetic operator::

	// Print the result of a+=b
	function addToValue(%a, %b)
	{
	   %original = %a;
	   %a += %b;
	   
	   echo("Sum of " @ %original @ " += " @ %b @ ": ", %a);
	}

In the above example, the + and = are combined together for a single operation. In simple terms, %a += %b can be verbalized as "A equals itself plus B." Unlike the addValue(...) function written earlier, a third variable is not used in this equation. This operation can be applied to the other arithmetic operators.

The last topic we will cover in this guide is comparison operators. As the name implies, these operators will compare two values together and produce a boolean (1 or 0) based on the results. Add the following function to see the first example::

	// Compare %a to %b, then print the relation
	function compareValues(%a, %b)
	{
	   if(%a > %b)
	      echo("A is greater than B");
	}


The above code is very straight forward. The values of %a and %b are compared to each other to see which is higher. Test the comparison code in the console using the following::

	compareValues(2,1);
	compareValues(3,2);
	compareValues(1,2);
	compareValues(0,0);

The output should be the following::

	A is greater than B
	A is greater than B
	<no output>
	<no output>


The first two calls will prove the comparison as "true", and print out the message. The comparison results to false on the last two calls, so nothing will be printed. The rest of the function showing off the comparison operators can be copied over what you currently have::

	// Compare %a to %b, then print the relation
	function compareValues(%a, %b)
	{
	   // Printing symbols just as a decorator
	   // Makes it easier to isolate the print out
	   echo("\n====================================");
	   
	   // Print out the value of %a and %b
	   echo("\nValue of A: ", %a);
	   echo("Value of B: ", %b);
	   
	   if(!%a)
	      echo("\nA is a zero value\n");
	   else
	      echo("\nA is a non-zero value\n");
	      
	   if(!%b)
	      echo("B is a zero value\n");
	   else
	      echo("B is a non-zero value\n");
	   
	   if(%a && %b)
	      echo("Both A and B are non-zero values\n");
	   
	   if(%a || %b)
	      echo("Either A or B is a non-zero value\n");
	      
	   if(%a == %b)
	      echo("A is exactly equal to B\n");
	   
	   if(%a != %b)
	      echo("A is not equal to B\n");
	   
	   if(%a < %b)
	      echo("A is less than B");
	   else if(%a <= %b)
	      echo("A is less than or equal to B");
	   
	   if(%a > %b)
	      echo("A is greater than B");
	   else if(%a >= %b)
	      echo("A is greater than or equal to B");
	 
	   // Printing symbols just as a decorator
	   // Makes it easier to isolate the print out  
	   echo("\n====================================");
	}


I have added "decorator text" to help separate console output and make the output easier to read. Notice that each operation uses an if(...) statement to compare. Remember, the if(...) code is based on checking for a 1 (true) or 0 (false) value. This is all a comparison operation will return. 

Conclusion
===========
The guide covers the basic arithmetic operators you will use in TorqueScript. For now, read back over the script code you have been provided with. Study the comments and echo(...) commands, and feel free to test out new operators.

You can download the entire script from this lesson HERE. Save the script as you would any other text file from a website::

	//-----------------------------------------------------------------------------
	// Torque 3D
	// Copyright (C) GarageGames, LLC 2011 All Rights Reserved
	//-----------------------------------------------------------------------------
	
	// Print the sum of %a and %b
	function addValues(%a, %b)
	{ 
	   %sum = %a + %b;
	   
	   echo("Sum of " @ %a @ " + " @ %b @ ": ", %sum);
	}
	
	// Print the difference between %a and %b
	function subtractValues(%a, %b)
	{
	   %difference = %a - %b;
	   
	   echo("Difference between " @ %a @ " - " @ %b @ ": ", %difference);
	}
	
	// Print the product of %a and %b
	function multiplyValues(%a, %b)
	{
	   %product = %a * %b;
	   
	   echo("Product of " @ %a @ " * " @ %b @ ": ", %product);
	}
	
	// Print the quotient of %a and %b
	function divideValues(%a, %b)
	{
	   %quotient = %a / %b;
	   
	   echo("Quotient of " @ %a @ " / " @ %b @ ": ", %quotient);
	}
	
	// Print remainder of %a divided by %b
	function moduloValue(%a, %b)
	{
	   %remainder = %a % %b;
	   
	   echo("Remainder of " @ %a @ " % " @ %b @ ": ", %remainder);
	}
	
	// Print the increment of %a
	function incrementValue(%a)
	{
	   %original = %a;
	   %a++;
	   
	   echo("Single increment of " @ %original @ ": ", %a);
	}
	
	// Print the decrement of %a
	function decrementValue(%a)
	{
	   %original = %a;
	   %a--;
	   
	   echo("Single decrement of " @ %original @ ": ", %a);
	}
	
	// Print the result of a+=b
	function addToValue(%a, %b)
	{
	   %original = %a;
	   %a += %b;
	   
	   echo("Sum of " @ %original @ " += " @ %b @ ": ", %a);
	}
	
	// Compare %a to %b, then print the relation
	function compareValues(%a, %b)
	{
	   // Printing symbols just as a decorator
	   // Makes it easier to isolate the print out
	   echo("\n====================================");
	   
	   // Print out the value of %a and %b
	   echo("\nValue of A: ", %a);
	   echo("Value of B: ", %b);
	   
	   if(!%a)
	      echo("\nA is a zero value\n");
	   else
	      echo("\nA is a non-zero value\n");
	      
	   if(!%b)
	      echo("B is a zero value\n");
	   else
	      echo("B is a non-zero value\n");
	   
	   if(%a && %b)
	      echo("Both A and B are non-zero values\n");
	   
	   if(%a || %b)
	      echo("Either A or B is a non-zero value\n");
	      
	   if(%a == %b)
	      echo("A is exactly equal to B\n");
	   
	   if(%a != %b)
	      echo("A is not equal to B\n");
	   
	   if(%a < %b)
	      echo("A is less than B");
	   else if(%a <= %b)
	      echo("A is less than or equal to B");
	   
	   if(%a > %b)
	      echo("A is greater than B");
	   else if(%a >= %b)
	      echo("A is greater than or equal to B");
	 
	   // Printing symbols just as a decorator
	   // Makes it easier to isolate the print out  
	   echo("\n====================================");
	}
	
	
	function compareStrings(%string1, %string2)
	{
	   // Print out the values of %string1 and %string2
	   echo("\nValue of String 1: ", %string1);
	   echo("Value of String 2: ", %string2);
	   
	   if(%string1 $= %string2)
	   {
	      echo("\nString 1 and String 2 contain identical text");   
	   }
	   
	   if(%string1 !$= %string2)
	   {
	      echo("\nString 1 and String 2 contain different text");   
	   }
	}
