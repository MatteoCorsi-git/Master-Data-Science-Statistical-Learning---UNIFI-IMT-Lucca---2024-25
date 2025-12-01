Here is the English version of the README.md file, written in a professional tone, without emoticons, and ready for copy-pasting.

-----

# Geospatial Analysis of 2022 Italian General Elections

This repository contains a geospatial data analysis project developed in **R**. The project investigates the results of the 2022 Italian General Election (Chamber of Deputies), with a specific focus on the spatial distribution and determinants of the vote for the **Center-Right coalition**.

The analysis integrates electoral data with demographic and socioeconomic indicators to model voting behavior using Spatial Econometrics techniques.

## Project Overview

The primary objective of this project is to understand the spatial dependence of voting patterns and to model the relationship between the percentage of votes for the Center-Right coalition and local socioeconomic variables (age and income), controlling for spatial autocorrelation.

The workflow includes:

1.  **Data Handling:** Cleaning and normalization of raw datasets.
2.  **Feature Engineering & Merging:** Integration of disparate data sources using ISTAT municipality codes.
3.  **Exploratory Spatial Data Analysis (ESDA):** Calculation of Global and Local Moran's I.
4.  **Spatial Modeling:** Application of a Spatial Error Model (SEM).

## Data Sources

The final dataset is constructed by merging three official sources, all updated to 2022 reference periods:

| Data Type | Source | Description |
| :--- | :--- | :--- |
| **Electoral** | [Ministry of Interior (Eligendo)](https://elezioni.interno.gov.it/) | 2022 Chamber of Deputies election results by municipality. |
| **Demographics** | [ISTAT - Permanent Census](http://dati-censimentipermanenti.istat.it/) | Population structure, age indices, and aging population data. |
| **Income** | [MEF - Dept. of Finance](https://www1.finanze.gov.it/) | Taxable income (IRPEF) data and income bracket distribution. |
| **Boundaries** | ISTAT | Administrative boundaries (Shapefiles) of Italian municipalities. |

## Methodology

### 1\. Data Preparation

The initial phase involves handling raw CSV files and Shapefiles. Key steps include:

  * Standardizing municipality names and ISTAT codes to ensure consistent merging keys.
  * Handling missing values and data inconsistencies.
  * **Feature Engineering:** Creating derived variables such as *Average Income per Capita*, *Old Age Index*, and the dependent variable *Percentage of Votes for Center-Right*.

### 2\. Exploratory Spatial Data Analysis (ESDA)

To detect spatial autocorrelation in the voting patterns, the following indices were calculated:

  * **Global Moran's I:** Used to test for the presence of overall spatial clustering in the dataset.
    $$I = \frac{N}{W} \frac{\sum_i \sum_j w_{ij} (x_i - \bar{x}) (x_j - \bar{x})}{\sum_i (x_i - \bar{x})^2}$$
  * **Local Moran's I (LISA):** Used to identify local clusters (Hotspots and Coldspots) and spatial outliers to map regional voting polarizations.

### 3\. Spatial Modeling (SEM)

Standard OLS regression often violates the assumption of independent errors in geospatial data. To address this, a **Spatial Error Model (SEM)** was implemented. The SEM assumes that spatial dependence enters through the error term (e.g., due to unobserved spatially correlated covariates).

The model specification is:

$$y = X\beta + u$$
$$u = \lambda Wu + \epsilon$$

Where:

  * $y$ is the vector of the dependent variable (% Center-Right votes).
  * $X$ is the matrix of explanatory variables (Income, Age).
  * $W$ is the spatial weights matrix.
  * $\lambda$ (Lambda) is the spatial error coefficient.
  * $\epsilon$ is the vector of uncorrelated error terms.

## Technologies and Libraries

The project is entirely built using **R**. The core libraries used include:

  * **Data Manipulation:** `tidyverse` (`dplyr`, `tidyr`, `readr`)
  * **Geospatial Data:** `sf` (Simple Features)
  * **Spatial Analysis:** `spdep`, `spatialreg`
  * **Visualization:** `ggplot2`

## Usage

To replicate this analysis:

1.  Clone this repository.
2.  Open the project in RStudio.
3.  Ensure the required packages are installed:
    ```r
    install.packages(c("tidyverse", "sf", "spdep", "spatialreg", "tmap"))
    ```
4.  Run the main R Markdown file or the provided R scripts to generate the analysis and maps.
