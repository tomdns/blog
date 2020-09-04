---
layout: default
title: Devnotes | Compute Shader Game Of Life
description: Devnotes
---

![Header](../images/simple-outline-post-process/header.png)

# Devnotes - Conway's Game of Life with Compute Shaders

* * *

## Note

Devnotes are a way for me to keep track of what I do and remind me of the important bits :)

## 1 - Core idea

I send a render texture to the compute that will contain the results of the simulation, I never read from it.
Then I send a RWStructuredBuffer of the size of my texture (width*height). So for each pixel I can have a struct of whatever data I need to send. For instance storing the previous/current state, a color, a lifetime, ... 

```c#
    public struct Pixel
    {
        public int oldState;
        public int state;
        public Vector4 color;
        public float health;
        public float startHealth;
    };

    ...

    Pixel[] pixels = new Pixel[width * height];

    ComputeBuffer pixelsBuffer = new ComputeBuffer(width * height, sizeof(int) * 2 + sizeof(float) * 6);
    pixelsBuffer.SetData(pixels);
```

The struct has to be matched in the compute exactly the same.

Each frame I send the texture to the material, the compute, and dispatch the compute.
I kept the thread counts to [8,8,1] so I dispatch it this way

```c#
    compute.Dispatch(updateKernel, width/8, height/8, 1);
```

## 3 - Conclusion
 
If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

* * *

[back](../)
