ArrayObject
===========

Data structure for storing indexed sequences of key/value pairs.

Inherit:
	:doc:`SimObject`

Description
-----------

This is a powerful array class providing PHP style arrays in TorqueScript.

The following features are supported:

* array pointers: this allows you to move forwards or backwards through the array as if it was a list, including jumping to the start or end.
* sorting: the array can be sorted in either alphabetic or numeric mode, on the key or the value, and in ascending or descending order
* add/remove elements: elements can be pushed/popped from the start or end of the array, or can be inserted/erased from anywhere in the middle
* removal of duplicates: remove duplicate keys or duplicate values
* searching: search the array and return the index of a particular key or value
* counting: count the number of instaces of a particular value or key in the array, as well as the total number of elements
* advanced features: array append, array crop and array duplicate

Array element keys and values can be strings or numbers.

Methods
-------

.. cpp:function:: void ArrayObject::add(string key, string value)

	Adds a new element to the end of an array (same as push_back() ).

	:param key: Key for the new element
	:param value: Value for the new element

.. cpp:function:: bool ArrayObject::append(ArrayObject target)

	Appends the target array to the array object.

	:param target: ArrayObject to append to the end of this array

.. cpp:function:: int ArrayObject::count()

	Get the number of elements in the array.

.. cpp:function:: int ArrayObject::countKey(string key)

	Get the number of times a particular key is found in the array.

	:param key: Key value to count

.. cpp:function:: int ArrayObject::countValue(string value)

	Get the number of times a particular value is found in the array.

	:param value: Array element value to count

.. cpp:function:: bool ArrayObject::crop(ArrayObject target)

	Removes elements with matching keys from array.

	:param target: ArrayObject containing keys to remove from this array

.. cpp:function:: bool ArrayObject::duplicate(ArrayObject target)

	Alters array into an exact duplicate of the target array.

	:param target: ArrayObject to duplicate

.. cpp:function:: void ArrayObject::echo()

	Echos the array contents to the console.

.. cpp:function:: void ArrayObject::empty()

	Emptys all elements from an array.

.. cpp:function:: void ArrayObject::erase(int index)

	Removes an element at a specific position from the array.

	:param index: 0-based index of the element to remove

.. cpp:function:: int ArrayObject::getCurrent()

	Gets the current pointer index.

.. cpp:function:: int ArrayObject::getIndexFromKey(string key)

	Search the array from the current position for the key.

	:param value: Array key to search for

	:return: Index of the first element found, or -1 if none 

.. cpp:function:: int ArrayObject::getIndexFromValue(string value)

	Search the array from the current position for the element.

	:param value: Array value to search for

	:return: Index of the first element found, or -1 if none 

.. cpp:function:: string ArrayObject::getKey(int index)

	Get the key of the array element at the submitted index.

	:param index: 0-based index of the array element to get

	:return: The key associated with the array element at the specified index, or "" if the index is out of range 

.. cpp:function:: string ArrayObject::getValue(int index)

	Get the value of the array element at the submitted index.

	:param index: 0-based index of the array element to get

	:return: The value of the array element at the specified index, or "" if the index is out of range 

.. cpp:function:: void ArrayObject::insert(string key, string value, int index)

	Adds a new element to a specified position in the array. 
	
	* index = 0 will insert an element at the start of the array (same as push_front())
	* index = array. count() will insert an element at the end of the array (same as push_back())

	:param key: Key for the new element
	:param value: Value for the new element
	:param index: 0-based index at which to insert the new element

.. cpp:function:: int ArrayObject::moveFirst()

	Moves array pointer to start of array.

	:return: Returns the new array pointer 

.. cpp:function:: int ArrayObject::moveLast()

	Moves array pointer to end of array.

	:return: Returns the new array pointer 

.. cpp:function:: int ArrayObject::moveNext()

	Moves array pointer to next position.

	:return: Returns the new array pointer, or -1 if already at the end 

.. cpp:function:: int ArrayObject::movePrev()

	Moves array pointer to prev position.

	:return: Returns the new array pointer, or -1 if already at the start 

.. cpp:function:: void ArrayObject::pop_back()

	Removes the last element from the array.

.. cpp:function:: void ArrayObject::pop_front()

	Removes the first element from the array.

.. cpp:function:: void ArrayObject::push_back(string key, string value)

	Adds a new element to the end of an array.

	:param key: Key for the new element
	:param value: Value for the new element

.. cpp:function:: void ArrayObject::push_front(string key, string value)

	Adds a new element to the front of an array.

.. cpp:function:: void ArrayObject::setCurrent(int index)

	Sets the current pointer index.

	:param index: New 0-based pointer index

.. cpp:function:: void ArrayObject::setKey(string key, int index)

	Set the key at the given index.

	:param key: New key value
	:param index: 0-based index of the array element to update

.. cpp:function:: void ArrayObject::setValue(string value, int index)

	Set the value at the given index.

	:param value: New array element value
	:param index: 0-based index of the array element to update

.. cpp:function:: void ArrayObject::sort(bool ascending)

	Alpha sorts the array by value.

	:param ascending: [optional] True for ascending sort, false for descending sort

.. cpp:function:: void ArrayObject::sorta()

	Alpha sorts the array by value in ascending order.

.. cpp:function:: void ArrayObject::sortd()

	Alpha sorts the array by value in descending order.

.. cpp:function:: void ArrayObject::sortf(string functionName)

	Sorts the array by value in ascending order using the given callback function.

	:param functionName: Name of a function that takes two arguments A and B and returns -1 if A is less, 1 if B is less, and 0 if both are equal.

	Example::

		function mySortCallback(%a, %b)
		{
		   returnstrcmp( %a.name, %b.name );
		}
		
		%array.sortf( "mySortCallback" );

.. cpp:function:: void ArrayObject::sortfd(string functionName)

	Sorts the array by value in descending order using the given callback function.

	:param functionName: Name of a function that takes two arguments A and B and returns -1 if A is less, 1 if B is less, and 0 if both are equal.

.. cpp:function:: void ArrayObject::sortfk(string functionName)

	Sorts the array by key in ascending order using the given callback function.

	:param functionName: Name of a function that takes two arguments A and B and returns -1 if A is less, 1 if B is less, and 0 if both are equal.

.. cpp:function:: void ArrayObject::sortfkd(string functionName)

	Sorts the array by key in descending order using the given callback function.

	:param functionName: Name of a function that takes two arguments A and B and returns -1 if A is less, 1 if B is less, and 0 if both are equal.

.. cpp:function:: void ArrayObject::sortk(bool ascending)

	Alpha sorts the array by key.

	:param ascending: [optional] True for ascending sort, false for descending sort

.. cpp:function:: void ArrayObject::sortka()

	Alpha sorts the array by key in ascending order.

.. cpp:function:: void ArrayObject::sortkd()

	Alpha sorts the array by key in descending order.

.. cpp:function:: void ArrayObject::sortn(bool ascending)

	Numerically sorts the array by value.

	:param ascending: [optional] True for ascending sort, false for descending sort

.. cpp:function:: void ArrayObject::sortna()

	Numerically sorts the array by value in ascending order.

.. cpp:function:: void ArrayObject::sortnd()

	Numerically sorts the array by value in descending order.

.. cpp:function:: void ArrayObject::sortnk(bool ascending)

	Numerically sorts the array by key.

	:param ascending: [optional] True for ascending sort, false for descending sort

.. cpp:function:: void ArrayObject::sortnka()

	Numerical sorts the array by key in ascending order.

.. cpp:function:: void ArrayObject::sortnkd()

	Numerical sorts the array by key in descending order.

.. cpp:function:: void ArrayObject::uniqueKey()

	Removes any elements that have duplicated keys (leaving the first instance).

.. cpp:function:: void ArrayObject::uniqueValue()

	Removes any elements that have duplicated values (leaving the first instance).

Fields
------

.. cpp:member:: bool  ArrayObject::caseSensitive

	Makes the keys and values case-sensitive. By default, comparison of key and value strings will be case-insensitive.

.. cpp:member:: caseString  ArrayObject::key

	Helper field which allows you to add new key['keyname'] = value pairs.
