---
layout: article
title: 🧊 Voxel Animation Textures Breakdown
description: VATs for voxel simulations, from Houdini to Unity using Alembic
thumbnail: ../images/voxel-animation-texture/thumb.gif
banner: ../images/voxel-animation-texture/banner.png
tags: [shaders, houdini, vfx]
date: 2019-12-01
last_update: 2019-12-01
---

## Introduction

Here's a small R&D project made in collaboration with [Pascal Beeckmans](https://www.behance.net/paqwak). We wanted to find a way to have voxel animations in Unity with lightweight textures.

## Voxel Animation Textures

The idea is to export a point cloud (.abc) from Houdini that contains all the points from the simulation (its bouding box, basically). Then a texture that contains the state of every cell of the simulation for each frame, and another one to store arbitrary data. In this case we used it to store the temperature of the simulation, so we can color the voxels in engine.

<div class="image_container">
    <img src="../images/voxel-animation-texture/explosion.gif" width="230"/>
    <img src="../images/voxel-animation-texture/waves.gif" width="230"/>
</div>

In Unity we used the *Alembic* package to import the point cloud. It already comes with a setup to draw any mesh instantiated on each point, using *DrawMeshInstancedIndirect*. Then in the shader we read the texture using the *SV_InstanceID* to isolate individual instances and collapse the vertices of the voxels according to their state at the specified frame.

***

[back](../blog.html)
