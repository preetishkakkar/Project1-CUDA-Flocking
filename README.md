**University of Pennsylvania, CIS 565: GPU Programming and Architecture,
Project 1 - Flocking** (I am trying this course on my own)

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

-------------