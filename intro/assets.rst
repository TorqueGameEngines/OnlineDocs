Assets
========

With Torque3D 4.0, the engine now utilizes an assets-based system to manage content for your game. 
Below goes into the high-level breakdown of the elements of it and how they work.

Modules
------------
Modules are the main organizational structure for assets. They act as containers for assets so you
can quickly parse them by group. Modules are defined via a module definition file ending with the 'module' extension and companion script file.

For example, we have here TestModule.module:

.. code-block:: rst
  <ModuleDefinition
    ModuleId="TestModule"
    VersionId="1"
    Description="A test module"
    ScriptFile="TestModule.cs"
    CreateFunction="create"
    DestroyFunction="destroy"
    Group="Game">
    <DeclaredAssets
      canSave="true"
      canSaveDynamicFields="true"
      Extension="asset.taml"
      Recurse="true" />
  </ModuleDefinition>

The primary parameters to focus on would be:

  * ModuleId: The name of the module when searching and utilizing assets
  * ScriptFile: Companion script file that can be utilized for extra loading/unloading management behavior
  * CreateFunction: Function called in companion script file upon module being created
  * DestroyFunction: Function called in companion script file upon module being destroyed
  * Group: What group this module is part of. Largely utilized for selectively loading sets of modules like 'Core', 'Game' or 'Tools'
  * DeclaredAssets: Subelement that defines the file extension to automatically parse upon load to register assets to this module
