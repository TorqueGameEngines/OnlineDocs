TSShapeConstructor - TODO
**************************

Introduction
===============

Terminology
=============

Example 1: Adding a Collision Mesh To an Existing Shape
=========================================================

Example 2: Adding a Mesh From an Existing DTS File
====================================================

Example 3: Auto-loading animations
======================================

Example 4: Splitting COLLADA animations
==========================================

Example 5: Rigid-body Player Character
=========================================

TSShapeConstructor Commands
==============================

Miscellaneous
----------------

dumpShape([string])
^^^^^^^^^^^^^^^^^^^^^

saveShape(string)
^^^^^^^^^^^^^^^^^^

Nodes
----------

getNodeCount()
^^^^^^^^^^^^^^^^^^
getNodeIndex(string)
^^^^^^^^^^^^^^^^^^^^^^^

getNodeName(S32)
^^^^^^^^^^^^^^^^^^

getNodeParentName(S32)
^^^^^^^^^^^^^^^^^^^^^^^^^

getNodeChildCount(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^
getNodeChildName(string, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getNodeObjectCount(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getNodeObjectName(string, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getNodeTransform(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

setNodeTransform(string, string, [string])
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

renameNode(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
addNode(string, string, [string])
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeNode(string)
^^^^^^^^^^^^^^^^^^^^

Objects
---------

getObjectCount()
^^^^^^^^^^^^^^^^^^
getObjectName(S32)
^^^^^^^^^^^^^^^^^^
getObjectNode(string)
^^^^^^^^^^^^^^^^^^^^^^^
setObjectNode(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

renameObject(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeObject(string)
^^^^^^^^^^^^^^^^^^^^^^

Meshes
--------

getMeshCount(string)
^^^^^^^^^^^^^^^^^^^^^^

getMeshname(string, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^

setMeshSize(string, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^

getMeshType(string)
^^^^^^^^^^^^^^^^^^^^^

setMeshType(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getMeshMaterial(string)
^^^^^^^^^^^^^^^^^^^^^^^^^

setMeshMaterial(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

addMesh(string, string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeMesh(string)
^^^^^^^^^^^^^^^^^^^

AutoBillboards
-----------------

addAutoBillboard(S32, S32, S32, S32, S32, bool, F32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeAutoBillboard(S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Sequences
-----------

getSequenceCount()
^^^^^^^^^^^^^^^^^^^^^

getSequenceIndex(S32)
^^^^^^^^^^^^^^^^^^^^^^

getSequenceName(S32)
^^^^^^^^^^^^^^^^^^^^^^^

getSequenceSource(S32)
^^^^^^^^^^^^^^^^^^^^^^^^

getSequenceFrameCount(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getSequencePriority(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

setSequencePriority(string, F32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getSequenceCyclic(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

setSequenceCyclic(string, bool)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getSequenceBlend(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^

setSequenceBlend(string, bool, string, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

getSequenceGroundSpeed(string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
setSequenceGroundSpeed(string, string, [string])
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

renameSequence(string, string)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

addSequence(string, string, [S32], [S32]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeSequence(string)
^^^^^^^^^^^^^^^^^^^^^^^^^

getTriggerCount(string)
^^^^^^^^^^^^^^^^^^^^^^^^^

getTrigger(string)
^^^^^^^^^^^^^^^^^^^

addTrigger(string, S32, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

removeTrigger(string, S32, S32)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Conclusion
============
