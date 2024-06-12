# [project name]
DSC 80 Spring 2024 Final Project
<br> Authors: Adrian Apsay, Ethan Flores

# Introduction
Welcome to our DSC 80 final project, where we aim to explore and gain insights focused on major power outage risks in the United States.  Over the past two decades, America has experienced numerous major outages, thus affecting millions of individuals causing numerous disruptions across the country. These outages highlight the urgent need for proactive measures to mitigate risks and enhance the resilience of our electrical grid.

We want to investigate the relationship of outage duration and severity based on the economic output of a given state. We hypothesize that states with lower economic output results in greater outage duration and severity due to the lack of resources and funds to maintain infrastructure that powers the electricity of the state. This question will provide insight into the economic productivity and performance of each state on a per-person basis, making it useful for comparing the economic status of different states based on the impact of power outages. By exploring this relationship, as represented by PC.REALGSP.STATE, we can assess how disruptions in electricity supply that provide power is affected by the economic well-being of each state. This analysis pinpoints vulnerabilities in states with lower economic output per capita, guiding policy decisions to enhance resilience to power outages and boost overall economic productivity for infrastructure funding.

Our dataset, derived from the article titled 'A Multi-Hazard Approach to Assess Severe Weather-Induced Major Power Outage Risks in the U.S.' by Mukherjee et al. (2018), covers the period from January 2000 to July 2016. It provides comprehensive information about severe weather-induced major power outages in the United States, including the geographical locations of the outages, regional climatic data, land-use characteristics, electricity consumption patterns, and economic indicators of the states affected by the outages. As defined by the Department of Energy, the major outages refer to those that impacted at least 50,000 customers or caused an unplanned firm load loss of at least 300 MW. The dataset, after simple formatting, contains a total of 1534 rows and 56 columns.  The key columns are listed below: 

|Column                |Description|
|---                |---        |
|`'YEAR'`                |Year an outage occurred|
|`'U.S._STATE'`                |State the outage occurred in|
|`'OUTAGE.DURATION'`                |Duration of outage events (in minutes)|
|`'PC.REALGSP.STATE'`                |Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)|
|`'UTIL.REALGSP'`                |Real GSP contributed by Utility industry (measured in 2009 chained U.S. dollars)|


# Data Cleaning and Exploratory Data Analysis
## Data Cleaning
The dataset cont They are as follows: [cols].

## Univariate Analysis

## Bivariate Analysis
<iframe
  src="assets/bivariate_graph_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Interesting Aggregates

# Assessment of Missingness

## NMAR Analysis

## Missingness Dependency

    
# Hypothesis Testing

    
# Framing a Prediction Problem

    
# Basline Model

    
# Final Model

    
# Fairness Analysis


~~~~~~~~~
null: The mean outage duration for power outages caused by "cold" weather is equal to the mean outage duration for power outages caused by "warm" weather.
alternative: the mean outage duration for power outages caused by "cold" weather is different from the mean outage duration for power outages caused by "warm" weather.

