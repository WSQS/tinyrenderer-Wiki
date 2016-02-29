# Permanently under construction

This page is not meant to be a FAQ section; instead I show here several examples of bugs me and my students were able to fix *without* looking into the source code, solely by observing things in the images. No made up situations, real renderings, real student pain is shown. The description of bugs is kept to a bare minimum, these images speak for themselves.

# Triangle rasterization: line sweeping

Frequent bug: while sorting by y-coordinate, the vertices are sorted, but the data coming with the vertices is not.

### Gouraud shading, forgot to sort intensities
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/line_sweeping/flat_shading_bad_sort.png)

### Z-buffer, forgot to sort z coordinates

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/line_sweeping/zbuffer_bad_sort.jpg)

### Horizontal sort of two vertices splitting the triangle

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/line_sweeping/bad_split_flip.jpg)


### Here are two examples of rounding errors creating holes in/between triangles:

Bad y interpolation while sweeping the line:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/line_sweeping/rounding/interpolated_y_coordinate.png)

The vertices were not casted to int prior to filling:
![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/line_sweeping/rounding/double_vertices_wold_be_better_to_cast_to_int.png)

# Bad data parsing

Forgot to decrement indices of vertices (remember in wavefront obj indices are starting from 1, not 0)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/parsing/obj_decrement.png)


Few broken reads of texture coordinates, notice that all the fan of triangles incident to a vertex is messy, thus the vertex is broken:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/parsing/corrupted_vt_read.jpg)


All "v", "vt" and "vn" lines are read in the same array, thus effectively killing any sense in the model. Very roundish shape of the rendering gives the idea about "vn" confused with "v". Prior to the bugfix and after:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/parsing/vt_vn_interpreted_as_v_as_well.jpg)


# Specular map

Frequent bug, anything elevated to the zero power equals to one:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/specular/power0.jpg)

# Texturing

This one needs a circular permutation of barycentric coordinates in the uv-interpolation:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/uv/barycentric_coordinates_circular_permutation.jpg)

The texture needs to be vertically flipped:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/uv/texture_flip.jpg)

While visually ressembling to the above one, this one is completely different (why?). Here the student used xy pixel coordinates (instead of uv) to fetch a color from the texture :

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/a7c5da19378566533bd780918fc66323226467cf/troubleshooting/uv/xy_and_not_uv_read_from_texture.jpg)

# Lighting

Light direction (instead of view direction) was used for backface culling. Prior and after bugfix.

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/troubleshooting/light/bad_backface_culling.png)


Broken normal map reading, before and after. [0,255]^3 RGB were brought to XYZ living in [0,2]^3 and not [-1,1]^3.

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/troubleshooting/light/broken_normal_map.jpg)