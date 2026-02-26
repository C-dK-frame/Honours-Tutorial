# README
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/C-dK-frame/Honours-Tutorial.git/HEAD)

# Multivariate Analysis of Zooplankton Species Counts

This study investigates differences in zooplankton community composition
between two coastal sites: Silverstroom and Ganzekraal.

By analysing multivariate species count data, we identified patterns in
community structure and determine which taxa contribute most to
variation between sites.

# Data Collection

- Species count data were collected at two coastal sites (Silverstroom
  and Ganzekraal).
- Data were recorded in spreadsheets and saved as `.xlsx` files.

## Taxa Included

The following taxa were included in the analysis:

- Isopods
- Amphipods
- Nematodes
- Salps
- Copepoda
- Eggs
- Chaetognaths
- Polychaetes
- Crustacean larvae
- Egg mass
- Euphausiids
- Mysids
- Medusa
- Mites

All data represent species count data collected at each site. Abundance
and Species Richness were calculated, however were used in this
analysis.

# Data Processing

Data were imported into R using readxl, cleaned using tidyverse, and
analysed using vegan. Thus all analyses were conducted in **R** using
the following packages: - vegan - readxl - tidyverse

# Multivariate Analysis

Principal Component Analysis (PCA) was performed to: 1. Identify taxa
contributing most strongly to variation 2. Explore differences in
community composition between sites

# Plotting

A PCA scatterplot was created with:

- PC1 (Principal Component 1) on the x-axis
- PC2 (Principal Component 2) on the y-axis
- Points grouped by site (Silverstroom and Ganzekraal)

This allowed visual comparison of clustering and separation between
sites.

## Data Management Plan (DMP)

https://docs.google.com/document/d/1fbFzw74dLa4MQ3mgLuRevqsiYPF2WICUrJZ6oA81-w0/edit?usp=sharing

### Data Processing and documentation

- All data cleaning and analysis performed in R scripts.
- No raw data were overwritten during processing.
- This README file provides project context and workflow description.
- R scripts are annotated with comments explaining each step.
- Variable names are clearly defined and consistent across datasets.
