Lighting Overview
********************

Introduction
=============
The lighting system in Torque3D is set up to support Shader Model 1.0 as a minimum. While the more advanced features will requires Shader Model 3.0, this will provide a balance between users with older and newer graphics cards. The lighting system provides for the use of shadow mapping techniques and deferred rendering.

This guide will give you a detailed analysis of the classes that create the functionality of Torque 3D's lighting system while showing you how some of them are used. In addition to the Source Code Tour (Lighting Source Code Tour - TODO Internal Link) and Light Manager Usage (Using the LightManager Class - TODO Internal Link), there are detailed function definitions for the following classes.

Basic Light Manager
====================
The Basic Light Manager (**class BasicLightManager**) requires that the graphics card have at least Shader Model 1.0. It is an override of the abstract class LightManager to provide a simple lighting solution to lower end graphics cards. Although it is targeted to lower end graphics cards, it does still support shadowing techniques.

Advanced Light Manager
=======================
The Advanced Light Manager (**class AdvancedLightManager**) requires that the graphics card support at least Shader Model 3.0. Much like the **BasicLightManager**, it is an override of the **abstract class LightManager**, however, it will provide a more sophisticated lighting solution for higher end graphics cards. The Advanced Light Manager supports multiple adaptations of shadow mapping techniques such as Dual Paraboloid and Cube Shadow maps.

The LightInfo Class
=====================
This is the base light information class that will be tracked by the engine. It basically contains a bounding volume and methods to interact with the rest of the system (for example, setting the GFX fixed function lights).

The LightInfoEx Class
=======================
This is the base class for extended lighting info that lies outside of the normal info stored in LightInfo. An example of where this class will be used is for creating **LightMapParams** and **ShadowMapParams**.

SceneLightingInterface
========================
The SceneLightingInterface object is responsible for returning **PersistChunk** and **ObjectProxy** classes for the lighting system to use. The **SceneLightingInterface** is used by the **AvailableSLInterfaces** to register systems to itself, such as "**class blInteriorSystem**".

AvailableSLInterfaces
======================
**AvailableSLInterfaces** makes use of the **SceneLightingInterface** to register lighting interfaces. By default, the BasicLightManager will register an instance of the "**blInteriorSystem**" and "**blTerrainSystem**" in its constructor.

The ShadowManager Base Class
=============================
The **ShadowManager** is a base class to be extended later by a more sophisticated shadow manager, such as the class **ShadowMapManager**. While the **ShadowManager** does not currently contain any pure virtual functions, creating an instance of **ShadowManager** will not manage any shadows.

The ShadowMapManager Class
============================
The **ShadowMapManager** is a full extension of the **ShadowManager** where the **SceneManager** will be notified to add the rendering function ("_onPreRender") to its list. The rendering function will then call the render function from its currently set shadow map pass.
