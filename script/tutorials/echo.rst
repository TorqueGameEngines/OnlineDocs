Echo
====

Start by running a Torque 3D project. Once the game is up, open the console by pressing the tilde (~) key. In the console, type the following::

	echo("Hello World");

	OUTPUT: Hello World

Now, let's make use of the second parameter. Passing in a value for the second argument will append it to your text::

	echo("Hello World", 3);

	OUTPUT: Hello World3

Notice how there is no space between World and 3. The optional text is appended exactly how you type it. If you want, you can include your own white space to format the output::

	echo("Hello World: ", 5);

	OUTPUT: Hello World: 5

As you can see, the colon and space are included in the output. 5 is still appended, but does not ignore the whitespace. In addition to echo(...), there are two other output functions you will find useful. Their syntax and functionality are nearly identical to echo, but the output is different.

The two functions I'm referring to are warn(...) and error(...). You can post a message in the console and log the same way you echo::

	warn("Be careful. Something bad might happen");

	error("Something has gone horribly wrong");

	OUTPUT: 
	Be careful. Something bad might happen (teal color)
	Something has gone horribly wrong (red color)

You can use these functions to output multicolored text to the console, which will help you identify problems with your scripts.

Creating the Script
-------------------

There is no real reason to have a script full of echo statements. You will want to use echo(...) while debugging your other functions. However, as an example, you can create a script consisting only of output statements.

First, we need to create a new script:

#. Navigate to your project's game/scripts/client directory.
#. Create a new script file called "Output.cs". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs
#. Open your new script using a text editor or Torsion.

Add the following code to the script::

	//-----------------------------------------------------------------------------
	// Torque 3D
	// Copyright (C) GarageGames.com 2000 - 2009 All Rights Reserved
	//-----------------------------------------------------------------------------

	// Create a nice border effect around these echos, makes it easier to find
	echo("************************************************************");
	echo("************************************************************");

	// Standard use
	echo("Hello");
	echo("World");
	echo("Hello World");

	// With escape commands
	echo("H\ne\nl\nl\no\nW\no\nr\nl\nd\n");

	// Appending
	echo("Hello World", 1);
	echo("Hello World ", 2);
	echo("Hello World: ", 3);

	// Warning
	warn("Warning! Watch for teal text");

	// Error
	error("Something has gone horribly wrong");
	echo("************************************************************");
	echo("************************************************************");

Save the script now.

Testing the Script
------------------

Open game/scripts/client/init.cs and locate the initClient() function. At the end of that function, execute your new script by typing the following::

	exec("./Output.cs");

Run your game, then open the console by pressing tilde (~). Look for the long string of asterisks (*****), and you will find your echo statements. Note: you may need to scroll up to find the echo statements.
