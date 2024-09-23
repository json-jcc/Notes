# Framebuffer

## default framebuffer

default framebuffer 最多包含4个 color buffer，分别为：

+ GL_FRONT_LEFT
+ GL_FRONT_RIGHT
+ GL_BACK_LEFT
+ GL_BACK_RIGHT



前缓冲包含前左，前右缓冲。

后缓冲包含后左，后右缓冲。



左缓冲一定存在，右缓存只有特定显卡支持，用来配合完成3D可视化。

前缓冲一定存在，后缓冲用来配合双缓冲技术。



双缓冲技术激活的情况下，若前缓冲的左缓冲被激活，后缓冲也会对应激活其左缓冲，右缓冲同理。



一般来说，前缓冲用来显示，后缓冲用来渲染，每次渲染完成后交换缓存即可。

不建议读取和渲染前缓冲区



The default framebuffer can also contain an accumulation buffer, which can be used to perform certain computations when rendering.

## ownership test

​	**像素所有权测试，因 *default framebuffer* 由 *opengl* 的外部资源（例如*glew*）管理，因此其中某些特定的像素不属于 *opengl* 的管辖，所以在 *pipeline* 到达这一阶段时，会将针对这些像素的片段丢弃。**

​	**该测试仅对 *default framebuffer* 有意义，其他 *framebuffer object* 中的片段将会全部通过该测试。**



像素是显卡资源，opengl可以获得向某些像素填写的权限。



如果第一个窗口被第二个窗口遮挡，那么第一个窗口被遮挡掉的部分的像素权限将不属于opengl，无法通过所有权测试，原本覆盖这些像素的片段都将被丢弃。