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

# Multi-criteria Suitability Analysis

## Plan for the Rest of Semester
* Suitability analysis
* Point pattern analysis
* Spatial autocorrelation
* Note: Won't cover spatial interpolation
* No lab 12 (focus on final project instead)

## Multi-Criteria Evaluation (MCE)
* Evaluate a number of alternatives based on a set of criteria (factors)
* Calculate criterion/factor scores for each alternative
    * Score standardization (e.g., 1 to 10 points)
* Combine factors
    * Adding factor scores
    * Applying factor weights (relative importance of the factors)
* Rank alternatives based on the combined scores



## Spatial MCE (Suitability Analysis)
* Rank sites/locations with a set of criteria/factors
* Alternatives:
    * Features (points, lines and polygons in the vector data model)
    * Cells (raster data model)



## Siting a New School Example
* A small town in Vermont has experienced a substantial increase in population
* A new school must be built to take the pressure off existing schools
* Task: Find potential sites as a GIS analyst

## Potential School Site Criteria
* Factor 1: Land use
    * Avoid steep slopes and wetlands
    * Preferred land use types: open land, forest, or pasture
* Factor 2: Proximity to existing schools
    * Not too close to existing schools
* Factor 3: Proximity to recreational facilities
    * Close to parks or existing recreational facilities



## Suitability Analysis Procedure
1. Determine factors and constraints
2. Derive factor maps
3. Standardize factor scores (Reclassify)
4. Determine factor weights
5. Combine factors (Weighted sum)
6. Choose the best sites

## Step 1: Factors and Constraints
* Factors: Criteria that define the degree of suitability (e.g., distance to parks)
* Constraints: Criteria that limit the alternatives (e.g., excluding wetlands or existing urban areas)
    * Binary: 1 (suitable) or 0 (not suitable)

## Step 2: Derive Factor Maps
* Distance to schools (Euclidean distance global operation)
* Distance to recreation sites (Euclidean distance global operation)
* Slope (Focal operation from DEM)
* Land use (Input categorical map)

## Step 3: Standardize Factor Scores
* Factors are measured in different units (meters, degrees, categories)
* Reclassify them into a common scale (e.g., 1 to 10)
* High score = More suitable
* Low score = Less suitable



## Standardizing Distance to Schools
* Goal: Sites should be further away from existing schools
* 0 - 1000m: 1 (least suitable)
* 1000 - 2000m: 3
* 2000 - 3000m: 6
* 3000 - 4000m: 10 (most suitable)

## Standardizing Land Use
* Forest: 10
* Pasture: 5
* Water: 0 (Constraint)
* Urban: 0 (Constraint)

## Step 4 & 5: Combine Factors
* Simple Addition (Equal weights)
    * $Total Score = Factor1 + Factor2 + Factor3 + Factor4$
* Weighted Linear Combination (WLC)
    * $Total Score = \sum (Weight_i \times Score_i)$
    * Sum of weights must equal 1.0

## Calculation Example
* Factors: Landuse (0.3), Recreation (0.3), School (0.2), Slope (0.2)
* Factor scores at a cell: 10, 10, 2, 5
* Calculation: $0.3(10) + 0.3(10) + 0.2(2) + 0.2(5) = 7.4$
* Compared to simple average: $27 / 4 = 6.75$



## Analytic Hierarchy Process (AHP)
* Used to determine factor weights when it is difficult to assign numbers directly
* Organizes factors into a tree structure
* Decomposes complex decisions into simpler comparisons
* Derives weights by comparing the relative importance between two factors at a time



## AHP Factor Weights Determination
* Factor relative importance through pairwise comparison using a 9-point scale:
    * 1: Equally important
    * 3: Moderately more important
    * 5: Strongly more important
    * 7: Very strongly more important
    * 9: Extremely more important
* The best weights are calculated to fit into a pairwise comparison matrix

## Summary of Suitability Analysis
* Suitability analysis identifies the best locations based on multiple geographical factors
* Requires standardization of diverse data types into a unified scoring system
* Weighted combinations allow analysts to prioritize certain factors over others
* The final output is a suitability map where higher values indicate better alternatives