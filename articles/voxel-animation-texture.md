---
layout: default
title: Voxel Animation Textures
description: Breakdown
---

# Shader Project - Voxel Animation Textures

***

<div class="image_container">
    <img src="../images/voxel-animation-texture/explosion.gif" width="250"/>
    <img src="../images/voxel-animation-texture/waves.gif" height="308"/>
</div>

Small experiment to have VATs to animate voxel simulations inside Unity, made in collaboration with [Pascal Beeckmans](https://www.behance.net/paqwak).
We export a point cloud from Houdini (.abc file) that contains all the possible cells of the animation, like the bounding box of the whole simulation. Then we export a texture that contains for each frame of the animation the state of each voxel cell, and another texture that contains the temperature or w/e data we want, so we can color the voxels in engine.

In Unity we used the Alembic package to import the point cloud. It already comes with a setup to draw any mesh instantiated on each point, using DrawMeshInstancedIndirect. Then in the shader we read the texture using the SV_InstanceID to collapse the vertices of the voxels according to their state at an instant t.

If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

***

[back](../)
