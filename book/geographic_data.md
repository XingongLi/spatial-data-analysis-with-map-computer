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

# Geospatial Data

## Topics
* Geospatial data
* Measurement and reference systems
* Mapping and measurement frameworks
* Map as stored function
* Types of maps

## Geospatial/Geographic Data
* Data about things on or close to the Earth's surface
* Terminology: Spatial, geospatial, or geographic data
* Scale: Operates at an Earth or planet scale
    * Spatial location
    * Spatial > geospatial
    * Geospatial = geographical
* Three components
    * Attribute (what)
    * Location (where)
    * Time (when)

## Why Do We Need Geospatial Data?
* Life is spatial
    * Life itself (matter) takes up space
    * It distinguishes itself from its environment
    * It interacts with the environment
    * It lives in space
* Spatial intelligence
    * One of Howard Gardner's multiple intelligences
    * Involves immediate sensory perception
* Geographical intelligence
    * Insight beyond the line-of-sight
    * Insight beyond sensory perception



[Image of Howard Gardner's multiple intelligences theory]


## Life and Information
* What is life?
    * The basis of life is information processing
    * Life collects, stores, and uses information
    * Applies to biological and artificial life, organizations, and the economy
* What is information?
    * Something that allows an observer to make predictions about the state of another system that are better than chance
* Information vs. Data
    * Data becomes information when it enables better-than-chance predictions about another system

## Measurement and Reference Systems
* Measurement
    * Classical physicist perspective: Provides a numerical relationship between a standard object and the object being measured
    * Representationalists perspective: Assignment of numbers to objects according to certain rules
    * Useful data includes both the numbers and the standard objects or rules used
* Measurement reference systems
    * A set of rules for measurement or standard objects
    * Provides a means to compare a particular number to others measured under the same set of rules

## Measurement Reference Systems
* Reference systems exist for attribute, time, and space
* Temporal reference systems
    * Local vs. global time
    * Gregorian vs. lunar calendars
* Attribute reference systems
    * Units (standard objects)
    * Levels of measurement: Nominal, Ordinal, Interval, and Ratio
* Running race example
    * A number to wear (Nominal)
    * The order of finishing the race (Ordinal)
    * Arrival time (Interval)
    * Elapsed running time (Ratio)

| Su | Mo | Tu | We | Th | Fr | Sa |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 31 | 1 | 2 | 3 | 4 | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 | 1 | 2 | 3 |

## Spatial Reference Systems
* Location distinguishes geospatial data from other types of data
    * Specifying location on the Earth's surface is essential
* Geospatial coordinate systems are designed to:
    * Define locations on or close to the Earth's irregular curved surface
    * Ensure each location is uniquely represented
    * Allow calculations of relationships such as distance and direction

## Geographic Coordinate Systems (GCS)
* Based on a spheroid model of the Earth
* Uses two angular measurements (latitude and longitude) to specify a location
* Components of a GCS:

| Geographic Coordinate System |
| :--- |
| Datum (Sphere or Ellipsoid) |
| Unit of Measure (DMS, DD, or Radian) |
| Prime Meridian |



[Image of geographic coordinate system latitude and longitude]


## (Horizontal) Datum
* A datum specifies a sphere or ellipsoid used to approximate the Earth's shape and size
* It defines how that model is aligned with the Earth
* Latitude and longitude are defined based on specific datums
* The same location may have different coordinates depending on the datum used
    * Earth-centered (WGS84) datum
    * Local (NAD27) datum

## Projected Coordinate Systems (PCS)
* A PCS consists of:

| Projected Coordinate System |
| :--- |
| A linear unit of measure (usually meters or feet) |
| A map projection with specific parameters |
| An underlying Geographic Coordinate System |

## GCS vs. PCS
* PCS is suitable for small areas
* PCS always contains some form of distortion
* GCS calculations for distance and area are more accurate but more complex
    * Uses spherical geometry
* Most GIS analytical functions are implemented based on PCS
* Use PCS primarily for printing or display on flat media

## Height and Vertical Datum
* The vertical datum is the zero surface to which elevation refers
* Geoids (equipotential surfaces) are standard zero surfaces
* Ellipsoids can also be used, such as in GPS readings
* The same location may have different elevation values based on different vertical datums



## Mapping—Creating Geographic Data
* The process involves turning things on or near the Earth's surface into data
    * Representing reality as numbers in a computer
* What is measured:
    * Objects and fields on or close to the Earth's surface
    * Location, attribute, and time components
* Considerations and constraints:
    * Purpose and resources/cost
    * Resolution and precision
    * Limitations of finite computing systems

## Mapping and Measurement Frameworks
* Geospatial data consists of location, attribute, and time components
    * All three components cannot be measured simultaneously
* Measurement frameworks provide rules for ignoring or controlling some components to measure one
    * One component must be fixed (irrelevant)
    * Another component serves as control (imposes discrete divisions)
* Discrete divisions constrain the resolution and accuracy of the measurement

## Common Mapping Measurement Frameworks
* Time is fixed: Measured at a specific point in time or during a period
* Location as control: Space is divided into cells, polygons, or administrative boundaries
    * Attributes are then measured for these divisions
* Attribute as control: Specific attributes (e.g., land cover types or elevations) are chosen
    * Locations are then measured for these attributes

## Mapping Surface Elevation—Raster Map
* Location serves as the control
    * Space is systematically divided into cells
* Attributes are measured at each cell
    * Rules like min, max, or mean may be applied
* Cell values are typically stored as a matrix



## Mapping Surface Elevation—Vector Map
* Attribute serves as the control
    * Focuses on discrete elevations (e.g., every 100m)
* Locations are measured for each elevation (e.g., contour lines)
* Location-value pairs are stored as rows in a table

| ID | Location/Geometry | Elevation |
| :--- | :--- | :--- |
| 1 | (x1,y1), (x2,y2) … (xn, yn) | 100 |
| 2 | (x1,y1), (x2,y2) … (xm, ym) | 200 |
| 10 | (x1,y1), (x2,y2) … (xk, yk) | 1000 |

## Vector Census Map
* Location serves as the control
    * Uses census blocks or aggregated boundaries
* Population is counted based on set rules

## Function and Map
* A function associates each element x of a domain to a single element y of a codomain
* Analogy for maps: Location represents the domain, and the measured attribute represents the codomain

## Stored Function
* Relations are explicitly stored when they cannot be represented mathematically
* A stored function acts as a lookup table
* Locations must be discretized (mapping units) due to finite computing power

## Map as Stored Function
* Relation between location and attribute: $Attribute = f(location)$
* Domain: Location on Earth
* Codomain: Any measured attributes/variables
* Map is a stored function because location-value relations usually lack mathematical formulas

## Raster Map
* Matrix serves as a stored function
    * Each cell is located by its row and column
* Each cell represents a location-value relation
* Usually, the upper-left corner cell is georeferenced; other locations are derived

## Zone Raster Map
* Cells with the same value form a "zone"
* The zone serves as the mapping unit location
* Typically includes an attribute table with counts/histograms

| Zone ID | Count | Value |
| :--- | :--- | :--- |
| 0 | 50 | 200 |
| 1 | 50 | 325.6 |

## Predicting Attribute Value at a Location
* Map as a function: Prediction is a fundamental capability ($v = m(l)$)
* Estimation/Interpolation is necessary when the target mapping unit differs from stored units

## Interpolating Attribute Value
* Land cover interpolation: Uses majority types for target polygons
* Population interpolation: Uses areal interpolation
* Attribute types:
    * Intensive: Magnitude independent of size (e.g., density)
    * Extensive: Magnitude is additive (e.g., mass, population)
* Spatially intensive: Value is the same everywhere within a mapping unit
* Spatially extensive: Value changes if the mapping unit is modified

## Multi-valued Vector Map
* Results from combining multiple single-valued maps (e.g., Soil + Land Cover)
* Each mapping unit represents a set of homogeneous attributes

| Map | Attributes |
| :--- | :--- |
| Soil | A, B |
| Land cover | C, D |
| Combined | (A, C), (A, D), (B, C), (B, D) |

## Multi-Valued Raster
* Each cell contains a set of attribute values (e.g., multi-band remote sensing)
* Storage methods: Band sequential (BSQ), Band interleaved by line (BIL), and Band interleaved by pixel (BIP)

## Meta-map: Map of Spatial Relationships
* Spatial relationship involves the exchange of matter, energy, and information between locations
    * Examples include watersheds and viewsheds
* Types of map relations:
    * Single-valued: {Location, value}
    * Multi-valued: {Location, {values}}
    * Meta-map: {Location, {(location, {values})}} (a map of maps)



## Flood Inundation Relations
* Floodplain pixels (FPP) can be flooded by flood source pixels (FSP) through backfill and spillover
* Depth to flood (DTF): The minimum depth at an FSP required to flood a specific FPP
* The FLDPLN model identifies these relations and DTFs through an iterative process