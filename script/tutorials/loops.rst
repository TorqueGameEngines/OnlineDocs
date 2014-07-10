Looping Structures
==================

There are two types of used in TorqueScript: for and while loops. A for loop repeats a statement or block of code for a set number of iterations. A while loop on the other hand repeats a statement or block of code as long as an expression given to the while loop remains true.

for Loop Syntax::

	for(expression0; expression1; expression2) 
	{
	    statement(s);
	}

One way to label the expressions in this syntax are (startExpression; testExpression; countExpression). Each expression is separated by a semi-colon.

while Loop Syntax::

	while(expression) 
	{
	    statements;
	}

As soon as the expression is met, the while loop will terminate.

Example For Loop::

	for(%count = 0; %count < 3; %count++) 
	{
	    echo(%count);
	}

	OUTPUT:
	0
	1
	2

While Loop::

	%countLimit = 0;

	while(%countLimit <= 5)
	{
	   echo("Still in loop");
	   %count++;
	}
	echo("Loop was terminated");

	OUTPUT:
	Still in loop
	Still in loop
	Still in loop
	Still in loop
	Still in loop
	Loop was terminated

Creating the Script
-------------------

First, we need to create a new script:

#. Navigate to your project's game/scripts/client directory.
#. Create a new script file called "loops". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs.
#. Open your new script using a text editor or Torsion.

Before writing any actual script code, we should go ahead and tell the game it should load the script. Open game/scripts/client/init.cs. Scroll down to the initClient function. Under the // Client scripts section, add the following:

Execute our new script::

	exec("./loops.cs");

We will start with a very basic loop. Add the following to your script::

	// Print 0 -> %count in the console
	function printNumbers(%count)
	{
	   for(%i = 0; %i < %count; %i++)
	   {
	      echo(%i);
	   }
	}

The above function takes in a single argument (%count). The for(...) loop uses three expressions. The first is declaration expression. This is the setup for the loop. In this example, the iterator is defined. The iterator is the variable that will change each loop.

The second expression sets up the condition that will cause the loop to terminate. In the above code, when the iterator is no longer less than the %count variable, the loop will end. Finally, the third expression is the logic that occurs after each loop. In our example, we increment the count of our iterator.

The main logic is enclosed in brackets after the loop declaration. In above code, the iterator (%i) is printed to the console each loop. To test your new script:

#. Save the script
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, and press enter::

	printNumbers(10);

Your output should look like the following::

	0
	1
	2
	3
	4
	5
	6
	7
	8
	9

As expected, the iterator is printed to the console then incremented by 1. Notice that it stops when it gets to 9, even though 10 was passed in. Look at the second expression's logic again::

	%i < %count;

When %i reaches 10, then it is equal to the %count passed in which is also 10. 10 is not less than 10. As soon as that expression failed, the loop terminated. To get the full ten count, modify the function to use a different logic check::

	function printNumbers(%count)
	{
	   for(%i = 0; %i <= %count; %i++)
	   {
	      echo(%i);
	   }
	}

Now, when you call the following code in the console::

	printNumbers(10);

Your output should be::

	0
	1
	2
	3
	4
	5
	6
	7
	8
	9
	10

You can apply different modifiers to your iterator. You do not always have to use an incremental counter. Add the following function to your script::

	// Print %startCount -> 0 in the console
	function countdown(%startCount)
	{
	   for(%i = %startCount; %i >= 0; %i--)
	   {
	      echo(%i);
	   }
	}

Save and run. Now you can see a countdown from a base number, as the following shows::

	countdown(5);

Output::

	5
	4
	3
	2
	1
	0

An important keyword to remember when working with for(...) loops is continue. The continue keyword will cause a loop to immediately skip to the next iteration, similar to how the return keyword works in a function. Add the following function to see it work::

	// Print 0 -> %count, except %skipNumber, in the console
	function skipCount(%count, %skipNumber)
	{
	   for(%i = 0; %i <= %count; %i++)
	   {
	      if(%i == %skipNumber)
	         continue;
	      
	      echo(%i);
	   }
	}

In the above code, when the iterator (%i) exactly matches the %skipNumber variable, the loop immediately goes to the next iteration. This ignores the echo(...) command on the next line. Try calling this in the console::

	skipCount(5, 4);

The output should be::

	0
	1
	2
	3
	5

Instead of terminating soon as the iterator reached 4, a continue keyword was used to skip to the next loop iteration. If a less complex loop is desired, the while(...) structure will be handy.

Add the following function to your script::

	// Increase %count incrementally until it is no
	// longer less than %breakNumber
	function whileExample(%count, %breakNumber)
	{
	   // While the count is less than the breaknumber
	   while(%count < %breakNumber)
	   {
	      // Print the count
	      echo(%count);
	      
	      // Increase the count
	      %count++;
	   }
	}

In this new function, the loop will check the expression in the parenthesis each time it completes an iteration. The body of the loop, contained in the brackets, simply prints the %count variable and then increases. You must be careful with loops, especially while(...) structures. The wrong use of variables can result in an infinite loop which will freeze your game.

Break is another keyword that affects looping structures. It will immediately terminate the loop. The following function shows proper use of a while loop avoiding infinite cycling::

	// Increase %iterator until it is equal to
	// %conditional. When it is, break out of
	// the infinite loop
	function breakOut(%iterator, %conditional)
	{
	   // If iterator is less than conditional
	   // we will be stuck in an infinite loop
	   // Error out and exit function.
	   if(%iterator > %conditional)
	   {
	      error("Iterator is greater than conditional, try again");
	      return;
	   }
	   
	   // Loop infinitely until a condition is met   
	   while(true)
	   {
	      // Condition has been met, break out.
	      if(%iterator == %conditional)
	         break;
	         
	      echo(%iterator);   
	      
	      %iterator++;
	   }
	}

Before the loop even starts, an if(...) check is made to make sure the variables used by the loop will insure a proper break. The goal of the loop is to continue iterating until the %iterator variable is equal to the %conditional.

The while(true) syntax creates the "infinite" loop. However, it will not loop infinitely since a break keyword is used. Once the %iterator is equal to the %conditional, a break is called. Otherwise, the %iterator is printed to the console and then increased.

To see the output, call the following in the console (pressing enter after each line)::

	breakOut(10,1);
	breakOut(10,10);
	breakOut(0, 10);

Output::

	Iterator is greater than conditional, try again

	0
	1
	2
	3
	4
	5
	6
	7
	8
	9

The first call gives you the error message. The second call immediately causes the loop to terminate since the two variables are already equal. The last call provides the proper output of the function.

The last concept we will cover is nested loops. These are loops within other loops. For the next example, the terminology should be addressed first. The first loop is identical to the structures you have created in the past.

The nested loop is declared inside the first loop. Remember, it is important to be smart about your variable names. You can name your iterators anything you want, such as using %iterator instead of %i. If you go with the longer name, then it would make sense to name your second iterator something like "%iteratorTwo".

The naming convention for loop iterators is preferential. The use of %i typically stands for iterator. In quite a few programming primers (such as the ones this writer has read), the second iterator is often named %j. For these simple examples, you can get away with this. In more complex or critical loops, you might want to name your iterators based on what the loop does.

Add the following function::

	// Run a nested loop
	// Print messages, color based on level
	function nestedLoops()
	{
	   // Max iteration for first loop
	   %firstCount = 10;
	   
	   // Execute first loop %firstCount times
	   for(%i = 0; %i < %firstCount; %i++)
	   {
	      // Print in teal
	      warn("Running main loop: " @ %i);
	   }
	}

Run the function in the console, and you should see the following printed in a teal color::

	Running main loop: 0
	Running main loop: 1
	Running main loop: 2
	Running main loop: 3
	Running main loop: 4
	Running main loop: 5
	Running main loop: 6
	Running main loop: 7
	Running main loop: 8
	Running main loop: 9

For the nested loop, we will stick with a pattern. A second count variable should be declared, and the nested loop should perform a similar operation. Modify the function to use this pattern::

	// Run a nested loop
	// Print messages, color based on level
	function nestedLoops()
	{
	   // Max iteration for first loop
	   %firstCount = 10;
	   
	   // Max iteration for nested loop
	   %secondCount = 2;
	   
	   // Execute first loop %firstCount times
	   for(%i = 0; %i < %firstCount; %i++)
	   {
	      // Execute nested loop %secondCount times
	      for(%j = 0; %j < %secondCount; %j++)
	      {
	         // Print in red
	         error("Running nested loop: " @ %j);
	      }
	      // Print in teal
	      warn("Running main loop: " @ %i);
	   }
	}

Run this function again to see the new output::

	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 0
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 1
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 2
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 3
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 4
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 5
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 6
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 7
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 8
	Running nested loop: 0
	Running nested loop: 1
	Running main loop: 9

Your console output will be color-coded. The main loop output should still be teal, and the nested loop output should be red. Here is the breakdown of the full loop:

#. First loop starts
#. Main iterator (%i) starts at 0
#. Nested loop starts
#. Second iterator (%j) starts at 0
#. Print second iterator (0)
#. Increment second iterator
#. Print second iterator (1)
#. End nested loop
#. Print first iterator
#. Increment first loop
#. Go back to step 3, repeat until first loop ends

Based on the default values, the nested loop will execute 10 times. Its iterator will reset each time the first loop iterates. Try adjusting the %firstCount and %secondCount variables to see the varying outputs if you are still trying to understand the concept.

Conclusion
----------

This guide covered the basics of looping structures. You will use these often when you need to accomplish repetitive tasks or iterate through lists. Remember the following:

* If you perform a task more than twice, you might want to use a loop
* Be smart when naming your iterators and other variables
* Always perform safety checks for infinite loops
