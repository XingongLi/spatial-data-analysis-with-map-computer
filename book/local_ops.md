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

# Local Operations

## Map Compute Framework
* Three kinds of analysis/mapping units (MUs) in maps
    * Cells, raster zones, features
* Four kinds of operations
    * Local, focal, and global operations (based on spatial scope)
    * Neighborhood relation operations

| Mapping Units | Neighborhood Relation: Local | Neighborhood Relation: Focal | Neighborhood Relation: Global |
| :--- | :--- | :--- | :--- |
| **Cells** | Local | Focal | Global |
| **Raster zones** | Local | | |
| **Features (vectors)** | Local | | |

## Topics
* Local operations
    * Cells and vector features as mapping units
    * Output/analysis MU itself is and defines the neighborhood
* Application examples
    * NDWI and mNDWI
    * Composite image
    * Create rainfall map using elevation map

## Local Operations
* Compute a new map where the value for each MU on the output map is a function of one or more values at the same MU on the input map(s)
* General form: $Value_{new} = f(Value_{in1}, Value_{in2}, ...)$
* Output map MUs are the same as (or defined by) the input MUs



## Local Operations in Practice
* Reclassify (e.g., fungus diffusion exercise)
* Turn precipitation table into a map (using weather station points)
* Map overlay (Intersect, Union, Erase, etc.)
* Field calculator (Vector) / Raster calculator (Raster)

## Types of Local Operations
* Local operations with one input map
    * $Value_{new} = f(Value_{in})$
* Local operations with multiple input maps
    * $Value_{new} = f(Value_{in1}, Value_{in2}, ...)$

## Local Operations: One Input Map
* Arithmetic and logical operations
    * $Map + 10$
    * $Map > 100$ (Boolean output)
* Reclassification
    * Grouping values into new categories
    * Example: Land cover types to "Suitable/Unsuitable"

## Local Operations: Multiple Input Maps
* Cell-by-cell or feature-by-feature combination
* Mathematical combinations
    * $Map_A + Map_B$
    * $(Map_{NIR} - Map_{Red}) / (Map_{NIR} + Map_{Red})$ (NDVI)
* Overlay (Vertical Integration)

## NDWI and mNDWI Example
* Normalized Difference Water Index (NDWI)
    * $NDWI = (Green - NIR) / (Green + NIR)$
* Modified NDWI (mNDWI)
    * $mNDWI = (Green - SWIR) / (Green + SWIR)$
* Uses local operations to enhance water features in satellite imagery



## Composite Image
* Combining multiple single-band raster maps into a single multi-band map
* Each band represents a different wavelength of light
* A local operation where the output is a multi-valued map

## Creating Rainfall Map using Elevation
* Relationship: $Rainfall = f(Elevation)$
* If a mathematical model exists (e.g., regression: $R = 0.5 \times Elev + 100$), it can be applied as a local operation to the elevation map

## Local Operations with Vector Features
* Calculating new attributes based on existing ones
* Example: Population Density = Population / Area
* Area is a geometric attribute of the MU itself

## Effective Local Neighborhood
* In a local operation, the "neighborhood" is the MU itself
* The operation only looks at the data within that specific unit to produce an output for that same unit

## Characterizing Effective Local Neighborhood
* Sometimes the output value depends on the geometry of the MU or the distribution of features within it
* Local Stats: Min, Max, Mean, Sum within the MU
* Examples:
    * LocalSum: Sum of points within a polygon (e.g., total population in a city)
    * LocalCount: Number of points within a polygon (e.g., number of crimes in a district)



## Summarize Data Toolset in ArcGIS
* **Aggregate Points**: Local operation using polygon MUs to count points within them
* **Summarize Within**: Local operation calculating statistics for features within a boundary (polygon/rectangle)

## Two Types of Local Operations Summary
* Type 1: Output MUs are the same as input MUs (Standard Map Algebra)
* Type 2: Characterize effective local neighborhood where output MUs may be different from the input MUs (e.g., points to polygons)

| Feature Type | Geometry attribute |
| :--- | :--- |
| **Point** | Count |
| **Line** | Length |
| **Polygon** | Area, Perimeter |