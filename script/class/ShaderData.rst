ShaderData
==========

Special type of data block that stores information about a handwritten shader.

Inherit:
	:doc:`SimObject`

Description
-----------

To use hand written shaders, a ShaderData datablock must be used. This datablock refers only to the vertex and pixel shader filenames and a hardware target level. Shaders are API specific, so DirectX and OpenGL shaders must be explicitly identified.

Example::

	// Used for the procedural clould system
	singleton ShaderData( CloudLayerShader )
	{
	   DXVertexShaderFile   = "shaders/common/cloudLayerV.hlsl";
	   DXPixelShaderFile    = "shaders/common/cloudLayerP.hlsl";
	   OGLVertexShaderFile = "shaders/common/gl/cloudLayerV.glsl";
	   OGLPixelShaderFile = "shaders/common/gl/cloudLayerP.glsl";
	   pixVersion = 2.0;
	};

Methods
-------

.. cpp:function:: void ShaderData::reload()

	Rebuilds all the vertex and pixel shader instances created from this ShaderData .

	Example::

		// Rebuild the shader instances from ShaderData CloudLayerShader
		CloudLayerShader.reload();

Fields
------

.. cpp:member:: string  ShaderData::defines

	String of case-sensitive defines passed to the shader compiler. The string should be delimited by a semicolon, tab, or newline character.

	Example::

		singleton ShaderData( FlashShader )
		{
		DXVertexShaderFile   = "shaders/common/postFx/flashV.hlsl";
		DXPixelShaderFile    = "shaders/common/postFx/flashP.hlsl";
		
		 //Define setting the color of WHITE_COLOR.defines = "WHITE_COLOR=float4(1.0,1.0,1.0,0.0)";
		
		pixVersion = 2.0
		}

.. cpp:member:: filename  ShaderData::DXPixelShaderFile

	Path to the DirectX pixel shader file to use for this ShaderData . It must contain only one program and no vertex shader, just the pixel shader. It can be either an HLSL or assembly level shader. HLSL's must have a filename extension of .hlsl, otherwise its assumed to be an assembly file.

.. cpp:member:: filename  ShaderData::DXVertexShaderFile

	Path to the DirectX vertex shader file to use for this ShaderData . It must contain only one program and no pixel shader, just the vertex shader.It can be either an HLSL or assembly level shader. HLSL's must have a filename extension of .hlsl, otherwise its assumed to be an assembly file.

.. cpp:member:: filename  ShaderData::OGLPixelShaderFile

	Path to an OpenGL pixel shader file to use for this ShaderData . It must contain only one program and no vertex shader, just the pixel shader.

.. cpp:member:: filename  ShaderData::OGLVertexShaderFile

	Path to an OpenGL vertex shader file to use for this ShaderData . It must contain only one program and no pixel shader, just the vertex shader.

.. cpp:member:: float  ShaderData::pixVersion

	Indicates target level the shader should be compiled. Valid numbers at the time of this writing are 1.1, 1.4, 2.0, and 3.0. The shader will not run properly if the hardware does not support the level of shader compiled.

.. cpp:member:: bool  ShaderData::useDevicePixVersion

	If true, the maximum pixel shader version offered by the graphics card will be used. Otherwise, the script-defined pixel shader version will be used.
