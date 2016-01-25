In this series of articles, I want to show the way OpenGL works by writing its clone (a much simplified one). Surprisingly enough, I often meet people who cannot overcome the initial hurdle of learning OpenGL / DirectX. Thus, I have prepared a short series of lectures, after which my students show quite good renderers.

So, the task is formulated as follows: using no third-party libraries (especially graphic ones), get something like this picture:

![](http://www.loria.fr/~sokolovd/cg-course/img/7ff5d9e311.png)

_Warning: this is a training material that will loosely repeat the structure of the OpenGL library. It will be a software renderer. **I do not want to show how to write applications for OpenGL. I want to show how OpenGL works.** I am deeply convinced that it is impossible to write efficient applications using 3D libraries without understanding this._

I will try to make the final code about 500 lines. My students need 10 to 20 programming hours to begin making such renderers. At the input, we get a test file with a polygonal wire + pictures with textures. At the output, we’ll get a rendered model. No graphical interface, the program simply generates an image.


Since the goal is to minimize external dependencies, I give my students just one class that allows working with [TGA](http://en.wikipedia.org/wiki/Truevision_TGA) files. It’s one of the simplest formats that supports images in RGB/RGBA/black and white formats. So, as a starting point, we’ll obtain a simple way to work with pictures. You should note that the only functionality available at the very beginning (in addition to loading and saving images) is the capability to set the color of one pixel.

There are no functions for drawing line segments and triangles. We’ll have to do all of this by hand. I provide my source code that I write in parallel with students. But I would not recommend using it, as this doesn’t make sense. The entire code is available on github, and here you will find the source code I give to my students.



output.tga should look something like this:
![](http://www.loria.fr/~sokolovd/cg-course/img/2d3b12170b.png)