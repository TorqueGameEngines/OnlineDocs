Variables
=========

A variable is a letter, word, or phrase linked to a value stored in your game's memory and used during operations. Creating a variable is a one line process. The following code creates a variable by naming it and assigning a value::

	%localVariable = 3;

You can assign any type value to the variable you want. This is referred to as a language being type-insensitive. TorqueScript does not care (insensitive) what you put in a variable, even after you have created it. The following code is completely valid::

	%localVariable = 27;
	%localVariable = "Heather";
	%localVariable = "7 7 7";

The main purpose of the code is to show that TorqueScript treats all data types the same way. It will interpret and convert the values internally, so you do not have to worry about typecasting. That may seem a little confusing. After all, when would you want a variable that can store a number, a string, or a vector?

You will rarely need to, which is why you want to start practicing good programming habits. An important practice is proper variable naming. The following code will make a lot more sense, considering how the variables are named::

	%userName = "Heather";
	%userAge = 27;
	%userScores = "7 7 7";

TorqueScript is more forgiving than low level programming languages. While it expects you to obey the basic syntax rules, it will allow you to get away with small mistakes or inconsistency. The best example is variable case sensitivity. With variables, TorqueScript is not case sensitive. You can create a variable and refer to it during operations without adhering to case rules::

	%userName = "Heather";
	echo(%Username);

In the above code, ``%userName`` and ``%Username``	 are the same variable, even though they are using different capitalization. You should still try to remain consistent in your variable naming and usage, but you will not be punished if you slip up occasionally.

There are two types of variables you can declare and use in TorqueScript: *local* and *global.* Both are created and referenced similarly::

	%localVariable = 1;
	$globalVariable = 2;

As you can see, local variable names are preceded by the percent sign ``%``. Global variables are preceded by the dollar sign ``$``. Both types can be used in the same manner: operations, functions, equations, etc. The main difference has to do with how they are scoped.

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
