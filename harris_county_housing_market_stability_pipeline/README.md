# Housing Market Stability Analysis Pipeline in Harris County from 2017 to 2025

## Client Background
Harris County has asked us to explore the stability of the Housing Market in Harris County from 2017 to 2025, specifically for the population between the 25th and 50th percentile of earners. Harris County wants to ensure that this population has adequeate access to housing and that market conditions remain stable enough to prevent ongoing affordability challenges.

Harris County has determined they need 500 thousand houses for this population<sup><a href="#note1">1</a></sup>. The County has determined that an affordable house is 4 times the yearly 

# Databricks Medallion Architecture

This repository demonstrates a Databricks Medallion Architecture using
notebook-based pipelines for Bronze, Silver, and Gold layers.

## Structure
- **Bronze**: Raw ingestion
- **Silver**: Cleansed and standardized data
- **Gold**: Business-ready aggregates

## Technology
- Databricks
- Pyspark
- Sql

## How to Use
Notebooks are organized by layer and numbered to indicate execution order.


#Notes
<a id="note1"></a>1. Harris County has a population of 5 million, the target percentile has a quarter of that population and the average household in the county is 2.5, hence we have 5,000,000/(4*2.5) = 500,000
