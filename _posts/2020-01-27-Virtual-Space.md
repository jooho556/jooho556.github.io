---
layout: post
title: Virtual Space
---

<head>
  <!-- Place your kit's code here -->
  <script src="https://kit.fontawesome.com/de7d103504.js" crossorigin="anonymous"></script>
</head>

![Galaxy](/assets/Galaxy.gif){: .align-center}
-----

Side project for rendering space scene mainly focused on galaxy and nebulae<br/>
You can check my repository here: <i class="fab fa-github"></i>[GitHub](https://github.com/jooho556/Virtual-Space)

<em>C++, OpenGL, SDL<br/>
October 2019 ~ </em>

<!--more-->

## Rendering a galaxy

<div class="message">
  Particle + Point Sprite + Compute Shader = Galaxy!
</div>
https://github.com/jooho556/jooho556.github.io
One of the major building blocks for rendering a galaxy is particle. Every particle has its position and informations about its orbit, which is an ellipse. Let's start with the orbits.

1. Draw an ellipse (Center of galaxy)
2. Increase the diameter and slightly tilt it
3. Draw that ellipse
4. Repeat step 2 & 3...

and you get this:

![Orbits](/assets/Orbits.png)

Next step is put some particles to these otbits, but how? Maybe we could get x and y coordinate from equation of ellipse, but that is cumbersome process. We should use parametric equation of ellipse.

{% highlight js %}
F(t) = (x(t), y(t))
x(t) = a * cos(t)
y(t) = b * sin(t)
//where a is major axis, b is minor axis
{% endhighlight %}

If t is 0, point goes to right side of the ellipse<br/>
If t is π/2, point goes to left side of the ellipse<br/>
...

We can random values of t ranging from 0 to 2π if value a and b is given.

So this is the outline:
{% highlight js %}
vector<Point> pos;
vector<Info> info;
Ellipse ellipse;
for(Until loop counter reaches to certain radian)
{
  for(The number of particle of current orbit(ellipse))
  {
    float t = GetRandomValue(0, 2π);
    Point p = ellipse.GetPoint(t);
    pos.push_back(p);
    info.push_back(Info(t, ellipse.getA(), 
      ellipse.getB(), ellipse.getRotation()));
  }
  ellipse.AddRadius(some_value);
  ellipse.Rotate();
}
{% endhighlight %}

After binding 'pos' and 'info' to vertex buffer object correctly, use glDrawArrays with GL_POINTS as primitive. Find any particle texture you want and use GL_POINT_SPRITE as well. There should be visual enhancement. Then your output should be like:

![Nebula](/assets/Galaxy_unfinished.png)

Beautiful, but it is not moving. Every particle must update their position, and that is where compute shader comes in. Vertex buffers have t values and informations for ellipse. You have to have compute shader update the t value (by increasing small amount of offset, like 0.0001f) and build the equation of ellipse and re-calculate x and y position using updated t and equation of ellipse.

If you are unfamiliar with compute shader, check this out: [OpenGL 4 Shading Language Cookbook - Third Edition](https://www.oreilly.com/library/view/opengl-4-shading/9781789342253/)

-----
## Rendering a nebula (Still in progress)

![Nebula](/assets/Nebula.jpg)

<div class="message">
  Perlin Noise + ??? = Nebula!
</div>

We need a random noise, but looked more natural. Perlin noise is perfect for rendering cloudy objects like nebula. What I am doing here is just blending the image of nightsky with the image of perlin noise and that's it! However, that means I just used the raw noise data. We can do more than this. What I am thinking is using volume rendering...

## Reference
[https://beltoforion.de/article.php?a=spiral_galaxy_renderer](https://beltoforion.de/article.php?a=spiral_galaxy_renderer)
[https://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/perlin-noise-part-2](https://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/perlin-noise-part-2)
