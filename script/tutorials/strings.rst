String Manipulation
===================

Text, such as names or phrases, are supported as strings. Numbers can also be stored in string format. Standard strings are stored in double-quotes::

	"abcd"    (string)

Example::

	$UserName = "Heather";

Strings with single quotes are called "tagged strings."::

	'abcd'  (tagged string)

Tagged strings are special in that they contain string data, but also have a special numeric tag associated with them. Tagged strings are used for sending string data across a network. The value of a tagged string is only sent once, regardless of how many times you actually do the sending.

On subsequent sends, only the tag value is sent. Tagged values must be de-tagged when printing. You will not need to use a tagged string often unless you are in need of sending strings across a network often, like a chat system.

There are special values you can use to concatenate strings and variables. Concatenation refers to the joining of multiple values into a single variable. The following is the basic syntax::

	"string 1" operation "string 2"

You can use string operators similarly to how you use mathematical operators (=, +, -, \*). You have four operators at your disposal::

	@      (concatenates two strings)
	TAB    (concatenation with tab)
	SPC    (concatenation with space)
	NL     (newline)

Creating the Script
-------------------

First, we need to create a new script:

#. Navigate to your project's game/scripts/client directory.
#. Create a new script file called "stringManip". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs.
#. Open your new script using a text editor or Torsion.

Before writing any actual script code, we should go ahead and tell the game it should load the script. Open game/scripts/client/init.cs. Scroll down to the initClient function. Under the // Client scripts section, add the following:

Execute our new script::

	exec("./stringManip.cs");

In the new script, define three global variables at the very top as shown in the following code::

	$PlayerName = "Player";
	$GameName = "Default";
	$BattleCry = "Hello World";

These are the strings that will be manipulated in this script. To test one of the variables, write the following function::

	// Print player name string
	function printPlayerName()
	{
	   echo($PlayerName);
	}

The printPlayerName() function simply prints out the string value held by $PlayerName to the console. To test your new script:

#. Save the script
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, and press enter::

	printPlayerName();

The output is extremely basic. All you will see is the string held by the variable. We can perform some string manipulation to print out something more descriptive. Change the function code to the following::

	// Print player name string
	function printPlayerName()
	{
	   // Concatenate "Player's Name" with the variable
	   // Containing the name
	   echo("Player's Name: " @ $PlayerName);
	}

Now, when you call the function you will see the following output::

	Player's Name: Default

This kind of string formatting and manipulation will make debugging and management a lot easier. Add the following code to achieve the same affect for the $GameName variable::

	// Print game name string
	function printGameName()
	{
	   // Concatenate "Game Name" with the variable
	   // Containing the name
	   echo("Game Name: " @ $GameName);
	}

We will do something slightly different with the battle cry. You can store the result of a string manipulation in a variable before you use it. This will come in handy for saving permanent changes for strings and numbers. Use the following code to create a new function::

	// Print battle cry string
	function printBattleCry()
	{
	   // Concatenate the string in $PlayerName
	   // with the static string yelled: "
	   %message = $PlayerName @ " yelled: \"";

	   // Concatenate the value of %message with
	   // the string in $BattleCry and the " symbol
	   // Store the results in the %message variable
	   %message = %message @ $BattleCry @ "\"";
	   
	   // Print the new string after it
	   // has been manipulated
	   echo(%message);
	}

The printBattleCry() function starts by defining a new local variable (%message) and assigning it the value of the $PlayerName concatenated with a static string. The second line concatenates the new %message variable with the contents of $BattleCry, and wraps the quotation mark around the actual phrase. In the same line, the %message variable is replaced with itself + the concatenated string.

Let's go ahead and create a function to print all of the variables out with a little decoration. Add the following to your script::

	// Print all the game strings using a single function
	function printGameStrings()
	{
	   echo("\n***********************************");
	   echo("*         GAME STATS              *");
	   echo("***********************************\n");
	   
	   echo("Game Name: " @ $GameName);
	   echo("Player's Name: " @ $PlayerName);
	   echo($PlayerName @ " battle cry: \"" @ $BattleCry @ "\"");
	}

When you call this function in the console, you will get the following output::

	***********************************
	*         GAME STATS              *
	***********************************

	Game Name: Default
	Player's Name: Player
	Player battle cry: "Hello World"

So far we have been concatenating and printing out strings. You can also assign string values using the assignment operator (=), and compare string values using the string equality operator ($=).

The following function uses the operators to adjust the game string variables::

	// Set game strings with other strings
	// %playerName will be assigned to $PlayerName
	// %gameName will be assigned to $GameName
	// %battleCry will be assigned to $BattleCry
	function setGameStrings(%playerName, %gameName, %battleCry)
	{
	   // Check to see if the two strings are identical
	   // If so, do nothing and print a message.
	   // Otherwise, assign the new string
	   if($PlayerName $= %playerName)
	      echo("New player name is identical. Doing nothing");
	   else
	      $PlayerName = %playerName;
	}

The above function takes in three variables containing strings, one of which is used initially. The first if(...) check compares $PlayerName to %playerName. If the two are identical, the assignment of a new value will not occur. A message will be printed to console instead.

You can also apply the logical NOT (!) operator to a comparison to achieve the opposite test::

   // Check to see if the two strings are different
   // If so, assign the new string
   // Otherwise, do nothing and print a message.
   if($GameName !$= %gameName)
      $GameName = %gameName;
   else   
      echo("Game name is identical. Doing nothing");

In this check, if the two strings are NOT the same, then the new value assignment will occur. Otherwise, a message is printed to the console. You can go ahead and add the last portion of the code handling the %battleCry assignment::

	// Check to see if the two strings are identical
	// If so, do nothing and print a message.
	// Otherwise, assign the new string   
	if($BattleCry $= %battleCry)
	  echo("Battle cry is identical. Doing nothing");
	else
	  $BattleCry = %battleCry;

Conclusion
----------

This guide covered the most popular operators used for string manipulation: concatenate (@), assignment (=), string equality ($=), and string inequality (!$=). Outside of simply printing to the console, during development you will be manipulating strings that directly affect game play, interface messages, and the saving of important data.
