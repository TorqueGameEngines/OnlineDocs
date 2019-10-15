Assets
========

With Torque3D 4.0, the engine now utilizes an assets-based system to manage content for your game. 
Below goes into the high-level breakdown of the elements of it and how they work.

Modules
------------
Modules are the main organizational structure for assets. They act as containers for assets so you
can quickly parse them by group. Modules are defined via a module definition file ending with the 'module' extension and companion script file.

For example, we have here TestModule.module:

.. code-block:: xml

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

Assets
------------
An 'Asset' is any specific chunk of content. This can be a singular file, such as an image, or multiple related files together,
like a GUI having a gui file and script file, or a level having the level script file, decal cache, postFX settings, forest object cache, etc.

The Assets system is a system by which said content can be registered into a database for easy loading, utilization, and referencing.
This is done via the use of Asset Definitions, which is a type of metadata. When modules are loaded, they scan
their respective directory and find any asset metadata files within and register them with the Asset Database. This enables them
to be easily referenced via the paradigm of <ModuleName>:<AssetName>. If referenced in this way, the engine will automatically find, reference
and load the asset, handling the file paths and resource management automatically. Different asset types have different Asset Definitions,
but they largely follow a similar structure:

.. code-block:: xml

<LevelAsset
    canSave="true"
    canSaveDynamicFields="true"
    AssetName="TestLevel"
    LevelFile="TestLevel.mis"
    LevelName="Test Level"
    LevelDescription="A simple test level."
    VersionId="1" />

The most important parameter is the AssetName, which is used in combination with it's owner module to formulate an
AssetID. This, referened above as <ModuleName>:<AssetName> when referencing assets and it will handle the referencing 
and loading behavior automatically