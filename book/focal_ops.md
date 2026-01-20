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

# Focal Operation

## Focal Operations
* Operations:
    * Local, focal and global operations based on the spatial scope of neighborhood
    * Neighborhood relation operations
* 3 kinds of mapping/analysis units:
    * Cells
    * Raster zones
    * Features

| Mapping Units | Neighborhood Relation: Local | Neighborhood Relation: Focal | Neighborhood Relation: Global |
| :--- | :--- | :--- | :--- |
| **Cells** | Local | Focal | Global |
| **Raster zones** | Local | | |
| **Features (vectors)** | Local | | |

## Topics
* Focal operations with raster map
    * Moving-window, distance/direction based, irregular weighted neighborhoods
* Focal operations with vector map
    * Buffer
* Domain-based focal neighborhoods
    * Watershed
* Types of focal operations

## Focal Operations
* Compute for each output MU with the neighbors of its focal neighborhood
* Cells, raster zones, vector features as MUs
* Data manipulation within MU's focal neighborhood



## Focal Neighborhood
* A set of locations that has a certain relationship with a MU
    * Beyond the MU itself (vs local neighborhood)
* Represents interactional relationship between a MU and other locations
    * Exchange of matter, energy, and information
* The MU is also referred to as the neighborhood focus
* The related locations are referred to as the neighbors

## Characterizing Focal Neighborhoods
* Two ways to characterize focal neighborhoods:
    * Based on distance and direction
        * Moving-window (raster), Buffer (vector/raster)
    * Based on domain knowledge/processes
        * Watershed, viewshed, network, etc.

## Moving-Window Neighborhoods
* Neighborhood defined by a "window" of a specific shape and size
* The window "moves" from cell to cell
* Neighborhood is same for all cells (relative to the focus)
* Types:
    * Square (3x3, 5x5, etc.)
    * Circle
    * Plus (rook's case)



## Focal Statistics
* Calculate a statistic for the values within the moving window
* Common statistics:
    * **FocalSum**: Total value (e.g., total biomass)
    * **FocalMean**: Average value (smoothing)
    * **FocalMax/FocalMin**: Range or edge detection
    * **FocalVariety**: Number of unique values (diversity)

## Examples of Moving-Window Operations
* **Smoothing**: Use FocalMean to reduce noise in data
* **Edge Detection**: Use FocalMax - FocalMin to find where values change rapidly
* **Focal Variety**: Useful for identifying boundaries between different land cover types

## Morphology/Shape Analysis
* Use Focal operations to analyze the shape of features
* **Erosion**: Using FocalMinimum on a binary map
    * Removes outer layer of pixels
* **Expansion/Dilation**: Using FocalMaximum on a binary map
    * Adds an outer layer of pixels



## Morphology/Shape Analysis (cont.)
* **Inner Boundaries**: Identify cells that are part of the feature but touch the background
* **Outer Boundaries**: Identify background cells that touch the feature
* Combined boundaries provide detailed structural analysis

## Distance/Direction-Based Neighborhoods
* Neighborhood defined by specific distance and directional parameters
* Neighborhoods in ArcGIS:
    * Rectangle, circle, annulus (donut), or wedge (a slice of a circle)



## Finding Appropriate Wind Farm Sites
* Selection criteria:
    * **Wind speed**: Higher elevation generally equals higher speed (Elevation >= 1000m)
    * **Aspect**: Facing the prevailing wind direction
    * **Wind exposure**: Not blocked by nearby hills in the prevailing wind direction
* Data needed:
    * Prevailing wind direction (e.g., 225° to 315°)
    * Digital Elevation Model (DEM)
* **Wedge neighborhood**: Used to check for obstructions in the specific wind direction

## Types of Focal Operations
* **Simple Focal Operations**: Neighborhood is predefined (shape/size)
    * Example: Moving window
* **Irregular/Weighted Focal Operations**: Neighbors have different "weights" or importance
    * Example: Gravity model, Kernel density estimation
* **Process-based Focal Operations**: Neighborhood is defined by a physical process
    * Example: Watershed (defined by terrain/gravity)


## Irregular Weighted Neighborhood
* Neighborhood and weights are defined by a matrix
    * 0s indicate a location is not a neighbor
    * Other values represent weight (neighbor relation property)
* Matrix can be stored as a neighborhood text file
    * Kernel file in ArcGIS
* All cells use the same neighborhood structure
* Operation: **Weighted Summary**
    * Get the neighbor value from the input map
    * Summarize (weight * value)

## Weighted Moving-Average (Smoothing)
* Weights are inversely proportional to distance
* The weight for the focus MU is typically the largest
* Used to reduce noise while preserving more detail than a simple mean

## Kernel Density Estimation (KDE)
* Neighborhood is a circle with a radius (bandwidth)
* Weights are defined by a continuous kernel function
    * Weight is highest at the center and decreases to zero at the boundary
* Operations:
    1. Calculate weighted value for each neighbor (Weight * Value)
    2. Sum all weighted values
    3. Normalize (optional)

## Process-Based Focal Neighborhoods
* Neighborhood is defined by a physical or social process
* Examples:
    * **Watershed**: Neighborhood defined by terrain and gravity (flow of water)
    * **Viewshed**: Neighborhood defined by line-of-sight and topography
    * **Service Area**: Neighborhood defined by travel time on a road network

## Watershed as a Focal Neighborhood
* A watershed is a neighborhood where all locations drain to a common outlet (focus)
* Interaction: Water, sediment, and pollutants move from neighbors to the focus
* Neighborhood is irregular and varies from location to location

## Types of Focal Operations (Based on Output)
* Three types of focal operations based on what the output value represents:
    1. Characterize focal neighborhood
    2. Compare focus MU and its neighbors
    3. Predict attribute at the focus MU

## Type 1: Characterize Focal Neighborhood
* The output value summarizes the attributes within the neighborhood
* Focal Statistics:
    * **FocalSum**: Total amount
    * **FocalMean**: Average intensity/density
    * **FocalMax/FocalMin**: Extremes
    * **FocalVariety**: Diversity/Heterogeneity
    * **FocalMajority**: Dominant type

## Type 2: Compare Focus MU and Neighbors
* The output value represents the relationship or contrast between the focus and its surrounding area
* Operations:
    * **ContrastLocation**: Distance to specific neighbors
    * **ContrastValue**: Difference between focus value and neighborhood mean
    * **FocalPercentage**: Percentage of neighbors with values equal to the focus
    * **FocalPercentile**: Percentage of neighbors with values less than the focus

## ContrastValue Operation Examples
* **FocalPercentage**: 
    * Measures the homogeneity of the focus relative to its neighbors
* **FocalPercentile**: 
    * Identifies if a focus MU is a local peak (high percentile) or local pit (low percentile)