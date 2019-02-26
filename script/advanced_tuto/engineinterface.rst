Engine To Script
******************

Introduction
==============
This document intends to give an overview and a set of rules for creating and documenting Torque control layer interfaces. There are specific functions used for communication between TorqueScript and the C++ engine. This system makes heavy use of macros and ties in closely with the Console system.

If you plan on extending the engine to support new classes or functionality, you will need to adhere to this guide so as to not break your build. Equally important is the practice of documenting your extensions, so make heavy use of the fields that exist for documentation.

.. note:: This document was primarily written for C++ programmers with access to Torque 3D's source code. Without source code you will not be able to directly implement any of the following. However, someone without source access should still be able to harvest important documentation on Torque 3D's control layer interface.


Creating Call-in Points
========================
A call-in point is an entry point from the control layer into Torque. In simpler terms, these are functions called from TorqueScript. There are two types of call-in functions: global and class

Global functions
------------------
These are stand alone functions that can be called in TorqueScript without belonging to any class or object.

Example::

    echo("Hello World");

You define a global function by using the following procedure:


Include engineAPI.h in your cpp implementation file::

    #include "console/engineAPI.h"
                

Define the function::

    DefineEngineFunction( myFunction, myReturnType, ( S32 arg1, F32 arg2, const char* arg3 ),, "Documentation string" )
    {
       // Code goes here
    }

**Working Example in Torque 3D**::

    DefineEngineFunction(addBadWord, bool, (const char* badWord),,
    					 "Add a string to the bad word filter\n"
    					 "The bad word filter is a table containing words which will not be "
    					 "displayed in chat windows. Instead, a designated replacement string will be displayed.\n"
    					 "@param badWord Exact text of the word to restrict.\n"
    					 "@return True if word was successfully added, false if the word or a subset of it already exists in the table\n"
    					 "@see filterString\n\n"
    					 "@tsexample\n"
    						"// In this game, \"Foobar\" is banned\n"
    						"%badWord = \"Foobar\";\n\n"
    						"// Returns true, word was successfully added\n"
    						"addBadWord(%badWord);\n\n"
    						"// Returns false, word has already been added\n"
    						"addBadWord(\"Foobar\");"
    					 "@endtsexample\n"
    					 "@ingroup Game")
    {
    	TORQUE_UNUSED(badWord);
    	return gBadWordFilter->addBadWord(badWord);
    }



Class methods
--------------
These are functions called in TorqueScript from an object associated with a class, such as SFXSource.

**Example**::

    %sfxSourceObject.stop() 


You define a class method by using the following procedure:

Include engineAPI.h in your cpp implementation file::

    #include "console/engineAPI.h"
                
Define the method::

    DefineEngineMethod( MyClass, myMethod, myReturnType, ( S32 arg1, F32 arg2, const char* arg3 ),, "Documentation string" )
    {
       // Code goes here
    }
                
**Working Example in Torque 3D**::

    DefineEngineMethod( GuiCanvas, reset, void, (),,
    				   "@brief Reset the update regions for the canvas.\n\n"
    
    				   "@tsexample\n"
    				   "Canvas.reset();\n"
    				   "@endtsexample\n\n")
    {
    	object->resetUpdateRegions();
    }

Within the function bodies, you can access the given parameters and return a value just like with a normal C++ function. To assign default values to arguments (like in C++: S32 index=-1), you use the macro argument left empty above::

    DefineEngineMethod( MyClass, myMethod, myReturnType, ( S32 arg1, F32 arg2, const char* arg3 ), ( -1.f, "foo" ), "Documentation string" )
    {
       // Code goes here
    }


Here, -1.f is the default argument for "arg2" and "foo" is the default argument for "arg3." **Be aware that the default argument list is matched starting from the end of the argument list (like it happens in C++)**.


**Working Example in Torque 3D**::

    DefineEngineMethod( SFXSource, play, void, ( F32 fadeInTime ), ( -1.f ),
       "Start playback of the source.\n"
       "If the sound data for the source has not yet been fully loaded, there will be a delay after calling "
       "play and playback will start after the data has become available.\n\n"
       "@param fadeInTime Seconds for the sound to reach full volume.  If -1, the SFXDescription::fadeInTime "
          "set in the source's associated description is used.  Pass 0 to disable a fade-in effect that may "
          "be configured on the description." )
    {
       object->play( fadeInTime );
    }


Notes
------

* You cannot currently use references (&) as argument types. This is due to the default argument code here and might change in the future.
* All types used in an engine API function/method must have registered console types including an ImplementConsoleTypeCasters instance for the given native C++ type. If this is missing, you will see link-time errors or compile-time errors in the templates.
* There are two exceptions:
    * U32 can be used and is treated internally like S32
    * Pointers to SimObject-derived classes can be used freely
* Do not use String for string arguments. Use "const char*". You may use Strings as return values, though (for TS: memory will be copied to evaluator stack).
* If you return "const char*", the API assumes the lifetime of the string exceeds that of the call-in. If that is not the case, you need to use Con::getReturnBuffer.
* If you return String, the API assumes the String is temporary and will automatically copy it with Con::getReturnBuffer.
* Due to the template trickery involved in the engineAPI macro system, default argument values will be constructed once during global startup (except if the compiler is smart enough to optimize the non-side-effecting constructors away). **This means that any default argument value must not use a feature of Torque that requires global ctors to have executed. Using String::EmptyString is an example of what would not work.**

Creating Call-out Points
=========================
A call-out point is an exit point from the C++ engine to the control layer (TorqueScript). This is often referred to as a callback. The main purpose of a callback is to trigger a function in script from C++ after an important piece of code has been executed. The following procedure is used to creating a callback:


In your class definition, declare the callbacks for the class with DECLARE_CALLBACK:


Example::

    protected:      
       /// @name Callbacks
       /// @{
       
       DECLARE_CALLBACK(void, onAdd, (SimObjectId ID) );

       /// @}


In your implementation file, include the engineAPI.h header::

    #include "console/engineAPI.h"

Then, use the IMPLEMENT_CALLBACK macro for each of the callbacks::

    IMPLEMENT_CALLBACK( ScriptObject, onAdd, void, ( SimObjectId ID ), ( ID ),
    	"Called when this ScriptObject is added to the system.\n"
    	"@param ID Unique object ID assigned when created (%this in script).\n"
    );

The two list arguments to the macro represent the raw argument type list ( type arg1, type arg2... ) as well as the argument call list ( arg1, arg2 ). This is needed by the macros to chain the call along. To trigger a callback in the code, invoke the given callback method by appending _callback to its name::

    bool ScriptObject::onAdd()
    {
       if (!Parent::onAdd())
          return false;
    
       // Call onAdd in script!
       onAdd_callback(getId());
       return true;
    }


Creating Types
================
Before a native C++ type can be used in the engine API, it must be registered with the console system. How this is done depends on the kind of type. For all registered types, TYPEID<type>() returns the numeric type ID of the static type. 

Creating an Object Type
--------------------------
To define a new object type for use in the control layer API, use the following procedure. For a class T, this allows to use pointers to T objects to be used in the API. Derive your class directly or indirectly from SimObject::

    class SFXAmbience : public SimDataBlock
    {


In the class interface, define a public typedef "Parent" as an alias for the parent class::

    public:
        typedef SimDataBlock Parent;


Also, in the public interface, use DECLARE_CONOBJECT. Optionally, also supply a description and category::

    DECLARE_CONOBJECT( SFXAmbience );
    DECLARE_CATEGORY( "SFX" );
    DECLARE_DESCRIPTION( "An ambient sound environment." );


Then, in the implementation file, use IMPLEMENT_CONOBJECT or one of its variants (for datablocks and netobjects)::

    IMPLEMENT_CO_DATABLOCK_V1( SFXAmbience );

Creating an Enumeration Type
------------------------------
To define a new enumeration type for use in the control layer API, use the following procedure. In the file where your native enum type is defined, include the type header::

    #include "console/dynamicTypes.h"


After the enum definition::

    /// Rolloff curve used for distance volume attenuation of 3D sounds.
    enum SFXDistanceModel
    {
       SFXDistanceModelLinear,             ///< Volume decreases linearly from min to max where it reaches zero.
       SFXDistanceModelLogarithmic,        ///< Volume halves every min distance steps starting from min distance; attenuation stops at max distance.
    };


Declare the public type bits::

    DefineEnumType( SFXDistanceModel );


In the corresponding implementation file, add the corresponding implementation detail::

    ImplementEnumType( SFXDistanceModel,
       "Type of volume distance attenuation curve.\n"
       "The distance model determines the falloff curve applied to the volume of 3D sounds over distance.\n\n"
       "@ref SFXSource_volume\n\n"
       "@ingroup SFX" )
       { SFXDistanceModelLinear, "Linear",
          "Volume attenuates linearly from the references distance onwards to max distance where it reaches zero." },
       { SFXDistanceModelLogarithmic, "Logarithmic", 
          "Volume attenuates logarithmically starting from the reference distance and halving every reference distance step from there on. "
          "Attenuation stops at max distance but volume won't reach zero." },
    EndImplementEnumType;

Note you can declare fields of this type directly::

    addField( "soundDistanceModel", TYPEID< SFXDistanceModel >(), Offset( mSoundDistanceModel, LevelInfo ), "The distance attenuation model to use." );


Be aware that the native C++ enum type used in the macros must be global (the resulting type name will be global). To use nested enum types, simply work around this with a typedef::

    typedef SFXPlayList::ELoopMode SFXPlayListLoopMode;
    DefineEnumType( SFXPlayListLoopMode );


Creating a Bitfield Type
--------------------------
To define a new bitfield type for use in the control layer API, follow the instructions for defining an enumeration type with the following macros substituted for their enumeration counterparts:

Declare the type::

    DefineBitfieldType( MaterialAnimType );


Implement the type::

    ImplementBitfieldType( MaterialAnimType,
       "The type of animation effect to apply to this material.\n"
       "@ingroup GFX\n\n")
       { Material::Scroll, "Scroll", "Scroll the material along the X/Y axis.\n" },
       { Material::Rotate, "Rotate" , "Rotate the material around a point.\n"},
       { Material::Wave, "Wave" , "Warps the material with an animation using Sin, Triangle or Square mathematics.\n"},
       { Material::Scale, "Scale", "Scales the material larger and smaller with a pulsing effect.\n" },
       { Material::Sequence, "Sequence", "Enables the material to have multiple frames of animation in its imagemap.\n" }


Immediately after you will end the implementation::

    EndImplementBitfieldType;
  
Documentation
===============
Torque 3D makes it very easy to document the code via strings written directly into the implementations. Documentation strings for engine API items use the JavaDoc tag syntax (@param, @ingroup, etc...). 

Documenting an engine function/method
----------------------------------------
Place the documentation in the DefineEngineXXX macro. If not containing a @brief, the first line (i.e. up to \n) will be taken as the function @brief and automatically split out from the doc string. This allows the coder to omit the @brief in almost all cases as the first line will generally be good enough. Write explicit @briefs where this is not the case. For functions, place them in a group by using @ingroup tag:


**Example**::

    DefineEngineFunction( strIsMatchExpr, bool, ( const char* pattern, const char* str, bool caseSensitive ), ( false ),
       "Match a pattern against a string.\n"
       "@param pattern The wildcard pattern to match against.  The pattern can include characters, '*' to match "
          "any number of characters and '?' to match a single character.\n"
       "@param str The string which should be matched against @a pattern.\n"
       "@param caseSensitive If true, characters in the pattern are matched in case-sensitive fashion against "
          "this string.  If false, differences in casing are ignored.\n"
       "@return True if @a str matches the given @a pattern.\n\n"
       "@tsexample\n"
       "strIsMatchExpr( \"f?o*R\", \"foobar\" ) // Returns true.\n"
       "@endtsexample\n"
       "@see strIsMatchMultipleExpr\n"
       "@ingroup Strings" )
    {
       return FindMatch::isMatch( pattern, str, caseSensitive );
    }


Handling overloaded functions
-------------------------------
Overloading is not currently supported by engineAPI. TorqueScript functions that have varying argument lists thus cannot be implemented with engineAPI right now.


Example::

    GuiControl::setExtent( Point2I p )
    GuiControl::setExtent( S32 width, S32 height )

These functions must remain implemented with the old ConsoleXXX macros. For documentation, these functions must be split into multiple independent functions/methods for Doxygen. This is achieved using the following procedure:


Document the original function for in-game purposes but @hide it from Doxygen::

    ConsoleMethod( GuiControl, setExtent, void, 3, 4,
       "( Point2I p | int x, int y ) Set the width and height of the control.\n\n"
       "@hide" )


Write an independent ConsoleDocFragment for each variant of the function method::

    static ConsoleDocFragment _sGuiControlSetExtent1(
       "@brief Resize the control to the given dimensions.\n\n"
       "Child controls will resize according to their layout settings.\n"
       "@param width The new width of the control in pixels.\n"
       "@param height The new height of the control in pixels.",
       "GuiControl", // The class to place the method in; use NULL for functions.
       "void setExtent( S32 width, S32 height );" ); // The definition string.
    
    static ConsoleDocFragment _sGuiControlSetExtent2(
       "@brief Resize the control to the given dimensions.\n\n"
       "Child controls with resize according to their layout settings.\n"
       "@param p The new ( width, height ) extents of the control.",
       "GuiControl", // The class to place the method in; use NULL for functions.
       "void setExtent( Point2I p );" ); // The definition string.



Handling variadic functions
-----------------------------
Variadic functions are not currently supported by engineAPI. TorqueScript functions that takes a variable number of arguments cannot be implemented with engineAPI right now.

**Example**::

    echo( string text... )

For now, these functions must remain implemented with the old ConsoleXXX macros. To document them, place the function argument prototype string first in the usage string and then include documentation for other types of functions.

**Class Function**::

    ConsoleMethod( SimSet, add, void, 3, 0,
       "( SimObject objects... ) Add the given objects to the set.\n"
       "@param objects The objects to add to the set." )

**Global Function**::

    ConsoleFunction( getRandom, F32, 1, 3,
    	"( int a=1, int b=0 ) "
    	"Get a random number between @a a and @a b.\n"
    	"@param a Lower bound on the random number.  The random number will be >= @a a.\n"
    	"@param b Upper bound on the random number.  The random number will be <= @a b.\n"
    	"@return A pseudo-random number between @a a and @a b.\n" )


Documenting an engine callback
--------------------------------
Place the documentation on the IMPLEMENT_CALLBACK macro. If not containing a @brief, the first line (i.e. up to \n) will be taken as the function @brief and automatically split out from the doc string. This allows to omit the @brief in almost all cases as the first line will generally be good enough. Write explicit @briefs where this is not the case::

    IMPLEMENT_CALLBACK( GuiControl, onActive, void, ( bool state ), ( state ),
       "Called when the control changes its activeness state, i.e. when going from active to inactive or vice versa.\n"
       "@param stat The new activeness state.\n"
       "@see isActive\n"
       "@see setActive\n"
       "@ref GuiControl_VisibleActive" );


Documenting an engine class
-----------------------------
Place the documentation either in a .txt file in Documentation/scriptDocs/docs or in the C++ implementation files using the ConsoleDocClass macro. Always use @ingroup and @brief::

    ConsoleDocClass( SFXAmbience,
       "@brief A datablock that describes an ambient sound space.\n\n"
       
       "Each ambience datablocks captures the properties of a unique ambient sound space.  A sound space is comprised of:\n"
       
       "- an ambient audio track that is played when the listener is inside the space,\n"
       "- a reverb environment that is active inside the space, and\n"
       "- a number of SFXStates that are activated when entering the space and deactivated when exiting it.\n"
       "\n"
       
       "Each of these properties is optional.\n\n"
       
       "An important characteristic of ambient audio spaces is that their unique nature is not determined by their location "
       "in space but rather by their SFXAmbience datablock.  This means that the same SFXAmbience datablock assigned to "
       "multiple locations in a level represents the same unique audio space to the sound system.\n\n"
       
       "This is an important distinction for the ambient sound mixer which will activate a given ambient audio space only "
       "once at any one time regardless of how many intersecting audio spaces with the same SFXAmbience datablock assigned "
       "the listener may currently be in.\n\n"
       
       "Each SFXAmbience instance will automatically add itself to the global SFXAmbienceSet.\n\n"
    
       "At the moment, transitions between reverb environments are not blended and different reverb environments from multiple "
       "active SFXAmbiences will not be blended together.  This will be added in a future version.\n\n"
       
       "@tsexample\n"
       "singleton SFXAmbience( Underwater )\n"
       "{\n"
       "   environment = AudioEnvUnderwater;\n"
       "   soundTrack = ScubaSoundList;\n"
       "   states[ 0 ] = AudioLocationUnderwater;\n"
       "};\n"
       "@endtsexample\n"
          
       "@see SFXEnvironment\n"
       "@see SFXTrack\n"
       "@see SFXState\n"
       "@see LevelInfo::soundAmbience\n"
       "@see Zone::soundAmbience\n"
       "@ref Datablock_Networking\n"
       "@ingroup SFX\n"
       "@ingroup Datablocks\n"
    );

Documenting a field
---------------------
Place the documentation directly on the addField usage string. The first line (i.e. up to the first \n) is taken as the @brief and showed in inspectors. The rest is only used for doc output::

    addField( "coneOutsideVolume",   TypeF32,    Offset( mConeOutsideVolume, SFXDescription ),
             "Determines the volume scale factor applied the a source's base volume level outside of the outer cone.\n"
             "In the outer cone, starting from outside the inner cone, the scale factor smoothly interpolates from 1.0 (within the inner cone) "
             "to this value.  At the moment, the allowed range is 0.0 (silence) to 1.0 (no attenuation) as amplification is only supported on "
             "XAudio2 but not on the other devices.\n\n"
             "Only for 3D sound.\n"
             "@ref SFXSource_cones" );


Documenting a variable
------------------------
Place the documentation on the Con::addVariable() call. Use @ingroup to properly associate the documentation with a group. The first line of the doc string will be taken as the @brief::

    Con::addVariable( "SFX::numSources", TypeS32, &mStatNumSources, NULL,
          "Number of SFXSources that are currently instantiated.\n"
          "@ingroup SFX" );
    

Make sure the ``Con::addVariable()`` call is within the engine init phase and will be available after the engine has started up. Don't put the call on conditional paths. If necessary, use the module system (core/module.h) for relevant initialization 

Documenting a constant
------------------------
Place the documentation on the Con::addConstant() call. Use @ingroup to properly associate the documentation with a group. The first line of the doc string will be taken as the @brief::

    Con::addConstant( "SFX::REVERB_FLAG_DECAYTIMESCALE", TypeS32, &sReverbFlagDecayTimeScale, NULL,
          "SFXEnvironment::envSize affects reverberation decay time.\n"
          "@see SFXEnvironment::flags\n\n"
          "@ingroup SFX" );

Make sure the ``Con::addConstant()`` call is within the engine init phase and will be available after the engine has started up. Don't put the call on conditional paths. If necessary, use the module system (core/module.h) for relevant initialization. 

Inserting an arbitrary piece of documentation
-----------------------------------------------
Arbitrary code documentation can be inserted using the ConsoleDoc macro::

    ConsoleDoc(
       "@defgroup MyGroup\n"
       "@brief Blabla\n\n"
       "My description.\n\n"
       "@ingroup Parent"
    );

Be aware that only one ConsoleDoc instance can be in any given .cpp file. To work around this, either place the macro instances in different namespaces or use the ConsoleDocFragment class directly::

    static ConsoleDocFragment _sGuiControlSetExtent1(
       "@fn void GuiControl::setExtent( int width, int height )\n"
       "@brief Resize the control to the given dimensions.\n\n"
       "Child controls will resize according to their layout settings.\n"
       "@param width The new width of the control in pixels.\n"
       "@param height The new height of the control in pixels." );
    
    static ConsoleDocFragment _sGuiControlSetExtent2(
       "@fn void GuiControl::setExtent( Point2I p )\n"
       "@brief Resize the control to the given dimensions.\n\n"
       "Child controls with resize according to their layout settings.\n"
       "@param p The new ( width, height ) extents of the control." );
               

You can also place a fragment inside a class::

    static ConsoleDocFragment _sFragment(
       "doc",
       "className", //NULL to place globally
       "definition" ); //optional

Important Notes
=================
Things to watch out for:

* Put two newlines after @brief, i.e. "@brief Text\n\n"
* Put two newlines at the end of a paragraph, i.e. "My paragraph.\n\n"
* Put two newlines before @tsexample.
* Put two newlines to separate a @see from a @ref. Otherwise Doxygen will put the @ref on the same line as the @see which is visually unpleasing.
* Put @ingroup at the end of doc strings.
* Put datablocks in two groups; first in the group that the non-datablock object is in (e.g. PlayerData should be in the same group with Player) and second in the "Datablocks" group
* Use @tsexample and @endtsexample instead of @code and @endcode


Conclusion
===========
After reading through this document you should a solid understanding of how the C++ engine communicates with the script layer. This is how the Torque team extends the engine and generates its official documentation. You should adhere to these standards if you wish to maintain stability while extending the engine. 
