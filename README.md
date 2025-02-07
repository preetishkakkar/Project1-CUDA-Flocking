**University of Pennsylvania, CIS 565: GPU Programming and Architecture,
Project 1 - Flocking** (I am studying this course on my own)

* Preetish Kakkar
  * https://www.linkedin.com/in/preeteesh/

NOTE:
-------------------------------------------------------------------------------
This project requires a CUDA-capable graphics card
-------------------------------------------------------------------------------

Summary
============================

This project implements a flocking simulation based upon Reynolds Boids algorithm (https://en.wikipedia.org/wiki/Boids). It adds optimizations using
a uniform grid & a uniform grid with semi-coherent memory access. Coherent memory access means that any changes made to memory will be visible immediately for all other reads. 

A CUDA kernel is responsible for calculating the velocity & positions of boids at each timestamp. Drawing is done using OpenGL.

Step 1
-------------

First phase of project implements below ideas

1.) cohesion - boid move towards center of mass of neighbors
2.) separation - boids keep a certain distance from it's neighbors
3.) alignment - boids try to follow their neighbors speed & distance.

These rules ultimately helps us compute velocity change at each timestamp. 

<img src="demo_imgs/working_part1.gif" width = 600>

-------------

Step 2
-------------

Second phase of project is all about optimizations. In first phase, we simply did a naive implementation that looked around all of it's neighbors. This won't be performant since we have a lot of boids. In this step we will implement a uniform spatial grid that can help us cull neighbors that are not next to the current boid. We will implement function kernUpdateVelNeighborSearchScattered 

This is how my initial buggy implementation looked like, it was a very minor bug, looked like a cool blackhole animation :)

<img src="demo_imgs/blackhole_anim.gif" width = 600>

After fixing bug with 50000 boid. Hurray!

<img src="demo_imgs/working_part2.gif" width = 600>

Step 3
-------------

The third phase of the project is about a bit more optimizations, namely eliminating the use of particleIndexBuffer to refer to velocity & positions. We create another buffer so that velocity and position buffer are mapped in a contiguous memory.

<img src="demo_imgs/working_part3.gif" width = 600>