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

# The Map Compute Framework

## Topics
* Overview of spatial data analysis
* Overview of Map Compute Framework (MCF)
* MCF vs Map Algebra (Cartographic Modelling)

## Spatial Data Analysis: A Continuum of Sophistication
* Measure/Mapping
    * Systematically collecting geospatial data (location + attributes)
    * Create regular maps ({location: {attributes}})
* Visualize
    * Present geospatial data for human interpretation and understanding
    * Show maps (variation in space)
* Query
    * Maps as stored functions
    * Attribute, spatial and compound queries
    * {location: {attributes}}
    * Linkage between location and attributes
* Predict/estimate value at a location/MU
    * $a = f(l)$
    * Entanglement between location and attributes (population)

## Spatial Data Analysis: A Continuum of Sophistication
* Model geospatial interactional relationships and processes
    * Exchange of matter, energy and information in space
    * Create meta-maps ({location: {(location: {attributes})})
* Fundamental geospatial interactional relationships
    * Co-locational relationship
    * Distance as a proxy of interactional relationship
        * Euclidean and non-Euclidean distance (cost distance)
* Spatial auto-correlation
    * How attribute is self-correlated in space
    * First law of geography
* Domain geospatial interactional relationships
    * Physical, biological and social processes involved in the exchange of matter, energy and information on or close to earth surface
    * Hydrology, ATM, etc.

## Map Compute Framework (MCF)
* A comprehensive framework for analyzing geospatial data
    * Based on the concept of "Map as Function"
    * Focuses on the "Compute" part of GIS
* Two components
    * Data model: How to represent geospatial data (MUs and attributes)
    * Computational model: How to manipulate and analyze geospatial data
* Key elements
    * Mapping Units (MU)
    * Attributes
    * Spatial relationships (neighborhoods)
    * Operations (local, focal, zonal, global)



## Mapping Units (MU)
* Discrete divisions of space
* Used as the domain of the map function
* Types of MUs
    * Regular: Raster cells (squares, hexagons, etc.)
    * Irregular: Points, lines, polygons (vector features)
* Resolution and precision
    * Size and shape of MUs affect the quality of data and analysis

## Attributes
* Qualitative or quantitative characteristics of a MU
* Used as the co-domain of the map function
* Levels of measurement
    * Nominal, ordinal, interval, ratio
* Single-valued vs. multi-valued maps

## Spatial Relationships (Neighborhoods)
* How MUs are related to each other in space
* Used to model interactional processes
* Types of neighborhoods
    * Immediate: Adjacent MUs (topology)
    * Proximity: MUs within a certain distance
    * Domain-specific: Watersheds, viewsheds, network connectivity
* Neighborhood is a mapping: $MU \to \{MU\}$



## Map Operations
* Mathematical or logical operations applied to maps
* Classified by their spatial scope (Tomlin, 1990)
* Local operations
    * Output value at a location depends only on the input value(s) at the same location
* Focal operations
    * Output value depends on the input values within a neighborhood of the location
* Zonal operations
    * Output value depends on the input values within a predefined zone
* Global operations
    * Output value depends on the input values of the entire map

## Local Operations
* $Value_{new} = f(Value_{old})$
* Cell-by-cell or feature-by-feature processing
* Examples:
    * Scalar math (e.g., $map \times 2$)
    * Map overlay (e.g., $map_A + map_B$)
    * Reclassification



## Focal Operations
* $Value_{new} = f(Values\ in\ neighborhood)$
* Also known as neighborhood operations
* Requires a predefined neighborhood (kernel/window)
* Examples:
    * Smoothing (mean), edge detection, slope, aspect
    * Focal flow (hydrology)



## Zonal Operations
* $Value_{new} = f(Values\ in\ zone)$
* Two input maps:
    * Zone map: Defines the zones
    * Value map: Contains the attributes to be summarized
* Examples:
    * Average elevation per watershed
    * Total population per county



## Global Operations
* $Value_{new} = f(Values\ in\ entire\ map)$
* Examples:
    * Global mean, maximum, or minimum
    * Euclidean distance (from a source to all other points)
    * Least cost path analysis

## Tomlin’s Map Algebra
* Simple but powerful approach/tools for analyzing geospatial raster data
    * Primary way of analyzing raster data
    * Implemented in commercial/open source GIS software
* All the existing extensions followed the original framework
    * Local, focal, zonal
* Remaining issues
    * Inconsistent structure (focal vs zonal)
    * Limited (enumerated) neighborhoods
    * Only available for raster data

## Map Algebra Operations in the MC Framework
* Local operations
    * Cells as MUs
* Focal operations
    * Cells as MUs
    * Predefined (and limited) neighborhoods
    * Doesn't distinguish using and modeling geospatial interactional relationships
* Zonal operations
    * Zones as neighborhoods (focal operations)
    * Zones as analysis units (local operations)
* Concepts in MC but labs and tools are still using MA!
    * Map Compute Engine (MCE) is not entirely implemented yet

| Mapping Units | Neighborhood Relation: Local | Neighborhood Relation: Focal | Neighborhood Relation: Global |
| :--- | :--- | :--- | :--- |
| **Cells** | Local | Focal | Global |
| **Raster zones** | Zonal | | |
| **Features (vectors)** | | | |

## Readings
* Tomlin, 2017 Cartographic modeling, The International Encyclopedia of Geography