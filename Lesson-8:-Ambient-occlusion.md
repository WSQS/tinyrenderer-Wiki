# Work in progress

In previous lectures we used local illumination model. In other words, for computing illumination of a current pixel we did not take into account its neighbors. [Phong reflection model](https://en.wikipedia.org/wiki/Phong_reflection_model) is a famous example of such approach:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/e3720a5dfedc49edb0bf70f8bc64204a.png)

In this model final illumination intensity for a point is a sum of three components: ambient intensity, constant for all points in the scene, diffuse and specular highlights depending on normal vectors. Wait a minute, why did he choose **constant** ambient component?

# Second attempt in the global illumination: ambient occlusion

Well, I was not 100% right: we did use a bit global illumination when we computed shadow mapping. Let us check another possibility to improve our renders (note that one does not exclude another!). Here is an example where I used only ambient component of the Phong reflection model:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/45d82ad9f666f7068488dc3f1e5c9da1.png)

**No diffuse component, no specular. Ambient only, however it is easy to see that I did not choose it to be constant.** Okay, the problem is stated as follows: let us ambient intensity for each point of our scene. When we previously supposed constant ambient illumination, it means that we supposed our scene so nice that all light was reflected everywhere equally. A bit strong hypothesis that is. Of course, it was made back in the old days where computing power was severely limited. Nowadays, we can spend a bit more to get more realistic images. Global illumination is more expensive than the local is. Recall that for shadow mapping we were forced to do two-passes rendering, thus roughly dividing our FPS by 2. 

# Brute force attempt

The source code is available [here](https://github.com/ssloy/tinyrenderer/tree/631386c5ab1987d4cfa097e8f89894cadd593c2d). Let us suppose that our object is surrounded by a hemisphere, emitting light uniformly (cloudy sky). Then let us choose randomly, say, a thousand points at the hemisphere, render the object thousand times and to compute what parts of the model were visible.

**Exercise:** Do you know hot to choose **uniformly** a thousand points on a (hemi-)sphere? Something like this:

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/48b9ff4834579809cc61362360995b98.png)

If we simply choose randomly a longitude and a latitude, we will obtain an accumulation of points near the poles, thus breaking our assumption on uniform lighting of the sky. [Check the answer](http://mathworld.wolfram.com/SpherePointPicking.html).

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/d6393412463267f66a15c48e2816b5cc.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/05c950df6f1b4bac904bc309068ba260.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/5ef7454c7294416fa7fa3b80c3663a71.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/6031c8b2ccd84e2d8e15584a3b91c8a2.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/1ba93fa5a48646e2a9614271c943b4da.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/ea0db451f6934992a7a4a04f6dbe0bd8.png)

![](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/08-ambient-occlusion/feceed3f2a964e2fb79926a167f15500.png)