Introduction to TorqueScript
******************************

What is TorqueScript?
=======================

TorqueScript (TS) is a proprietary scripting language developed specifically for Torque technology. The language itself is derived from the scripting used for Tribes 2, which was the base tech Torque evolved from. Scripts are written and stored in .cs files, which are compiled and executed by a binary compiled via the C++ engine (.exe for Windows or .app OS X). The CS extension should not be confused with C# files.

The CS extension stands for "C Script," meaning the language resembles C programming. Though there is a connection, TorqueScript is a much higher level language and is easier to learn than standard C or C++. 

Basic Usage
=============

Like most other scripting languages, such as Python or Java Script, TorqueScript is a high-level programming language interpreted by Torque 3D at run time. Unlike C++, you can write your code in script and run it without recompiling your game. 

All of your interfaces can be built using the GUI Editor, which saves the data out to TorqueScript. The same goes for data saved by the World Editor or Material Editor. Most of the editors themselves are C++ components exposed and constructed via TorqueScript. 

More importantly, nearly all of your game play programming will be written in TorqueScript: inventory systems, win/lose scenarios, AI, weapon functionality, collision response, and game flow. All of these can be written in TorqueScript. The language will allow you to rapidly prototype your game without having to be a programming expert or perform lengthy engine recompilation.

Scripting vs Engine Programming 
=================================

As mentioned above, TorqueScript is comprised of the core C++ objects needed to make your game. For example, you will use the PlayerData structure to create player objects for your game. This structure was written in C++::

	struct PlayerData: public ShapeBaseData {
		typedef ShapeBaseData Parent;
		bool renderFirstPerson;    ///< Render the player shape in first person


		mass = 9.0f;         // from ShapeBase
		drag = 0.3f;         // from ShapeBase
		density = 1.1f;      // from ShapeBase

Instead of having to go into C++ and create new PlayerData objects or edit certain fields (such as mass), PlayerData was exposed to TorqueScript::

	datablock PlayerData(DefaultPlayerData)
	{
		renderFirstPerson = true;

		className = Armor;
		shapeFile = "art/shapes/actors/gideon/base.dts";

		mass = 100;
		drag = 1.3;
		maxdrag = 0.4;

		// Allowable Inventory Items
		maxInv[Pistol] = 1;
		maxInv[PistolAmmo] = 50;
	};

If you want to change the name of the object, the mass, the inventory, or anything else, just open the script, make the change, and save the file. When you run your game, the changes will immediately take effect. Of course, for this example you could have used the in-game Datablock Editor, but you should get the point. TorqueScript is the first place you should go to write your game play code.

Getting Started
=================

Like the rest of the documentation, the TorqueScript guides should be read in order (from top to bottom in the table of contents). This means you should start by reading the Syntax Guide. If you have never written TorqueScript before, **DO NOT SKIP** the Syntax Guide.

The docs in the **Simple Tutorials** will provide you with working code meant to show off syntax and basic TorqueScript structures. This is where you will create, edit, debug, and execute your first scripts.

Finally, the **Advanced Tutorials** section will walk you through complex functionality and algorithms. These tutorials make full use of Torque 3D's editors, networking structure, input system, and TorqueScript. These examples will even get into game play mechanics.

If you simply need a quick reference while writing scripts, you can read through the **TorqueScript Reference Guide**.
