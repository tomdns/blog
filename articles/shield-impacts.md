---
layout: default
title: Shield Impacts
description: Breakdown
---

# Shader Breakdown - Shield Impacts

***

<!-- <div class="image_container">
    <img src="../images/shield-impacts/shield.gif" width="250"/>
    <img src="../images/shield-impacts/bread.gif" width="250"/>
</div> -->

Quick breakdown of the shader I showed on twitter.

<blockquote class="twitter-tweet" data-dnt="true" data-theme="dark"><p lang="en" dir="ltr">Couldn&#39;t resist... I made a shield shader again 🙈<a href="https://twitter.com/hashtag/gamedev?src=hash&amp;ref_src=twsrc%5Etfw">#gamedev</a> <a href="https://twitter.com/hashtag/madewithunity?src=hash&amp;ref_src=twsrc%5Etfw">#madewithunity</a> <a href="https://twitter.com/hashtag/shaders?src=hash&amp;ref_src=twsrc%5Etfw">#shaders</a> <a href="https://twitter.com/hashtag/vfx?src=hash&amp;ref_src=twsrc%5Etfw">#vfx</a> <a href="https://t.co/DYToUr7B9N">pic.twitter.com/DYToUr7B9N</a></p>&mdash; Thomas Denis (@tomdns_) <a href="https://twitter.com/tomdns_/status/1177389679815135233?ref_src=twsrc%5Etfw">September 27, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Here whenever I detect a collision with the sphere I add the position to a Vector4 list, containing the time when it hit aswell in the w component.

```c#

hits.Add(new Vector4(hit.x, hit.y, hit.z, t));

```

I send the list to the shader, and loop through it. To make rings, for each hit position I do as follows:

Take the distance between the hit position and the vertex position

![Distance](../images/shield-impacts/process_distance.png)

Step the distance, using the time of impact *t* value

![Distance](../images/shield-impacts/process_step.png)

Step the distance again using *t - ringWidth* then substract both stepped values

![Distance](../images/shield-impacts/process_ring.png)

Then take the *max()* of the resulting value and the previous one in the loop to add them all together.

In my case I use *smoothstep* instead of *step* to have a smoother transition of values instead of either 0 or 1, but step is easier to explain.

The *t* value is used to drive the step/smoothstep of the distances, meaning a bigger *t* will make the ring travel further.
We only need the time of impact so we can do *1 - saturate(_Time.y - t)*, meaning that at the time of impact *t = _Time.y* (ring is stepped at 0), and as _Time.y goes up *t* will naturally go up to 1 maximum, capped by the saturate function that clamps the value between 0 and 1. Each ring also gets multiplied by its *t* value, so that as it travels it also fades to black.

Here's some sample code

```c#
    float mask = 0;
    for(uint i = 0; i < HIT_COUNT; i++)
    {
        float t = 1.0 - saturate(_Time.y - _HitPosition[i].w);

        float d0 = distance(vertex, _HitPosition[i].xyz);
        float d1 = step(t, d0);
        float d2 = step(t - _RingWidth, d0);
        
        mask = max(mask, d1 - d2);
    }
```

Ofc if you only need a single hit to show instead of multiple ones at the same time it gets a bit easier. 

Then I use this mask as alpha, here's a small decomposition of the effect

![Process](../images/shield-impacts/process.png)

If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

***

[back](../blog.html)
