## Pipeline

+ **Vertex Specification**

  + Vertex Rendering

+ **Vertex Processing**

  + ***Vertex Shader***

  + Tessellation

    + ***Tessellation Control Shader***
    + Tessellation Primitive Generator

    + ***Tessellation Evaluation Shader***

  + ***Geometry Shader***

+ **Vertex Post-Processing**

  + Transform Feedback
  + Primitive Assembly
  + Clipping
  + Face Culling

+ **Rasterization**

+ **Fragment Processing**

  + ***Fragment Shader***

+ **Per-Sample Operations (normal)**

  + Pixel Ownership Test ($)
  + Scissor Test ($)
  + ***Fragment Shader***
  + Alpha To Coverage Operations
  + Alpha Test (RGBA only)

  + Stencil Test (*)
  + Depth Test (*)
  + Occlusion Query (*)
  + Blending
  + SRGB Conversion
  + Dithering
  + Logical Operation
  + Additional Multisample Fragment Operations

+ **Per-Sample Operations (early enabled)**

  + Pixel Ownership Test ($)
  + Scissor Test ($) 
    + 剪裁测试，剪裁框以外的像素对应的片段全部丢弃
  + Stencil Test (*)
    + 模板测试，
  + Depth Test (*)
    + 深度测试，
  + Occlusion Query (*)
  + ***Fragment Shader***
  +  
  + Alpha Test (RGBA only)

  + Blending
  + SRGB Conversion
  + Dithering 不可干预
  + Logical Operation
  + Additional Multisample Fragment Operations