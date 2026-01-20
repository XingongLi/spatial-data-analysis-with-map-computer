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

# Spatial Autocorrelation

Characterize overall attribute pattern in space

## Analyze and Map Spatial Variations
* Spatial variation of the location of objects/events:
    * Spatial descriptive statistics (mean center, standard deviation ellipse).
    * Point pattern analysis (Randomness and cluster mapping).
* Spatial variation of attributes associated with objects/events:
    * Spatial autocorrelation (Moran's I).
* Spatial variation of relationships:
    * How relationships vary in space.

## Characterize Attribute Spatial Pattern
* Location randomness (Point patterns): Quadrat analysis and Nearest neighbor distance.
* Attribute randomness (Spatial autocorrelation):
    * How different is an observed attribute pattern from a random distribution?
    * Positive spatial autocorrelation: Similar values cluster together.
    * Negative spatial autocorrelation: Dissimilar values cluster together (checkerboard).


## First Law of Geography
* Waldo Tobler (1970): "Everything is related to everything else, but near things are more related than distant things."
* Spatial autocorrelation is a quantification of this law.

## Moran’s I
* The most common measure of spatial autocorrelation.
* Compares the attribute value at each location with the values at its neighboring locations.
* Formula components:
    * $z_i$: Deviation of an attribute for feature $i$ from its mean ($x_i - \bar{x}$).
    * $w_{i,j}$: Spatial weight between feature $i$ and $j$ (neighborhood definition).
    * $S_0$: Aggregate of all spatial weights.

## Interpreting Moran’s I
* Range is generally between -1.0 and +1.0.
* Positive value: Clustered pattern (Positive autocorrelation).
* Zero: Random pattern.
* Negative value: Dispersed/Checkerboard pattern (Negative autocorrelation).


## Spatial Weights ($w_{i,j}$)
* Define the neighborhood relationship for the autocorrelation calculation.
* Binary weights: 1 if $j$ is a neighbor of $i$, 0 otherwise.
* Distance-based weights: $1/d$ or $1/d^2$ (inverse distance).
* Adjacency-based:
    * Rook's Case: Share an edge.
    * Queen's Case: Share an edge or a corner.

## Significance Testing
* Null Hypothesis: The attribute being analyzed is randomly distributed among the features in the study area.
* Z-score and p-value are used to determine if the observed Moran's I index is statistically significant.
* If p < 0.05, we reject the null hypothesis of randomness.

## Spatial Lag
* The "spatial lag" of a variable is the weighted average of the values of its neighbors.
* $Lag(x_i) = \sum (w_{i,j} \times x_j)$
* Moran's I can be seen as the correlation between a variable and its spatial lag.

## Correlograms
* A plot of spatial autocorrelation (Moran’s I) against different distance "lags" (neighborhood sizes).
* Typically, autocorrelation is highest at short distances and decreases as distance increases.
* The point where it hits zero or stays flat indicates the "range" of spatial influence.

## Semivariance as a Measure of Difference
* While Moran's I measures similarity, semivariance measures difference.
* Computed from sample pairs at a certain distance $h$ (the lag).
* $\gamma(h) = \frac{1}{2N(h)} \sum [z(x_i) - z(x_i + h)]^2$

## The Variogram (or Semivariogram)
* A plot of semivariance versus distance (lag).
* Nugget: Measurement error or micro-scale variation at zero distance.
* Sill: The point where the variance flattens out.
* Range: The distance at which locations are no longer spatially autocorrelated.

## Summary
* Spatial autocorrelation helps distinguish between meaningful spatial patterns and random noise.
* Moran's I focuses on global similarity across a map.
* Variograms focus on the scale and distance of spatial dependence, often used as a precursor to spatial interpolation.