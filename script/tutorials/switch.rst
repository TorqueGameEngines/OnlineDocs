Switch Statements
=================

There are two types of switch statements used in TorqueScript. switch(...) is used to compare numerical values and switch$(...) is used to compare strings.

Standard switch statements use numerical values to determine which case to execute.

switch Syntax::

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

Switch statements requiring string comparison use the switch$ syntax.

switch$ Syntax::

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

Creating the Script
-------------------

First, we need to create a new script:

#. Navigate to your project's game/scripts/client directory.
#. Create a new script file called "switch". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs.
#. Open your new script using a text editor or Torsion.

Before writing any actual script code, we should go ahead and tell the game it should load the script. Open game/scripts/client/init.cs. Scroll down to the initClient function. Under the // Client scripts section, add the following:

Execute our new script::

	exec("./switch.cs");

The first function we are going to write will take in a numerical argument. This number will be checked for a specific value, and a message will be printed based on the value comparison. Create the following function in your script::

	// Print a message to a console based on
	// the amount of ammo a weapon has
	// %ammoCount - Ammo count (obviously)
	function checkAmmoCount(%ammoCount)
	{
	   // If the ammo is at 0, we are out of ammo
	   // If the ammo is at 1, we are at the end of the clip
	   // If the ammo is at 100, we have a full clip
	   // If the ammo is anything else, we do not care
	   if(%ammoCount == 0)
	      echo("Out of ammo, time to reload");
	   else if(%ammoCount == 1)
	      echo("Almost out of ammo, warn user");
	   else if(%ammoCount == 100)
	      echo("Full ammo count");
	   else
	      echo("Doing nothing");
	}

To test your new script:

#. Save the script
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, press enter after each line::

	checkAmmoCount(0);
	checkAmmoCount(1);
	checkAmmoCount(100);
	checkAmmoCount(44);

Your console output should be the following::

	Out of ammo, time to reload

	Almost out of ammo, warn user

	Full ammo count

	Do nothing

Instead of using four separate if/else checks, we can use a single switch statement to handle all of the cases. Change the checkAmmoCount(...) function to use the following code::

	// Print a message to a console based on
	// the amount of ammo a weapon has
	// %ammoCount - Ammo count (obviously)
	function checkAmmoCount(%ammoCount)
	{
	   // If the ammo is at 0, we are out of ammo
	   // If the ammo is at 1, we are at the end of the clip
	   // If the ammo is at 100, we have a full clip
	   // If the ammo is anything else, we do not care
	   switch(%ammoCount)
	   {
	      case 0:
	         echo("Out of ammo, time to reload");
	      case 1:
	         echo("Almost out of ammo, warn user");
	      case 100:
	         echo("Full ammo count");
	      default:
	         echo("Doing nothing");
	   }
	}
                
The switch is declared using the switch(%ammoCount){...} syntax. The test value is kept in the parenthesis, and the cases are defined in the brackets. Each case you wish to check for is defined by the keyword case, the value, and a colon (case: 0).

You can write as few or as many lines of TorqueScript code between cases as you need to handle each numerical value. The default keyword is used when you want to handle a value that does not have a defined case. Without the default case, any other value besides was is defined as a case will be ignored.

If you test the function as you did previously, you should get the same result::

	checkAmmoCount(0);
	checkAmmoCount(1);
	checkAmmoCount(100);
	checkAmmoCount(44);

Result::

	Out of ammo, time to reload

	Almost out of ammo, warn user

	Full ammo count

	Do nothing

Testing strings in switch statements requires a small syntactical change. There are multiple ways to perform a string comparison. Write the following function in your script::

	// Check to see if a person's name is 
	// a known user
	// %userName - String containing person's name
	function matchNames(%userName)
	{
	   if(!strcmp(%userName, "Heather"))
	      echo("User Found: " @ %userName);
	   else if(%userName $= "Mich")
	      echo("User Found: " @ %userName);
	   else if(%userName $= "Nikki")
	      echo("User Found: " @ %userName);
	   else 
	      echo("User " @ %userName @ " not found");
	}

The above code defines a function which takes in a string as an argument, then performs three separate string comparison to find a result. The first if(...) check uses the strcmp function to check the %userName variable against a static string ("Heather").

The two other checks use the basic $= string equality operator. Finally, an else statement exists to inform the system that no user was found. Run the script and type the following to test the function::

	matchNames("Heather");
	matchNames("Mich");
	matchNames("Nikki");
	matchNames("Brad");

Output::

	User Found: Heather
	User Found: Mich
	User Found: Nikki
	User Brad not found

Instead of four separate if/else string comparison statements, a single switch can clean the code up greatly. Replace the matchNames(...) function with the following::

	// Check to see if a person's name is 
	// a known user
	// %userName - String containing person's name
	function matchNames(%userName)
	{
	   switch$(%userName)
	   {
	      case "Heather":
	         echo("User Found: " @ %userName);
	      case "Mich":
	         echo("User Found: " @ %userName);
	      case "Nikki":
	         echo("User Found: " @ %userName);
	      default:
	         echo("User: " @ %userName @ " not found");
	   }
	}

Just like the switch statement used in the checkAmmoCount(...) function, the above code starts with the switch$ keyword. This is followed by the string we are testing, held in the parenthesis. Instead of numerical values, the case keywords are followed by a strings.

In the above example, the case statements are comparing the test (%userName) against string literals. String literals are raw text displayed in code between quotations. If you have variables that contain a string value to test against, you can use those instead.

As with a numerical switch statement, you can write your logic in between the case statements.

Conclusion
----------

This guide covered the basics of the switch and switch$ statement structures. When you need to perform one or two logical checks, you will use the basic control statements such as if(...), if else(...), and else. When you need a complex control statement handling multiple outcomes based on a value, try using a switch statement instead.
