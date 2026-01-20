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

# Spatial Relations: Co-location

## Topics
* Co-locational spatial relationship
* Readings: Lloyd Chp. 5

## Fundamental/Basic Spatial Relationships
* Relationships between two attribute values
    * >, <
    * difference, ratio
* Relationships between two locations (spatial relationships)
    * = (occupy the exact same space)
    * Co-locate (share some space, i.e., overlap in space)
    * Distance (no co-locate)
* Mapping unit as location in practice

## Co-locational Relationships
* Share some space
* Qualitative co-locational relationship
    * Intersect, touch, contain, ..., disjoint
    * Independent of coordinates
    * Topological relationship
* Quantitative co-locational relationship
    * Where is the shared (or not shared) space located?
    * Based on and derived from coordinates

## Qualitative Locational (Topological) Relationship
* Locations that share some space
    * intersect, touch, contain, ...
* Most GIS support some common spatial relationships
    * Hard to define precisely
    * intersect, touch, contain, ...
* Dimensionally Extended 9-Intersection Model (DE-9IM)
    * Decompose a MU into interior, boundary and exterior
    * Relationship base on the dimensionality of the intersection of boundary, interior, and exterior
    * 9-intersection model (9IM) is a special case (Egenhofer and Herring, 1991)



## DE-9IM
* A feature decomposed into interior (I), boundary (B) and exterior (E)

| Feature Type | Interior (I) | Boundary (B) | Exterior (E) |
| :--- | :--- | :--- | :--- |
| **Polygon** | points within the polygon | the rings | points not in the polygon |
| **Line** | points of the line except endpoints | the endpoints | points not on the line |
| **Point** | the point | empty set | points other than the point |

* Dimensionality of intersection: {None (-1), Point (0), Line (1), Area (2)}

## DE-9IM Examples
* A contains B: $I(B) \cap E(A) = \varnothing$ and $I(A) \cap I(B) \neq \varnothing$
* A disjoint B: $I(A) \cap I(B) = \varnothing$ and $I(A) \cap B(B) = \varnothing$ and $B(A) \cap I(B) = \varnothing$ and $B(A) \cap B(B) = \varnothing$



## Quantitative Co-locational Relationship
* Where is the shared/not shared space located?
* Use mapping units (MUs) as the location
    * New MUs created as the result of overlapping existing MUs
    * Also called Map Overlay
    * Attributes of new MUs are associated with original attributes

## Map Overlay
* Create new maps (MUs) based on existing maps (MUs)
* Vertical integration
* Two steps
    1. Determine the geometry of new mapping units
        * Overlap existing mapping units
    2. Assign attribute values to the new mapping units
        * Inherit from existing mapping units



## Geometry of New Mapping Units
* Intersect boundaries of original MUs to create new MUs
* New MUs are more "homogeneous" than original MUs

## Identify Relations between MUs
* For two maps A and B, four kinds of new mapping units (at most) can be created:
    * MUs in A and also in B (A AND B)
    * MUs in A but not in B (A NOT B)
    * MUs in B but not in A (B NOT A)
    * MUs neither in A nor in B (NOT A AND NOT B)
* Total space = (A AND B) + (A NOT B) + (B NOT A) + (NOT A AND NOT B)



## Map Overlay on Raster Maps
* Determine the geometry of new MUs
    * Two raster maps must have the same "geometry"
        * Same resolution, same orientation, same extent
    * New MUs are just the original cells
* Assign attribute values to the new MUs
    * Combine values of original cells at the same location
    * Map Algebra (Tomlin, 1990)
* Relation between cells is 1-to-1



## Map Overlay on Vector Maps
* Determine the geometry of new MUs
    * Intersect boundaries of original MUs to create new MUs
* Assign attribute values to the new MUs
    * Combine values of original MUs
* Relation between MUs is typically M-to-N



## Attributes of the New Mapping Units
* Typically a combination of the attributes of the original mapping units
    * Multi-valued map
    * $Value_{new} = \{Value_A, Value_B\}$
* A new attribute value can be calculated based on original values
    * $Value_{new} = f(Value_A, Value_B)$
    * Boolean (0, 1), Arithmetic (+, -, *, /)

## Overlay Tools in ArcGIS
* Different tools keep different kinds of new MUs
* Intersect, Union, Identity, Erase, Symmetrical Difference, Update

## Map ArcGIS Overlay Tools to Kinds of MUs Kept
* One kind of MUs
    * A AND B (intersect)
    * A NOT B (erase)
    * B NOT A (erase)
* Two kinds of MUs
    * A NOT B, A AND B (identity)
    * B NOT A, A AND B (identity)
    * A NOT B and B NOT A (symmetrical difference)
* All kinds of MUs
    * A AND B, A NOT B, B NOT A (union)

## Clip Tool in ArcGIS
* What’s the difference between Intersect and Clip tool?
    * Attributes of the new MUs
    * Clip tool in the Extract toolset—Why?
* How about Erase tool?

## Other Overlay Tools in ArcGIS
* Two steps
    * Choose output MUs for the new map
    * Process/handle related MUs (including attributes)

## Overlay and Attribute Table
* Number of new MUs (rows)
    * Vector: Usually increases
    * Raster: Stays the same
* Number of attributes (columns)
    * Usually increases (attributes from both original maps)


## Dimensionally Extended Nine-Intersection Model (DE-9IM)

**Author:** Christian Strobl, German Remote Sensing Data Center (DFD), German Aerospace Center (DLR)

## Synonyms
Dimensionally Extended Nine-Intersection Model (DE-9IM), Nine-Intersection Model (9IM), Four-Intersection Model (4IM), Egenhofer Operators, Clementini Operators; Topological Operators.

## Definition
The Dimensionally Extended Nine-Intersection Model (DE-9IM) or Clementini-Matrix is specified by the OGC "Simple Features for SQL" specification for computing the spatial relationships between geometries. 

It is based on the Nine-Intersection Model (9IM) or Egenhofer-Matrix, which is an extension of the Four-Intersection Model (4IM). The DE-9IM considers the two objects' interiors, boundaries, and exteriors and analyzes the intersections of these nine parts for their relationships. The model records the maximum dimension (-1, 0, 1, or 2) of the intersection geometries, where -1 corresponds to no intersection (empty set).

The primary spatial relationships described by the DE-9IM are:
* Equals
* Disjoint
* Intersects
* Touches
* Crosses
* Within
* Contains
* Overlaps

## Main Text
There are three common approaches for describing topological relationships between geodata, each based on an intersection matrix.

### Four-Intersection Model (4IM)
The 4IM considers only the interior and the boundary of two objects. It creates a 2x2 matrix that describes whether the intersections between the interiors and boundaries of objects A and B are empty (0) or non-empty (1).

### Nine-Intersection Model (9IM)
The 9IM extends the 4IM by including the exterior of the objects. This results in a 3x3 matrix. Like the 4IM, it traditionally uses boolean values (empty or non-empty) to describe the intersections of Interior (I), Boundary (B), and Exterior (E).



### Dimensionally Extended Nine-Intersection Model (DE-9IM)
The DE-9IM further refines the 9IM by recording the **dimension** of the intersection rather than just a boolean state.

The intersection of any two parts results in a set of points. The value in the DE-9IM matrix is the maximum dimension of this point set:
* **-1**: The intersection is empty ($\emptyset$).
* **0**: The intersection contains only points (0-dimensional).
* **1**: The intersection contains lines (1-dimensional).
* **2**: The intersection contains polygons/areas (2-dimensional).

The matrix is structured as follows:

| | Interior(B) | Boundary(B) | Exterior(B) |
| :--- | :---: | :---: | :---: |
| **Interior(A)** | dim(I(A)∩I(B)) | dim(I(A)∩B(B)) | dim(I(A)∩E(B)) |
| **Boundary(A)** | dim(B(A)∩I(B)) | dim(B(A)∩B(B)) | dim(B(A)∩E(B)) |
| **Exterior(A)** | dim(E(A)∩I(B)) | dim(E(A)∩B(B)) | dim(E(A)∩E(B)) |

## Geometric Operators and Predicates

### Disjoint
$A \cap B = \emptyset$
The interiors and boundaries of the two geometries do not intersect at all.
* Pattern: `FF*FF****`



### Intersects
$A \cap B \neq \emptyset$
The complement of Disjoint. The geometries share at least one point.
* Pattern: `T********` or `*T*******` or `***T*****` or `****T****`

### Touches
$A \cap B \neq \emptyset$, but $Interior(A) \cap Interior(B) = \emptyset$.
The geometries have at least one point in common, but their interiors do not overlap. This applies to Area/Area, Line/Line, Line/Area, and Point/Area, but not Point/Point.
* Pattern: `FT*******` or `F**T*****` or `F***T****`



### Crosses
The geometries share some but not all interior points, and the dimension of the intersection is less than the maximum dimension of the two geometries.
* Pattern: `T*T******` (for Line/Area) or `0********` (for Line/Line)



### Within
The geometry A lies entirely within the interior of B.
* Pattern: `T*F**F***`

### Contains
The inverse of Within. Geometry B is within Geometry A.
* Pattern: `T*****FF*`

### Overlaps
The geometries share some but not all points in common, and the intersection has the same dimension as the geometries themselves.
* Pattern: `T*T***T**` (for Area/Area) or `1*T***T**` (for Line/Line)



### Equals
The two geometries are topologically equal; they occupy the same space.
* Pattern: `T*F**FFF*`

## Summary
The DE-9IM is a powerful mathematical framework that allows GIS systems to query spatial relationships between complex objects rigorously. By using a 3x3 matrix of dimensions, it provides a unique "fingerprint" for every possible topological configuration between two geometric features.