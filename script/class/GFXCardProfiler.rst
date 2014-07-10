GFXCardProfiler
===============

Provides a device independent wrapper around both the capabilities reported by the card/drivers and the exceptions recorded in various scripts.

Description
-----------

The GFXCardProfiler provides a device independent wrapper around both the capabilities reported by the card/drivers and the exceptions recorded in various scripts.

The materials system keeps track of most caps-related rendering optimizations and/or workarounds, but it is occasionally necessary to expose capability information to higher level code (for instance, if some feature depends on a specific subset of render functionality) or to keep track of exceptions.

The proper way to fix this is to get the IHV to release fixed drivers and/or move to a single consistent rendering path that works. Of course, when you're releasing a game, especially on a timeline (or with a less than infinite budget) this isn't always a valid solution.

It's also often convenient to be able to tweak performance/detail settings based on the identified card type.

GFXCardProfiler addresses both these needs by providing two data retrieval methods and a generic interface for querying capability strings.

.. note::

	The GFXCardProfiler is at heart a system for implementing WORKAROUNDS. It is not guaranteed to work in all cases. The capability strings it responds to are specific to each implementation. You should be EXTREMELY careful when working with this functionality. When used in moderation it can be a project-saver, but if used to excess or without forethought it can lead to complex, hard-to-maintain code.

The first data retrieval method that the GFXCardProfiler supports is a card-specific capability query. This is implemented by each subclass. In the case of DirectX, this means using the built-in capability query. For OpenGL or other APIs, more exotic methods may be necessary. The goal of this method is to retrieve some reasonable defaults that can be overridden later if necessary.

The second data retrieval method is script based. In ./profile a collection of script files are stored. They are named in one of the forms:

    Renderer.cs
    Renderer.VendorString.CardString.cs
    Renderer.VendorString.CardString.cs
    Renderer.VendorString.CardString.VersionString.card-specific

These files are found and executed from most general to most specific. For instance, say we're working in the D3D renderer with an nVidia GeForce FX 5950, running driver version 53.36. The following files would be found and executed:

    D3D.cs
    D3D.nVidia.cs
    D3D.nVidia.GeForceFX5950.cs
    D3D.nVidia.GeForceFX5950.5336.cs

The general rule for turning strings into filename parts is to strip all spaces and punctuation. If a file is not found, no error is reported; it is assumed that the absence of a file means all is well.

Several functions are made available to allow simple logic in the script functions (for instance, to enable a workaround for a given range of driver versions). They are:

* GFXCardProfiler::getRenderer()
* GFXCardProfiler::getVendor()
* GFXCardProfiler::getCard()
* GFXCardProfiler::getVersion()

In addition, specific subclasses may expose other values (for instance, chipset IDs). These are made available as static members of the specific subclass. For instance, a D3D-specific chipset query may be made available as GFXD3DCardProfiler::getChipset().

Finally, once a script file has reached a determination they may indicate their settings to the GFXCardProfiler by calling GFXCardProfiler::setCapability(). For instance,

::

	// Indicate we can show the color red.
    GFXCardProfiler::setCapability("supportsRed", true);

GFXCardProfiler may be queried from script by calling GFXCardProfiler::queryProfile() - for instance::

	GFXCardProfiler::queryProfile("supportsRed", false); // Query with default.