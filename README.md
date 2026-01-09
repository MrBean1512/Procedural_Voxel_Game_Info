# Procedural Terrain Generation — Notes, Experiments, and Current Approach

## Introduction

I started exploring procedural terrain generation because I wanted to build a voxel‑like game that wasn't limited to the classic blocky aesthetic. Games like **Valheim** first sparked the idea, but **Enshrouded** proved that highly detailed voxel terrain with smooth, organic, and rich in variation, is actually doable.

This document isn’t a tutorial or a polished repo. It’s a running log of what I’ve learned—what I’ve tried, what failed, what worked, and the direction I’m taking as I figure out how to generate detailed voxel terrain. It covers a bit of everything because most of the documentation I’ve found focuses on just one approach, which has led me more than once to follow a method deep into a project only to realize it won’t get me the results I’m after. My goal here is to lay out each technique with its strengths and limitations so the trade-offs are clear from the start. My focus here is on the sandbox/world generation itself, not the full game loop around it. That said, I keep gameplay in mind throughout, because many tutorials ignore real gameplay needs and end up being incomplete or impractical.

Because this is an evolving project, I’m not sharing full repositories until I reach a point where the results feel solid and worth presenting.

---

## Topics I've Had to Learn (and Am Still Learning)

This project has required diving into a wide range of systems and techniques. These aren’t tutorials, just the major areas that have shaped my approach so far.

### Noise & Terrain Shape
- Understanding different noise types (Perlin, Simplex, FBM, domain warping)
- Combining multiple noise layers to form believable terrain
- Using noise for heightmaps, density fields, and biome distribution

### Mesh Generation
- Converting voxels into actual meshes
- Working with marching cubes, dual contouring, surface nets, 
- Handling vertices, triangles, normals, and tangents
- Generating collision meshes vs. visual meshes

### World Structure & Optimization
- Chunk systems for streaming large worlds
- Level of Detail (LOD) strategies for distant terrain
- Octrees and spatial partitioning
- Mesh stitching to avoid cracks between chunks

### Shaders, Compute-Shaders Materials, Textures
- Offloading heavy voxel and mesh operations
- Adding details to materials/textures/shaders to make it more than just a flat texture.
- Writing shaders to color and texture terrain
- Using triplanar mapping to avoid stretching
- GPU‑side calculations for terrain detail

## Methods with Pros & Cons

### Noise

#### Perlin Noise
- **Details** - Perlin Noise is one of the most famous noise algorithms. It generates sort of hills and valleys
- **Pros** - Tried and true and generally good for simple terrain
- **Cons** - Sorta old, there's alternatives that are newer, slightly faster, and do almost the same thing
