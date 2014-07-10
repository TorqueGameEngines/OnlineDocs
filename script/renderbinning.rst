Render Binning
==============

The render sorting and batching system. 

Classes
-------

.. toctree::
	:maxdepth: 1

	class/RenderBinManager
	class/RenderGlowMgr
	class/RenderImposterMgr
	class/RenderMeshMgr
	class/RenderObjectMgr
	class/RenderOcclusionMgr
	class/RenderParticleMgr
	class/RenderPassManager
	class/RenderPassStateBin
	class/RenderPassStateToken
	class/RenderPrePassMgr
	class/RenderTerrainMgr
	class/RenderTexTargetBinManager
	class/RenderTranslucentMgr

Description
-----------

In Torque we use a binning system to do the initial ordering and batching of rendering operations.

When rendering a pass is made thru all the game objects visible in the scene. The game objects will each submit one or more RenderInst to the RenderPassManager. The pass manager maintains an ordered list of RenderBinManagers each which get a chance to consume the RenderInst.

After all the game objects have been processed the RenderPassManager lets each bin sort then render the RenderInsts they contain.

Currently from script you can only define and change the order of the bins in the RenderPassManager. To create new types of bins or add new rendering methods you will need C++ source access.

.. seealso::

	The file core\scripts\client\renderManager.cs.

Enumeration
-----------

.. cpp:member:: enum  RenderTexTargetSize

	What size to render the target texture. Sizes are based on the Window the render is occuring in.

	:param windowsize: Render to the size of the window.
	:param windowsizescaled: Render to the size of the window, scaled to the render target's size.
	:param fixedsize: Don't scale the target texture, and render to its default size.

Variables
---------

.. cpp:member:: bool  RenderOcclusionMgr::debugRender  [static, inherited]

	A debugging feature which renders the occlusion volumes to the scene.

.. cpp:member:: bool  RenderTerrainMgr::renderWireframe  [static, inherited]

	Used to enable wireframe rendering on terrain for debugging.
