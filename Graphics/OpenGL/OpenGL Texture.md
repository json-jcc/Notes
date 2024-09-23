# OpenGL Texture





## texture buffer

只能通过 texelFetch 访问

 







## mipmap

只有部分类型的texture可以拥有mipmap，mipmap指同一个图形的较低分辨率的版本，opengl有自动生成mipmap的函数，该函数会根据你提供的原始图像生成mipmap，生成多少层也由你提供的参数决定



对于超过级别0的每个mipmap级别，其大小都会减少一半，并四舍五入。因此，如果具有二维图像的纹理的基本mipmap级别为67x67，则mipmap级别1中的图像大小为33x33。对于级别2，它们将为16x16。依此类推。



当所有尺寸均为1时，mipmap链停止；那是最大的mipmap级别。级别索引值的“最大值”，因为基本级别从0开始。   