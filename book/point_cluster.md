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

# Point Pattern Analysis: Clusters

Topics:
* Mapping point clusters
* Clustering points

## Point Randomness
* Characterizing the overall point pattern (randomness):
    * Random
    * Uniform (Dispersed)
    * Clustered

## Locate Clusters
* Knowing that a point distribution is clustered does not necessarily give information about where the clusters reside.
* Mapping clusters:
    * Calculate spatial variation of point density.
    * Useful if points are samples.
* Clustering points:
    * Identify specific points that are close to each other.
    * Useful if points are the "population."

## Mapping Clusters (Kernel Estimation)
* Areas of high point density indicate clusters.
* Naïve point density mapping:
    * Use a regular grid in space.
    * Calculate the density of points within a circular neighborhood at each grid center.
    * $Density = Number\ of\ points / \pi d^2$

## Kernel Density Estimation (KDE)
* A focal operation where weights are defined by a continuous kernel function.
* The weight is highest at the center (focus) and decreases to zero at the neighborhood boundary (bandwidth).
* Provides a smoother surface than naïve density mapping.


## Issues with KDE
* Choice of bandwidth (radius) significantly impacts the result.
    * Small bandwidth: Shows local variation and noise.
    * Large bandwidth: Shows broad trends but hides local clusters.
* Choice of kernel function (e.g., Quartic, Gaussian) has less impact than bandwidth.

## Clustering Points
* Grouping points into categories based on spatial proximity.
* Goal: Find groups of points that are "closer" to each other than to points outside the group.

## K-Means Clustering
* Partitions $n$ points into $k$ clusters.
* Procedure:
    1. Randomly select $k$ points as initial cluster centers (centroids).
    2. Assign each point to the nearest centroid.
    3. Re-calculate the centroids of the new clusters.
    4. Repeat steps 2 and 3 until centroids no longer move significantly.
* Issue: You must specify the number of clusters ($k$) in advance.

## Density-Based Spatial Clustering (DBSCAN)
* Classifies points into three categories:
    * Cores: Points inside a cluster with at least $m-1$ points within distance $r$.
    * Borders: Points inside a cluster but with fewer than $m-1$ points within distance $r$.
    * Noise: Points not belonging to any cluster.
* Does not require specifying the number of clusters in advance.
* Can identify clusters of arbitrary shapes.

## DBSCAN in the Map Compute Framework (MCF)
* Viewed as a series of Neighborhood Relation and Graph operations.
* Step 1: NbrGraph (Neighborhood relation operation)
    * Create a distance-based neighborhood ($r$).
    * Form a graph where points are nodes and proximity forms links.
* Step 2: Graph Analysis
    * Identify sub-graphs (connected components).
    * Classify sub-graphs based on the number of points ($m$).
* Step 3: Node Classification
    * Nodes in small sub-graphs ($< m$) are noise.
    * Nodes in large sub-graphs ($\ge m$) are core or border based on their degree (number of links).

## Summary: Mapping vs. Clustering
* Mapping (KDE) results in a continuous surface (raster) showing the intensity of events.
* Clustering (DBSCAN, K-Means) results in categorical assignments (attributes) for the original point features.
* Choice of method depends on whether you want to visualize a "heat map" or identify distinct groups for further analysis.
