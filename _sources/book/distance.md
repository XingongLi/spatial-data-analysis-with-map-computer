---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Spatial Relationship: Distance

Note: see [frechet and hausdorff distance](https://shapely.readthedocs.io/en/2.1.1/reference/shapely.frechet_distance.html#shapely.frechet_distance) function in shapely.

## Topics
* Co-locational relationship
    * Qualitative (topological) and quantitative relationships
* Interactional relationship
    * Connection between two locations
    * Exchange of matter, energy and information links locations
* Distance relationship
    * As a measure/proxy of interactional relationship
    * Quantify the disjoint relationship (beyond co-location)

## Spatial Interactional Relationships
* Interactional relationships
    * Exchange of matter, energy and information between locations
    * Beyond distance
    * Domain dependent
    * Viewshed, watershed, hydro-connectivity, ...
* Some may be described by physical processes
* Some are still mysterious/unknown
    * Teleconnection, gravity, ...
* Connections or links between locations

## Why Care About Spatial Relationships
* Yoneda Lemma
    * If you want to understand a mathematical object, all of the information about that object is contained in the totality of relationships that object has with all other objects in its environment
* We can learn a lot about a location by seeing how the location interacts with other locations
    * May vary from location to location
* Meta-map (a map of maps)
    * Location -> {(location, {attributes})}
    * Map of spatial relationships

## Distance as the Proxy of Interactional Relationship
* "Everything is related to everything else, but near things are more related than distant things." (Waldo Tobler, 1970)
* Distance is used to represent the movement of matter, energy and information when the underlying physical processes are not well understood
* Distance is the least movement cost between two locations

## Types of Distance Relationships
* Distance to specific location(s)
* Buffers
* Proximity regions (Thiessen Polygons/Voronoi Diagram)

## Distance to Specific Location(s)
* Every location in a study area has a distance to a specific location
* Examples:
    * Distance to the coastline
    * Distance to the nearest hospital
    * Distance to the nearest highway

## Buffers
* A buffer is a region within a specified distance of a geographic feature
* Buffer types:
    * Points, lines, or polygons
    * Fixed distance vs. variable distance
    * Single vs. multiple rings

## Proximity Regions (Voronoi Diagram)
* Every location within a proximity region is closer to the associated generator point than to any other generator point
* Boundaries are the perpendicular bisectors of the lines connecting neighboring points



## Calculating Distance
* Movement cost in different space/media
* Euclidean space (vacuum/abstract space)
    * Euclidean distance (straight line)
* Non-Euclidean space
    * On a spheroid (Great circle distance)
    * In a network (Road/river networks)
    * On a friction surface (Terrain/Least cost path)

## Euclidean Distance
* $d_{ij} = \sqrt{(x_i - x_j)^2 + (y_i - y_j)^2}$
* Straight line distance in a flat plane (PCS)
* Manhattan distance ($L_1$ norm): $d_{ij} = |x_i - x_j| + |y_i - y_j|$

## Distance on a Spheroid
* Great circle distance
* The shortest distance between two points on the surface of a sphere
* Calculated using latitude and longitude (GCS)



## Network Distance
* Distance is constrained by a network of interconnected lines (links) and points (nodes)
* Shortest path algorithm (e.g., Dijkstra's algorithm)
* Examples: travel time, fuel consumption

## Distance on a Friction Surface
* Movement cost varies across space due to different "friction" or "impedance"
* Cost Surface/Friction Surface:
    * A raster map where each cell represents the cost of moving across it
* Least Cost Path:
    * The path between two locations that minimizes the cumulative cost
* Accumulated Cost Surface:
    * A map showing the minimum cost to reach a source from any location



## Isotropic vs. Anisotropic Friction
* Isotropic: Cost is the same regardless of the direction of movement (e.g., land cover)
* Anisotropic: Cost depends on the direction of movement (e.g., wind, slope/terrain)

## Summary
* Distance is the least movement cost between two locations
    * Affects the exchange of matter, energy and information
    * Proxy for interactional relationship
* Types of distance for a location/MU
    * Distance to specific locations/MUs
    * Buffers
    * Proximity regions
* Distance in different space/media
    * Euclidean space
    * Non-Euclidean space (Spheroid, Network, Friction Surface)

## Map of Distance Relationship (meta-map)
* A map where each MU has a “distance” map
* A “distance” map stores locations and distance (and other attributes)
    * To pre-identified locations, buffers, proximity regions
    * Euclidean and non-Euclidean
    * Vector and raster MUs