Objects
=======

The most complex aspect of TorqueScript involves dealing with game objects. Much of your object creation will be performed in the World Editor, but you should still know how to manipulate objects at a script level. One thing to remember is that everything in TorqueScript is an object: players, vehicles, items, etc.

Every object added in the level is saved to a mission file, which is written entirely in TorqueScript. This also means every game object is accessible from script.

Syntax
------

Even though objects are originally created in C++, they are exposed to script in a way that allows them to be declared using the following syntax::

	%objectID = new ObjectType(Name : CopySource, arg0, ..., argn) 
	{
	   <datablock = DatablockIdentifier;>
	   
	   [existing_field0 = InitialValue0;]
	   ...
	   [existing_fieldN = InitialValueN;]

	   [dynamic_field0 = InitialValue0;]
	   ...
	   [dynamic_fieldN = InitialValueN;]
	};

%objectID
	Is the variable where the object's handle will be stored.

new
	Is a key word telling the engine to create an instance of the following ObjectType.

ObjectType
	Is any class declared in the engine or in script that has been derived from SimObject or a subclass of SimObject. SimObject-derived objects are what we were calling "game world objects" above.

Name (optional)
	Is any expression evaluating to a string, which will be used as the object's name.

CopySource (optional)
	The name of an object which is previously defined somewhere in script. Existing field values will be copied from CopySource to the new object being created. Any dynamic fields defined in CopySource will also be defined in the new object, and their values will be copied. Note: If CopySource is of a different ObjectType than the object being created, only CopySource's dynamic fields will be copied.

arg0, ..., argn (optional)
	Is a comma separated list of arguments to the class constructor (if it takes any).

datablock
	Many objects (those derived from GameBase, or children of GameBase) require datablocks to initialize specific attributes of the new object. Datablocks are discussed below.

existing_fieldN
	In addition to initializing values with a datablock, you may also initialize existing class members (fields) here. In order to modify a member of a C++-defined class, the member must be exposed to the Console.

dynamic_fieldN
	Lastly, you may create new fields (which will exist only in Script) for your new object. These will show up as dynamic fields in the World Editor Inspector.

The main object variants you can create are SimObjects without a datablock, and game objects which require a datablock. The most basic SimObject can be created in a single line of code::

	// Create a SimObject without any name, argument, or fields.
	$exampleSimObject = new SimObject();

The ``$exampleSimObject`` variable now has access to all the properties and functions of a basic SimObject. Usually, when you are creating a SimObject you will want custom fields to define features::

	// Create a SimObject with a custom field
	$exampleSimObject = new SimObject() 
	{
	   catchPhrase = "Hello world!";
	};

As with the previous example, the above code creates a SimObject without a name which can be referenced by the global variable ``$exampleSimObject``. This time, we have added a user defined field called "catchPhrase." There is not a single stock Torque 3D object that has a field called "catchPhrase." However, by adding this field to the SimObject it is now stored as long as that object exists.

The other game object variant mentioned previously involves the usage of datablocks. Datablocks contain static information used by a game object with a similar purpose. Datablocks are transmitted from a server to client, which means they cannot be modified while the game is running.

We will cover datablocks in more detail later, but the following syntax shows how to create a game object using a datablock::

	// create a StaticShape using a datablock
	datablock StaticShapeData(ceiling_fan)
	{
	   category = "Misc";
	   shapeFile = "art/shapes/undercity/cfan.dts";
	   isInvincible = true;
	};

	new StaticShape(CistFan) 
	{
	   dataBlock = "ceiling_fan";
	   position = "12.5693 35.5857 59.5747";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	};

Once you have learned about datablocks, the process is quite simple:

#. Create a datablock in script, or using the datablock editor
#. Add a shape to the scene from script or using the World Editor
#. Assign the new object a datablock

Handles vs Names
----------------

Every game object added to a level can be accessed by two parameters:

Handle
	A unique numeric ID generated when the object is created

Name
	This is an optional parameter given to an object when it is created. You can assign a name to an object from the World Editor, or do so in TorqueScript.

Example::

	// In this example, CistFan is the name of the object
	new StaticShape(CistFan) 
	{
	   dataBlock = "ceiling_fan";
	   position = "12.5693 35.5857 59.5747";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	};

While in the World Editor, you will not be allowed to assign the same name to multiple, separate objects. The editor will ignore the attempt. If you manually name two objects the same thing in script, the game will only load the first object and ignore the second.

Singletons
----------

If you need a global script object with only a single instance, you can use the singleton keyword. Singletons, in TorqueScript, are mostly used for unique shaders, materials, and other client-side only objects.

For example, SSAO (screen space ambient occlusion) is a post-processing effect. The game will only ever need a single instance of the shader, but it needs to be globally accessible on the client. The declaration of the SSAO shader in TorqueScript can be shown below::

	singleton ShaderData( SSAOShader )
	{   
	   DXVertexShaderFile 	= "shaders/common/postFx/postFxV.hlsl";
	   DXPixelShaderFile 	= "shaders/common/postFx/ssao/SSAO_P.hlsl";            
	   pixVersion = 3.0;
	};

Fields
------

Objects instantiated via script may have data members, referred to as Fields.

Methods
-------

In addition to the creation of stand-alone functions, TorqueScript allows you to create and call methods attached to objects. Some of the more important Console Methods are already written in C++, then exposed to script. You can call these methods by using the dot ``.`` notation::

	objHandle.function_name();

	objName.function_name();

Example::

	new StaticShape(CistFan) 
	{
	   dataBlock = "ceiling_fan";
	   position = "12.5693 35.5857 59.5747";
	   rotation = "1 0 0 0";
	   scale = "1 1 1";
	};

	// Write all the objects methods to the console log
	CistFan.dump();

	// Get the ID of an object, using the object's name
	$objID = CistFan.getID();

	// Print the ID to the console
	echo("Object ID: ", $objID);

	// Get the object's position, using the object's handle
	%position = $objID.getPosition();

	// Print the position to the console
	echo("Object Position: ", %position);

The above example shows how you can call an object's method by using its name or a variable containing its handle (unique ID number). Additionally, TorqueScript supports the creation of methods that have no associated C++ counterpart::

	// function - Is a keyword telling TorqueScript we are defining a new function.
	// ClassName::- Is the class type this function is supposed to work with.
	// function_name - Is the name of the function we are creating.
	// ... - Is any number of additional arguments.
	// statements - Your custom logic executed when function is called
	// %this- Is a variable that will contain the handle of the 'calling object'.
	// return val - The value the function will give back after it has completed. Optional.

	function Classname::func_name(%this, [arg0],...,[argn]) 
	{
	   statements;
	   [return val;]
	}
                
At a minimum, Console Methods require that you pass them an object handle. You will often see the first argument named %this. People use this as a hint, but you can name it anything you want. As with Console Functions any number of additional arguments can be specified separated by commas.

As a simple example, let's say there is an object called Samurai, derived from the Player class. It is likely that a specific appearance and play style will be given to the samurai, so custom ConsoleMethods can be written. Here is a sample::

	function Samurai::sheatheSword(%this)
	{
	    echo("Katana sheathed");
	}

When you add a Samurai object to your level via the World Editor, it will be given an ID. Let's pretend the handle (ID number) is 1042. We can call its ConsoleMethod once it is defined, using the period syntax::

	1042.sheatheSword();

	OUTPUT: "Katana sheathed"

Notice that no parameters were passed into the function. The ``%this`` parameter is inherent, and the original function did not require any other parameters.
