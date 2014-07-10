Array Manipulation
==================

Arrays are data structures used to store consecutive values of the same data type. Arrays can be single-dimension or multidimensional::

	$TestArray[n]   (Single-dimension)
	$TestArray[m,n] (Multidimensional)
	$TestArray[m_n] (Multidimensional)

If you have a list of similar variables you wish to store together, try using an array to save time and create cleaner code. The syntax displayed above uses the letters 'n' and 'm' to represent where you will input the number of elements in an array. The following example shows code that could benefit from an array::

	$userNames[0] = "Heather";
	$userNames[1] = "Nikki";
	$userNames[2] = "Mich";

	echo($userNames[0]);
	echo($userNames[1]);
	echo($userNames[2]);

Creating the Script
-------------------

First, we need to create a new script:

#. Navigate to your project's game/scripts/client directory.
#. Create a new script file called "arrays". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs.
#. Open your new script using a text editor or Torsion.

Before writing any actual script code, we should go ahead and tell the game it should load the script. Open game/scripts/client/init.cs. Scroll down to the initClient function. Under the // Client scripts section, add the following:

Execute our new script::

	exec("./arrays.cs");

This new script is going to work with two different arrays: $names and $board. $names is a single dimensional array containing strings. $board is a two dimensional array, also containing strings. The two are not related, but show off different uses of arrays. Let's create the initialization function::

	// Set up all of the arrays 
	// with default values
	function initArrays()
	{
	   // Initialize single dimensional array
	   // containing a list of names
	   $names[0] = "Heather";
	   $names[1] = "Nikki";
	   $names[2] = "Mich";
	   
	   // Initialize two dimensional array
	   // containing symbols for a 
	   // tic-tac-toe game
	   
	   // Row one values   
	   $board[0,0] = "_";
	   $board[0,1] = "_";
	   $board[0,2] = "_";
	   
	   // Row two values
	   $board[1,0] = "_";
	   $board[1,1] = "_";
	   $board[1,2] = "_";
	   
	   // Row three values
	   $board[2,0] = "_";
	   $board[2,1] = "_";
	   $board[2,2] = "_";
	}

The above code defines the two arrays ($names and $board). $names is given three strings representing people's names. $board is setup like a tic-tac-toe board. It will be making use of "X"s and "O"s, but for now the blank value is "_".

Instead of manually calling this function every time the game is run, we can call the function on game initialization. Open game/scripts/client/init.cs. Scroll down to the initClient function. Under this code::

	exec("./arrays.cs");

Add the following::

	initArrays();

Save the arrays.cs and init.cs scripts. Since there is nothing to see yet, create a function that will print out the values of $names::

	// Print out all the values 
	// in the $names array
	function printNames()
	{
	   // Print each name using 
	   // hard coded values (0,1,2)
	   echo("0:" @ $names[0]);
	   echo("1:" @ $names[1]);
	   echo("2:" @ $names[2]);
	}

To test your new script:

#. Save the script
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, and press enter::

	printNames();

The output is extremely basic. All you will see is the strings held by the array, by index::

	0: Heather
	1: Nikki
	2: Mich

This is a good start, but what if the array has 1000 elements? An optimization for this function would be to make use of a looping structure. Modify the printNames() function to use the following code::

	function printNames()
	{   
	   // Iterate through the names
	   // array and print the values
	   for(%i = 0; %i < 3; %i++)
	      echo(%i @ ": " @ $names[%i]);
	}

Instead of having three (or 1000) echo statements, you only have to script two lines. The above code iterates through the elements of the $names array using a for(...) loop. To change an individual element, add the following function to your script::

	// Change the value of an array item
	// %id = index to change
	// %name = the new value
	function setNames(%id, %name)
	{
	   // Our array only contains three elements:
	   // [0] [1] [2]
	   // If anything other than 0, 1, or 2 is
	   // passed in, inform the user of an error
	   if(%id > 2 || %id < 0)
	   {
	      error("Index " @ %id @ " out of range");
	      error("Please use 0 - 2 as the %id");
	   }
	   else
	      $names[%id] = %name;
	}

To use this function, run the game and open the console. The first variable determines which array index is changing, and the second variable is the new string (name) to use. Example usage::

	setNames(0, "Brad");

If you try to pass in any other numbers besides 0, 1, or 2, you will get an error message letting you know you have tried to access outside of the array bounds. Moving on, the script needs functions for printing, manipulating, and testing the $board array.

To print out just the values in order, add the following function::

	// Print out the the values
	// in the $board array
	function printBoardValues()
	{
	   // %i loops through rows
	   for(%i = 0; %i < 3; %i++)
	   {
	      // %j loops through columns
	      for(%j = 0; %j < 3; %j++)
	      {
	         // Print the value of the [%i,%j]
	         echo("[" @ %i @ "," @ %j @ "]: " @ $board[%i, %j]);
	      }
	   }
	}

The above code uses the concept of nested loops. Nested loops are simply loops within other loops. Notice there are two for(...) structures set up. This allows the iteration of each row and column, which is necessary with a two-dimensional array. Calling this function will result in the following output::

	[0,0]: _
	[0,1]: _
	[0,2]: _
	[1,0]: _
	[1,1]: _
	[1,2]: _
	[2,0]: _
	[2,1]: _
	[2,2]: _

As you can see, the function prints the current index and the value it contains. Being a tic-tac-toe board, it might help to visualize the board based on value locations. The following function will print the values of $board in a relative format::

	// Print tic-tac-toe board
	// in a relative format
	function printBoard()
	{
	   // Print out an entre row in 1 echo
	   echo($board[0,0] @" "@ $board[0,1] @" "@ $board[0,2]);
	   echo($board[1,0] @" "@ $board[1,1] @" "@ $board[1,2]);
	   echo($board[2,0] @" "@ $board[2,1] @" "@ $board[2,2]);
	}

The initial output without changing the values will look like this::

	_ _ _
	_ _ _
	_ _ _

If you have never played tic-tac-toe, each player takes a turn putting an X or O in one of the board positions. When three X's or O's are lined up, a player wins. The alignment can be three in a row, three in a column, or three diagonally. We can simulate this game play, but we will only work with rows.

We are going to change this function a few times, but we will start with the shell::

	// Set a specific value in the array
	// to an X or O
	function setBoardValue(%row, %column, %value)
	{
	   // Make sure "X" or "O" was passed in
	   if(%value !$= "X" && %value !$= "O")
	   {
	      echo("Invalid entry:\nPlease use \'X\' or \'O\'");
	      return;
	   }
	}

The user will input a row index (%row), a column index (%column), and a value (%value) represented by an "X" or "O" string. If anything other than a capital X or capital O are passed in, the function will throw an error message and exit. If the function gets past the check, the value is assigned::

	// Set a specific value in the array
	// to an X or O
	function setBoardValue(%row, %column, %value)
	{
	   // Make sure "X" or "O" was passed in
	   if(%value !$= "X" && %value !$= "O")
	   {
	      echo("Invalid entry:\nPlease use \'X\' or \'O\'");
	      return;
	   }
	   
	   // Set the board value
	   $board[%row, %column] = %value;
	}

Save the script and run. Call the following functions, in order, to see the results::

	printBoard();
	setBoardValue(0,0,"X");
	setBoardValue(0,1,"O");
	printBoard();

Your output should look like the following::

	_ _ _
	_ _ _
	_ _ _

	X O _
	_ _ _
	_ _ _

To reset back to the default values, you can create a function that iterates through the array::

	// Set all values of $board
	// array back to "nothing"
	// In this case, nothing is _
	function resetBoard()
	{
	   // %i loops through rows
	   for(%i = 0; %i < 3; %i++)
	   {
	      // %j loops through columns
	      for(%j = 0; %j < 3; %j++)
	      {
	         // Set value to _
	         $board[%i, %j] = "_";
	      }
	   }
	}

Now, any normal game will have a victory condition. Enable to win, a row must contain three of the same value. Creating a function for this is quite simple using array access and string comparisons::

	// Compare the values of each array
	// item in a row
	// If row contains the same values
	// Return true for a victory
	// Return false if values are different
	function checkForWin()
	{
	   // Make sure at least the first symbol is X or O
	   // Then compare the three values of a row

	   // Row 1
	   if($board[0,0] !$= "_" && $board[0,0] $= $board[0,1] && $board[0,1] $= $board[0,2])
	      return true;

	   // Row 2      
	   if($board[1,0] !$= "_" && $board[1,0] $= $board[1,1] && $board[1,1] $= $board[1,2])
	      return true;

	   // Row 3      
	   if($board[2,0] !$= "_" && $board[2,0] $= $board[2,1] && $board[2,1] $= $board[2,2])
	      return true;
	      
	   return false;
	}

The checkForWin() function will return true if any of the three if(...) statements pass. If there is no win condition, the function will return false. In a previous guide, you learned about the $= operator. Alternatively, you can use a function to compare two strings: strcmp(...).

The strcmp(...) function takes in two string, compares the two, then return a 1 or 0 based on the comparison. If the two strings are the same, it will return a 0. If the two strings are different, it will return a 1.

Example::

	%string1 = "Hello";
	%string2 = "Hello";
	%string3 = "World";

	// Returns 0
	strcmp(%string1, %string2);

	// Returns 1
	strcmp(%string1, %string3);

We can replace the $= operators in the checkForWin() function using a different set of operators. Comment out the first chunk of code, and replace it with the following::

	function checkForWin()
	{
	   // Make sure at least the first symbol is X or O
	   // Then compare the three values of a row
	   //if($board[0,0] !$= "_" && $board[0,0] $= $board[0,1] && $board[0,1] $= $board[0,2])
	      //return true;
	      //
	   //if($board[1,0] !$= "_" && $board[1,0] $= $board[1,1] && $board[1,1] $= $board[1,2])
	      //return true;
	      //
	   //if($board[2,0] !$= "_" && $board[2,0] $= $board[2,1] && $board[2,1] $= $board[2,2])
	      //return true;
	   
	   if($board[0,0] !$= "_" && !strcmp($board[0,0], $board[0,1]) && !strcmp($board[0,1], $board[0,2]))
	      return true;
	   
	   if($board[0,0] !$= "_" && !strcmp($board[1,0], $board[1,1]) && !strcmp($board[1,1], $board[1,2]))
	      return true;
	      
	   if($board[0,0] !$= "_" && !strcmp($board[2,0], $board[2,1]) && !strcmp($board[2,1], $board[2,2]))
	      return true;
	      
	   return false;
	}

Let's break down the if(...) statements to see what is going on::

	if($board[0,0] !$= "_" &&)

The first part checks to see if the row contains a blank entry ("_"). If this is true, then there is no point checking for anything else. The row does not have three similar values, so the function can move on to check the rest of the rows::

	!strcmp($board[0,0], $board[0,1])

If the first check succeeds, the values of the row's first and second column are compared. If they are the same, a 0 is returned. Instead of catching the return value in a variable and testing it, we can just use the logical NOT (!) operator.

If the first two columns are the same, we can just compare the third column to one of the others. There is no point in making three string comparisons::

	&& !strcmp($board[0,1], $board[0,2])

There are most likely more optimized ways to check for this kind of situation, but the above code demonstrates multiple syntactical approaches and comparisons. We can now have a way to check for a victory condition. Go back into the setBoardValue(...) function and add the win check::

	function setBoardValue(%row, %column, %value)
	{
	   // Make sure "X" or "O" was passed in
	   if(%value !$= "X" && %value !$= "O")
	   {
	      echo("Invalid entry:\nPlease use \'X\' or \'O\'");
	      return;
	   }
	   
	   // Set the board value
	   $board[%row, %column] = %value;
	   
	   // Check to see if we have the same
	   // three values in a row
	   if(checkForWin())
	   {
	      // Entire row matched
	      // Print a victory message
	      echo("\n**********************");
	      echo("*    Win Condition!  *");
	      echo("**********************\n");
	      
	      // Print the board
	      printBoard();
	      
	      // Reset the game
	      echo("\nResetting board");
	      resetBoard();
	   }
	}

Remember, the checkForWin() functions returns a true if the game has been won. The first portion of the code prints a message about the victory. After that, the board is printed to show what row won, and then resets the game.

While this version of the game is very rudimentary, you should be able to expand it by checking for columns and diagonals. There is plenty of room for optimization and more functions to make the game easier. However, this is not necessary to learning a powerful game engine like Torque 3D.

Conclusion
----------

This guide covered the concept of arrays, both single and multi-dimensional. Lessons from past guides were also used: string comparisons, logical operators, function declaration and calling, loop structures, etc.