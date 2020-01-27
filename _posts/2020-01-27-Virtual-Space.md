---
layout: post
title: Virtual Space
---

<head>
  <!-- Place your kit's code here -->
  <script src="https://kit.fontawesome.com/de7d103504.js" crossorigin="anonymous"></script>
</head>

![Galaxy](/assets/Galaxy.gif)
-----

Side project for rendering space scene mainly focused on galaxy and nebulae
You can check my repository here: <i class="fab fa-github"></i>[GitHub](https://github.com/jooho556/Virtual-Space)

<em>C++, OpenGL, SDL
<em>October 2019 ~

## Rendering a galaxy

<div class="message">
  Particle + Point Sprite + Compute Shader = Galaxy!
</div>

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

If t is 0, point goes to right side of the ellipse.
If t is π/2, point goes to left side of the ellipse.
...

We can random values of t ranging from 0 to 2π if value a and b is given.

## Rendering a nebula (Still in progress)

![Nebula](/assets/Nebula.jpg)

<div class="message">
  Perlin Noise + ??? = Nebula!
</div>

## Reference
https://beltoforion.de/article.php?a=spiral_galaxy_renderer
https://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/perlin-noise-part-2
