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

# Basic Statistics

## Topics
* Basic statistics on attributes
* Basic statistics on location
    * Readings: Lloyd Chp. 3, 4

## Statistics on Attributes (Chp. 3)
* Statistics on attributes
    * Univariate statistics
    * Multivariate statistics
    * Inferential statistics

## Descriptive Statistics for Attributes
* Measures of central tendency
    * Mean, median, mode
* Measures of dispersion
    * Range, minimum, maximum
    * Variance and standard deviation
        * The extent to which values vary from the mean
    * Coefficient of variation (CV)

## Multivariate statistics-- Correlation Coefficient
* How two attributes are related to each other
* Correlation Coefficient
    * A (normalized) measurement of the covariance of two variables
    * Has a value between -1 and 1
    * Formula: $r=\frac{\sum_{i=1}^{n}(y_{i}-\overline{y})(z_{i}-\overline{z})}{\sqrt{\sum_{i=1}^{n}(y_{i}-\overline{y})^{2}}\sqrt{\sum_{i=1}^{n}(z_{i}-\overline{z})^{2}}}$

| Variable 1 (y) | Variable 2 (zᵢ) | (yᵢ-ȳ) | (zᵢ-ž) | (yᵢ-ȳ)×(zᵢ-ž) | (yᵢ-ȳ)² | (zⱼ-ž)² |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 12 | 6 | -20.11 | -27.00 | 543.00 | 404.46 | 729.00 |
| 34 | 52 | 1.89 | 19.00 | 35.89 | 3.57 | 361.00 |
| 32 | 41 | -0.11 | 8.00 | -0.89 | 0.01 | 64.00 |
| 12 | 25 | -20.11 | -8.00 | 160.89 | 404.46 | 64.00 |
| 11 | 22 | -21.11 | -11.00 | 232.22 | 445.68 | 121.00 |
| 14 | 9 | -18.11 | -24.00 | 434.67 | 328.01 | 576.00 |
| 56 | 43 | 23.89 | 10.00 | 238.89 | 570.68 | 100.00 |
| 75 | 67 | 42.89 | 34.00 | 1458.22 | 1839.46 | 1156.00 |
| 43 | 32 | 10.89 | -1.00 | -10.89 | 118.57 | 1.00 |
| **SUM** | | | | **3092** | **4114.89** | **3172.00** |

* Calculation:
    * Numerator: 3092
    * Denominator: $\sqrt{4114.89} \times \sqrt{3172.00} = 64.1474 \times 56.3205 = 3612.8136$
    * $r = 3092 / 3612.8136 = 0.8558$

## Multivariate statistics--Linear Regression
* Relationship between dependent and independent variable(s)
* Ordinary least square regression
    * Least square approach
    * Minimize the sum of squared errors (residuals)
    * Coefficients are calculated by solving a set of equations
    * Equation: $z = a * y + b$
        * a — slope
        * b — intercept
* Example: $z = 8.8711 + 0.7514y$
    * $r^2 = 0.7325$
* Goodness of fit
    * Coefficient of determination
    * Percent of variation in z explained by y
    * $r^2 = (\text{correlation coefficient})^2$



## Geospatial Statistics on Attributes
* Conventional correlation and linear regression
    * Two variables measured on the same subjects
    * Variables related by subjects
* Geospatial correlation and linear regression
    * Variables related by location (and time)
    * Two variables at the same location
        * Example: temperature ~ elevation regression
    * Geographically weighted regression
        * Two variables nearby a location
* Spatial auto-correlation
    * How a variable is related to itself in space (and time)
    * Same attribute at two different locations

## Descriptive Statistics for Locations (Chp. 7.2)
* Where is the center of a geographic distribution
* How features are distributed around their center
* Why measure geographic distributions?
    * Know the general location of geographic features
    * Compare the distributions of different features/phenomena
    * Track changes of distribution in time
* Modified from one dimension (attribute) to two dimensions

## Mean Center
* The mean of X and Y coordinates
* Minimizing the sum of the squares of the distance to each point
* Center of mass/gravity
* Sensitive to extreme points
* Formula: $\overline{X} = \sum X_i / N, \overline{Y} = \sum Y_i / N$

## Central Feature and Median Center
* Central feature
    * The most centrally located feature
    * Shortest total distance from all the other features
* Median center
    * Minimizing the sum of the distances to each point
    * Less influenced by outliers
    * No simple formula (iterative process)

## Weighted Mean Center
* Center influenced by the attribute at a location
* Center of gravity
* Formula: $\overline{X}_w = \frac{\sum W_i X_i}{\sum W_i}, \overline{Y}_w = \frac{\sum W_i Y_i}{\sum W_i}$
* Example:
    * Points: (5, 0), (2, 4), (5, 8) with weights 2, 4, 4
    * Mean center (4, 4)
    * Weighted mean center (4.4, 4)



## Standard Distance
* How feature locations deviate from their mean center
* Average distance to mean center
* Two dimensional equivalent of standard deviation
* Compactness (dispersed vs. clustered)
* Formula: $S_{xy} = \sqrt{\frac{\sum (X_i - \overline{X})^2 + \sum (Y_i - \overline{Y})^2}{N}}$



## Standard Deviation Ellipse
* Standard distance does not show directional trend (anisotropy)
* The standard deviation ellipse gives dispersion and direction measure



## Standard Deviational Ellipse Example
* Example: Monthly mean centers of tornado touchdown locations from 1950 to 2004

## Lab #1—Descriptive Spatial Statistics
* Lab #1—Descriptive Spatial Statistics