---
layout: default
title: Shield Impacts
description: Project
---

# Shader Project - Shield Impacts

<div class="image_container">
    <img src="../images/shield-impacts/shield.gif" width="250"/>
</div>

***

Here whenever I detect a collision with the sphere I add the position to a Vector4 array, containing the time when it hit aswell in the w component.

Then I send the array to the shader, and for each hit in the array I take the distance from the hit position and the current vertex position. Then I manipulate this value so it gives me rings instead of only a gradient between the hit and the vertices (basically substracting two stepped distances), and take the min() of this distance and the previous one so all hits distances get combined nicely. 

The *t* value is used to drive the step/smoothstep of the distances, meaning a bigger *t* will make the ring travel further.
We only need the time of impact so we can do *saturate((_Time.y - t) / length)*, meaning that at the time of impact *t = _Time.y* (ring is stepped at 0), and as _Time.y goes up *t* will naturally go up to 1 maximum, capped by the saturate function that clamps the value between 0 and 1.

Then it's only a matter of making it pretty, here I went kind of overkill with a grabpass distortion, a small rim on the edge, a slight more faded rim teasing the hexagons texture, chromatic aberration, etc.

If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

***

[back](../)
