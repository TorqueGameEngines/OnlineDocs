Control Structures
==================

TorqueScript provides basic branching structures that will be familiar to programmers that have used other languages. If you are completely new to programming, you use branching structures to control your game's flow and logic. This section builds on everything you have learned about TorqueScript so far.

if, else
--------

This type of structure is used to test a condition, then perform certain actions if the condition passes or fails. You do not always have to use the full structure, but the following syntax shows the extent of the conditional::

	if(<boolean expression>) 
	{
	   pass logic
	}
	else 
	{
	   alternative logic
	}

Remember how boolean values work? Essentially, a bool can either be true (1) or false (0). The condition (boolean) is always typed into the parenthesis after the "if" syntax. Your logic will be typed within the brackets ``{}``. The following example uses specific variable names and conditions to show how this can be used::

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

Brackets for single line statements are optional. If you are thinking about adding additional logic to the code, then you should use the brackets anyway. If you know you will only use one logic statement, you can use the following syntax::

	// Global variable that controls lighting
	$lightsShouldBeOn = true;

	// Check to see if lights should be on or off
	if($lightsShouldBeOn)
	  turnOnLights();   // True. Call turn on lights function
	else
	  turnOffLights(); // False. Turn off the lights

switch, switch$
---------------

If your code is using several cascading if-then-else statements based on a single value, you might want to use a switch statement instead. Switch statements are easier to manage and read. There are two types of switch statements, based on data type: numeric (``switch``) and string (``switch$``)::

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

As the above code demonstrates, start by declaring the switch statement by passing in a value to the ``switch(...)`` line. Inside of the brackets ``{}``, you will list out all the possible cases that will execute based on what value being tested. It is wise to always use the default case, anticipating rogue values being passed in::

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

``switch`` only properly evaluates numerical values. If you need a switch statement to handle a string value, you will want to use ``switch$``. The ``switch$`` syntax is similar to what you just learned::

	switch$ (<string expression>)
	{
	   case "string value 0":
	                statements;
	   case "string value 1":
	                statements;
	   case "string value N":
	                statements;
	   default:
	                statements;
	}

Appending the $ sign to switch will immediately cause the parameter passed in to be parsed as a string. The following code applies this logic::

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

for
---

As the name implies, this structure type is used to repeat logic in a loop based on an expression. The expression is usually a set of variables that increase by count, or a constant variable changed once a loop has hit a specific point::

	for(expression0; expression1; expression2) 
	{
	    statement(s);
	}

One way to label the expressions in this syntax are (startExpression; testExpression; countExpression). Each expression is separated by a semi-colon::

	for(%count = 0; %count < 3; %count++) 
	{
	    echo(%count);
	}

	OUTPUT:
	0
	1
	2

The first expression creates the local variable ``%count`` and initializing it to 0. In the second expression determines when to stop looping, which is when the ``%count`` is no longer less than 3. Finally, the third expression increases the count the loop relies on.

foreach
-------

Simplify the iteration over sets of objects and string vectors. To loop over each object in a SimSet, use the foreach statement::

	foreach( %obj in %set )
	   /* do something with %obj */;

To loop over each element in a string vector, use the foreach$ statement::

	foreach$( %str in "a b c" )
	   /* do something with %str */;

while
-----

A while loop is a much simpler looping structure compared to a for loop.

::

	while(expression) 
	{
	    statements;
	}

As soon as the expression is met, the while loop will terminate::

	%countLimit = 0;

	while(%countLimit <= 5)
	{
	   echo("Still in loop");
	   %count++;
	}

	echo("Loop was terminated");

