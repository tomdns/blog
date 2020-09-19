---
layout: default
title: Sand Game With Compute Shaders
description: Breakdown
---

![Header](../images/compute-game-of-life/sandgame_unity.png)

# Shader Project - Sand Game With Compute Shaders

* * *

Small experiment notes on making a sand game running in a Compute Shader...

Here I send a render texture to the compute that will contain the results of the simulation, I never read from it.
I send a RWStructuredBuffer the size of my texture (width * height), so for each pixel I have a struct that contains whatever data I need to send. 
Every frame the compute is dispatched, the buffer gets modified, and the RenderTexture is written to with the content of the buffer.

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

Each frame I send the texture to the material, to the compute, and I dispatch the compute.
Here's how its dispatched for a thread count of [8,8,1] (so it's simpler to write to the texture) in the *Update()*

```c#
    compute.Dispatch(updateKernel, width/8, height/8, 1);
```

I also dispatch another kernel function (once) to set default values if I input a texture instead of a blank RT (see the Unity logo).
I dispatch it at the start and it just sets my buffer block types to AIR or TREE based on the pixels color. 
That means I have to set the pixelsBuffer to both kernels. No need to read back after dispatching the start kernel.
So in my *Start()* function after creating the *pixelsBuffer*:

```c#
    compute.SetBuffer(startKernel, "_Pixels", pixelsBuffer);
    compute.Dispatch(startKernel, width/8, height/8, 1);

    compute.SetBuffer(updateKernel, "_Pixels", pixelsBuffer);
``` 

The rules of the simulation are fairly simple, for each block type I describe what to do according to the direct neighbours to the current pixel. The tricky part is for example with sand you want to have a condition for the sand block to become air when falling and vice versa, since you can't modify neighbour pixels directly, you need to have both conditions. 
It can make more complicated block types a pain to make but still, using basic rules you can have some really cool effects.

![Types](../images/compute-game-of-life/sandgame.png)

Here for the fire behaviour I used Conway's game of life, and it spreads to neighbour pixels if they're trees. This means in my TREE behaviour if any neighbour is a FIRE or a TREE_BURNING, it has a chance to become a TREE_BURNING aswell next iteration.

```c++
    if(state == TREE)
    {
        for(int i = 0; i < 8; i++)
        {
            if(nbs[i] == FIRE || nbs[i] == TREE_BURNING)
            { 
                if(rand < BURN_CHANCE)
                SetState(id.xy, TREE_BURNING);
            }
        }
    }
```

And at last in the compute I also set the texture color according to the buffer pixels type, since as I said I'm only modifying the RWStructuredBuffer here, not the texture directly.

You can see it in action [here](https://preview.redd.it/vzwvhd3oehf51.gif?format=mp4&s=db4d21f6946280f9a162aa0b1a0a86245a7bd38c)

If you have any question you can message me directly [@tomdns_](https://twitter.com/tomdns_)

* * *

[back](../)
