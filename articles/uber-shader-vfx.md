---
layout: default
title: Uber Shader VFX
description: Project
---

# Shader Project - Uber Shader VFX

***

Recently I made a Uber shader specially for VFX, I made a few tests to try it out.

<div class="image_container">
    <img src="../images/uber-shader-vfx/projectiles.gif" width="250"/>
    <img src="../images/uber-shader-vfx/shockwave.gif" width="250"/>
</div>

<div class="card">
    <div>
        <img src="../images/uber-shader-vfx/shader.png" width="250"/>
    </div>

<div class="card_child">
It was also a good occasion to make a custom Material inspector, using the ShaderGUI api and MaterialPropertyDrawers. 

Here when serializing the properties I look up the shader's properties names directly so I can have special behaviours like grouping the texture and its tiling/offset/speed if the properties names match. 

The toggled foldouts are a bit hacky, I'm actually using a property in the shader that stores the state of the foldout toggle (activated/deactivated) and the state of the foldout itself (opened/closed). The property line itself (with the toggle) is drawn using a MaterialPropertyDrawer, and other properties that start with the name will get drawn below it, only when it's opened.
</div>
</div>

Here's an example in the shader

```c#
    [FoldoutToggle(_FEATURE_HITFLASH)] _ToggleHit ("Hit Flash", Vector) = (0,0,0,0)
    [HDR] _HitColor ("Hit Color", Color) = (1,1,1,1)
    _HitLength ("Hit Length", Float) = 1
```

Here _ToggleHit.x contains the toggle state, and _ToggleHit.y the tab state.

The MaterialPropertyDrawer of the toggle also handles setting the shader keywords, _FEATURE_HITFLASH in this case.

***

## 2021 Update

So I ended up continuing working on this, carrying it through projects and refining it every time. It now works a bit differently -- when I open the material inspector in *OnEnable()* I build up a list of every material property that exist, and their categories from the shader properties names, containing their foldout / toggle states. They all get saved in *SessionState*, which is kind of like *EditorPrefs/PlayerPrefs*, except that it only lives during the Unity session. Meaning that when I restart Unity the foldout states are not preserved. This is fine, I don't need it to remember which foldouts were open after quitting the engine, but for the toggle states ( which add / remove shader keywords ) I simply look up the existing shader keywords and set the toggles values based on that, also in the *OnEnable()* function.

I also took some time to make it prettier :)

![Shader](../images/uber-shader-vfx/shaderV2.png)

If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

* * *

[back](/blog.html)
