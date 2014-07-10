Packages
========

The package keyword tells the console that the subsequent block of code is to be declared but not loaded. Packages provide dynamic function-polymorphism in TorqueScript. In short, a function defined in a package will over-ride the prior definition of a same named function when the is activated. When the package is subsequently de-activated, the previous definition of any overridden functions will be re-asserted. 

A package has the following syntax::

	package package_name 
	{
	   function function_definition0() 
	   {
	      // code
	   }
	   function function_definitionN() 
	   {
	      // code
	   }
	};

Some things to know: 

* The same function can be defined in multiple packages. 
* Only functions can be packaged. 
* Datablocks cannot be packaged. 
* Packages 'stack' meaning that deactivating packages activated prior to the currently active (s) will deactivate all packages activated prior to the being deactivated (see example below). 
* Functions in a package may activate and deactivate packages. 

In order to use the functions in a package, the package must be activated::

	activatePackage(package_name);

Subsequently a package can be deactivated::

	deactivatePackage(package_name);

First, define a function and two packages, each of which provides an alternative definition by the same name::

	function testFunction() 
	{
	   echo( "testFunction() - unpackaged." );
	}
	package MyPackage0
	{
	  function testFunction() 
	  {
	      echo( "testFunction() - MyPackage0." );
	  }
	};
	package MyPackage1
	{
	  function testFunction() 
	  {
	      echo( "testFunction() - MyPackage1." );
	  }
	};

Now invoke the testFunction() function from the console under three different conditions::

	==> testFunction();
	testFunction() - unpackaged.
	==> activatePackage( MyPackage0 );
	==> testFunction(); 
	testFunction() - MyPackage0.
	==> activatePackage( MyPackage1 );
	==> testFunction(); 
	testFunction() - MyPackage1.
	==> deactivatePackage( MyPackage0 );  // MyPackage1 is automatically deactivated.
	==> testFunction(); 
	testFunction() - unpackaged.
