Types
=====

TorqueScript implicitly supports several variable data-types: numbers, strings, booleans, arrays and vectors. If you wish to test the various data types, you can use the ``echo(...)`` command. For example::

	%meaningOfLife = 42;
	echo(%meaningOfLife);

	$name = "Heather";
	echo($name);

The echo will post the results in the console, which can be accessed by pressing the tilde key :kbd:`~` while in game.

Numbers
-------

TorqueScript handles standard numeric types::

	123     (Integer)
	1.234   (floating point)
	1234e-3 (scientific notation)
	0xc001  (hexadecimal)

Strings
-------

Text, such as names or phrases, are supported as strings. Numbers can also be stored in string format. Standard strings are stored in double-quotes::

	"abcd"    (string)

Example::

	$UserName = "Heather";

Strings with single quotes are called "tagged strings"::

	'abcd'  (tagged string)

Tagged strings are special in that they contain string data, but also have a special numeric tag associated with them. Tagged strings are used for sending string data across a network. The value of a tagged string is only sent once, regardless of how many times you actually do the sending.

On subsequent sends, only the tag value is sent. Tagged values must be de-tagged when printing. You will not need to use a tagged string often unless you are in need of sending strings across a network often, like a chat system::

	$a = 'This is a tagged string';
	echo("  Tagged string: ", $a);
	echo("Detagged string: ", detag($a));

The output will be similar to this::

	Tagged string: 24
	Detagged string: 

The second echo will be blank unless the string has been passed to you over a network.

Booleans
--------

Like most programming languages, TorqueScript also supports booleans. Boolean numbers have only two values- true or false::

	true    (1)
	false   (0)

Again, as in many programming languages the constant "true" evaluates to the number 1 in TorqueScript, and the constant "false" evaluates to the number zero. However, non-zero values are also considered true. Think of booleans as "on/off" switches, often used in conditional statements::

	$lightsOn = true;

	if($lightsOn)
	  echo("Lights are turned on");

Arrays
------

Arrays are data structures used to store consecutive values of the same data type::

	$TestArray[n]   (Single-dimension)
	$TestArray[m,n] (Multidimensional)
	$TestArray[m_n] (Multidimensional)

If you have a list of similar variables you wish to store together, try using an array to save time and create cleaner code. The syntax displayed above uses the letters ``n`` and ``m`` to represent where you will input the number of elements in an array. The following example shows code that could benefit from an array::

	$firstUser = "Heather";
	$secondUser = "Nikki";
	$thirdUser = "Mich";

	echo($firstUser);
	echo($secondUser);
	echo($thirdUser);

Instead of using a global variable for each user name, we can put those values into a single array::

	$userNames[0] = "Heather";
	$userNames[1] = "Nikki";
	$userNames[2] = "Mich";

	echo($userNames[0]);
	echo($userNames[1]);
	echo($userNames[2]);

Now, let's break the code down. Like any other variable declaration, you can create an array by giving it a name and value::

	$userNames[0] = "Heather";

What separates an array declaration from a standard variable is the use of brackets []. The number you put between the brackets is called the index. The index will access a specific element in an array, allowing you to view or manipulate the data. All the array values are stored in consecutive order.

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

The first element ``[0,0]`` points to the letter 'a'. The last element ``[2,2]`` points to the letter 'i'.

Vectors
-------

Vectors are a helpful data-type which are used throughout Torque 3D. For example, many fields in the World Editor take numeric values in sets of 3 or 4. These are stored as strings and interpreted as "vectors"::

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
