---
layout: article
title: 🤖 Hologram Shader Breakdown (RTVFX Sketch 18)
description: GPU Particles, Compute & Geometry shaders
thumbnail: ../images/sketch-hologram/thumb.gif
banner: ../images/sketch-hologram/hologram_turnaround.gif
tags: [shaders, vfx]
date: 2018-11-01
last_update: 2018-11-01
---

## Introduction

Here are some notes on my entry for the 18th RTVFX Sketch (ended up 2nd! 🥈)
The theme was hologram.

## Breakdown

The particles were made with a custom GPU particles system, using compute shaders to update them and geometry shaders for rendering.

In the geometry shader for each point in the buffer I create a bunch of new line strips (using *LineStreams*) that are offsetted a bit randomly to give this blurry/fuzzy look.
Some of them connect the vertices to the "cylinder", which is faked by clamping the x and z position of each line end vertex.

The particles buffer is rendered using *Graphics.DrawProcedural* (with *MeshTopology.Points*).

I made it work for SkinnedMeshRenderers aswell, by baking the mesh each frame and sending the vertices to the compute shader (with *SkinnedMeshRenderer.BakeMesh()*)

You can see the work in progress on the RTVFX thread [here](https://realtimevfx.com/t/thomas-denis-sketch-18-hologram/6507).

And the final result:

![Final](../images/sketch-hologram/hologram_finish.gif)

***

[back](../blog.html)
