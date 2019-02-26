Quick Reference - TODO
*************************

Language Features
===================

TorqueScript is a typeless scripting language, with similarities in syntax to C/C++. In TorqueScript, you will find that most C/C++ operators work in the familiar way (with important exceptions, as noted here). Besides a subset of C/C++, TorqueScript provides:

* Case-insensitive symbols; keywords *false* and *FALSE* are identical.
* Auto creation and destruction of local/global variables and their storage.
* String concatenation, comparison, and auto-string-constant creation.
* Function packaging.


Variable Names
================

Constants
===========

Operators
==========

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

**Bitwise Operators**
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

**Assignment and Assignment Operators**
========  ====================  ==============  ===========
Operator  Name                  Example         Explanation
========  ====================  ==============  ===========
``=``     Assignment            ``$a = $b;``    Assign value of ``$b`` to ``$a``
                                                **Note:**  the value of an assignment is the value being assigned, so $a = $b = $c is legal.
``op=``   Assignment Operators  ``$a op= $b;``  Equivalent to ``$a = $a op $b``, where op can be any of:  * / % + - & | ^ << >>
========  ====================  ==============  ===========

**String Operators**
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

**Miscellaneous**
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


Keywords
=========

break
^^^^^^

case
^^^^^^

continue
^^^^^^^^^

datablock
^^^^^^^^^^

default
^^^^^^^^

else
^^^^^

FALSE
^^^^^^

for
^^^^

function
^^^^^^^^^

if
^^^^

new
^^^^^^

package
^^^^^^^^

parent
^^^^^^^

return
^^^^^^^^

switch
^^^^^^^

switch$
^^^^^^^^

TRUE
^^^^^

while
^^^^^^
