Lighting Source Code Tour
**************************

Introduction
===============
This document will explain the source code folders and files that make up Torque 3D's lighting system.

The Lighting Core
===================
You can find the core Lighting files in engine/lighting. Most of the classes in these files will be derivatives of more sophisticated types. For example, the class LightManager from engine/lighting/lightManager.h is the derivative of AdvancedLightManager from engine/lighting/advanced/advancedLightManager.h.

**Key Classes**

* **LightInfoEx :** Located in engine/lighting/lightInfo.h 
This is the base class for extended lighting info that lies outside of the normal info stored in LightInfo.
* **LightInfo :** Located in engine/lighting/lightInfo.h 
This is the base light information class that will be tracked by the engine. Should basically contain a bounding volume and methods to interact with the rest of the system.
* **ISceneLight :** Located in engine/lighting/lightInfo.h 
When the scene is queried for lights, the light manager will get this interface to trigger a register light call.
* **AvailableSLInterfaces :** Located in engine/lighting/lightingInterfaces.h 
List of available "systems" that the lighting system can use.
* **LightManager :** Located in engine/lighting/lightManager.h 
This is the base class for extending a lighting manager to support lighting features.
* **ShadowManager :** Located in engine/lighting/shadowManager.h 
This is the base class for extending a shadow manager to support more advanced shadowing techniques such as shadow maps.

Basic Lighting
===============
The basic lighting system that is created in Torque3D requires at least Shader Model 1.0. Much like the advanced lighting code, the basic lighting system is an override of already created classes from the lighting core (engine/lighting) that resides in engine/lighting/basic.

**Key Classes**

* **BasicLightManager :** Located in engine/lighting/basic/basicLightManager.h
The BasicLightManager is an override of the **LightManager** that will provide a lighting system for low end cards, it only requires shader model 1.0.

* **BasicSceneObjectLightingPlugin :** Located in engine/lighting/basic/BasicSceneObjectLightingPlugin.h
A **BasicSceneObjectLightingPlugin** is an override of the **SceneObjectLightingPlugin** that is used by the **BasicLightManager** during it's **_onPreRender** function for updating shadow plugins.


Advanced Lighting
==================
Torque3D takes advantage of Shader Model 3.0 to allow advanced lighting technqiues. The source code in engine/lighting/advanced is an override of already created classes from the lighting core (engine/lighting) to implement these techniques.

**Key Classes**

* **AdvancedLightingFeatures :** Located in engine/lighting/advanced/advancedLightingFeatures.h
    The **AdvancedLightingFeatures** class provided static methods for registering and unregistering features to the Feature Manager (**FeatureMgr**). When the function **registerFeatures** is scalled it will features related to lighting based upon the **GFXFormat** passed into the function. These features are defined in "Engine/source/materials/materialFeatureTypes.h" and have the prefix "**MFT_**".

* **AdvancedLightManager :** Located in engine/lighting/advanced/advancedLightManager.h
    The **AdvanceLightManager** is an override of **LightManager** that provides a setup for the deferred rendering system. **AdvanceLightManager** requires at least shader model 3.0.


Common Lighting Classes
========================
Common is a place where classes that do not particularly fit in one designated area, such as advanced or lighting. The are not considered core classes of the lighting system either. In here you will find classes that will be used to assist in implementing features for the lighting system.

**Key Classes**

* **ShadowBase :** Located in engine/lighting/common/shadowBase.h
The **ShadowBase** class is an abstract class containing all pure virtual functions that will be overwritten by the shadow technique using them.

* **BlobShadow :** Located in engine/lighting/common/blobShadow.h
A **BlodShadow** is one of the basic ways you may use the **ShadowBase** class. The **BlobShadow** is just a shadow based upon a radius.

* **LightMapParams :** Located in engine/lighting/common/lightMapParams.h
The **LightMapParams** is an override of the **LightInfoEx** from the lighting core. Most "**LightShadowMap**" based classes will use **LightMapParams** in their render function to determine if it should use light mapped geometry. As **LightMapParams** are a super class of **LightInfoEx**, they will be grabbed by LightInfo's "**getExtended**" function as a parameter type.


Shadow Maps
=============
There are a wide range of shadow maps available in Torque3D, such as the Paraboloid Shadow Map. This folder contains a common base class for many shadow maps to override (LightShadowMap) and also an override of the ShadowManager class from the lighing core folder that is named "ShadowMapManager".

**Key Classes**

* **ShadowMapManager :** Located in engine/lighting/shadowMap/shadowMapManager.h
The **ShadowMapManager** is used to render a shadow map pass via its onPreRender function that is triggered by a signal of the SceneGraph.

* **LightShadowMap :** Located in engine/lighting/shadowMap/lightShadowMap.h
Represents everything Torque 3D needs to render a shadow map for one light.

* **DualParaboloidLightShadowMap :** Located in engine/lighting/shadowMap/dualparaboloidLightShadowMap.h
The **DualParaboloidLightShadowMap** class uses the Dual Paraboloid shadow mapping technique and is an override of the **ParabolidLightShadowMap** class, which is an override of the **LightShadowMap**.



