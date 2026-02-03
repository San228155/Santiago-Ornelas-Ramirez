# Housing Market Stability Analysis Pipeline in Harris County from 2017 to 2025

## Client Background
Harris County has asked us to explore the stability of the Housing Market in Harris County from 2017 to 2025, specifically for the population between the 25th and 50th percentile of earners. Harris County wants to ensure that this population has adequeate access to housing and that market conditions remain stable enough to prevent ongoing affordability challenges.

Harris County has determined they need 500 thousand houses for this population<sup><a href="#note1">1</a></sup>. The County has determined that an affordable house is 4 times the yearly salary of a household. We look only at houses registerd to be single family residentials ("a1" category<sup><a href="#note2">2</a></sup>) or mobile homes ("a2" category), we do not count multi-family residentials ("b1") for this analysis

We provide an pipeline from Harris County's Property data <sup><a href="#note2">3</a></sup> using the medallion architecture. We emphasize providing reliable pipelines with clean data and visibility througt. The key insight and recommendations focus on teh follwoing areas.
### Target Metrics
- Supply of Houses vs Demand of Houses - Amount of availabe houses vs amount houses needed in **2025** for the target population
- Stability of the Market — We assess the stability category of the median home based on how long it has been since its most recent affordability‑bracket change. Stability categories are defined by whether properties have remained in the same 2025 affordability bracket over the past eight years, four years, and two years (counting backward from 2025), as well as by the number of properties that have shifted to a different bracket within the last two years.
- Number of times a property classified as affordable, for the target population, in 2025 has shifted to a different affordability bracket over the past eight years.


## Summary
### Executive summary
Metrics:
The 2025 analysis of the Harris County housing market indicates that housing supply is sufficient and pricing dynamics are stable for households in the second income quartile.

Housing availability exceeds expectations, with over 600,000 homes meeting eligibility criteria against a target of 500,000, signaling adequate inventory to support current population needs.

Price stability metrics further support this assessment. Homes in the second income quartile exhibit moderate price consistency, with a median of 4–8 years since the last bracket change. While the first quartile remains the most stable segment, the second quartile demonstrates meaningfully greater stability than higher-income segments, where prices shift more frequently.

Overall market volatility is limited, as the median number of bracket changes per home is one, indicating that most properties experience minimal reclassification over time.

Conclusion:
The Harris County housing market for second-quartile earners in 2025 is stable and well-supplied. Although not the most static segment of the market, it offers availability and price predictability, positioning suitable housing options for this income group.

## How to Use
This project implements an end-to-end Databricks pipeline that processes Harris County property data using a medallion architecture (Bronze, Silver, Gold). Pipeline execution is orchestrated via Databricks Jobs, with notebooks executed in a predefined order.

Detailed schemas, metrics, and pipeline flow diagrams are documented in the Design Specification, which serves as the authoritative reference for this project.


### Input Data Requirements

Raw source data is recuperated from two sources, the Harris County Property Data Website <sup><a href="#note2">3</a></sup> and from https://www.zip-codes.com/county/tx-harris.asp

Raw source data from the Harris County Property Data Website is expected to be delivered as uncompressed files (.txt files) to the configured landing location (this is the natural format from the Harris County Property Data Website)

Raw source data from www.zip-codes.com is recovered automatically through web scrapping

Raw files are treated as immutable inputs and are first registered in the Bronze layer

Note: Raw data files are not included in this repository. The Bronze layer defines the ingestion contract for all source data

### Notebook Structure & Execution

Notebooks are organized by medallion layer and numbered to indicate execution order:

Folder name represents the pipeline layer (Bronze / Silver / Gold)

Each notebook is designed to be rerunnable and idempotent

Execution can be triggered either manually (for development) or via Databricks Jobs (for production runs)

The Repo must have this strucutre for the job to run
/Repo
  /h_c_notebooks
    /bronze
      owners_bronze
      property_bronze
      zip_codes_bronze
    /silver
      owners_silver
      property_silver
      zip_codes_silver
      joined_silver
    /gold
      Gold_layer
      scd_gold
    /logging
      log_notebook
    init_schema

### How to run this project

1. In Databricks, go to Repos → Add Repo → paste this GitHub URL.
2. Open Jobs → Create Job → Import → select jobs.json (found in jobs folder in this repo)
3. The job will automatically reference the notebooks inside the repo

This file uses a for_each_task for loop with parameters [2017,2018,...,2025]. These parameters are already included inside the jobs.json file

### Output & Data Contracts

Final, analytics-ready tables are published in the Gold layer

Table structures, relationships, and metrics are defined in the Design Specification

Downstream consumers should rely on Gold tables only

The intended customer are Data Analysts as the final product are tables with simple data structures, ideal to use for further visualization

All required table creation is managed internally as to allow visibility of the data throught the project

### Monitoring & Troubleshooting

Execution status and logs are available in Databricks Job Runs

Failed tasks prevent downstream execution

Individual notebooks may be rerun independently if remediation is required

All runs are logged in three different ways
- Pipeline runs - Logs the execution of all notebooks, independently, most importantly noting if the execution was succesful or not, in which case also noting the error
- Data quality runs- Logs the execution of unit tests for a notebook, independently, noting if the test was successful or not, including the error. This registers the most important data quality checks and will shut down the notebook and pipeline if it finds any
- Metrics - Logs metrics accumulated thorught the process of the pipeline. This does not shut down a notebook or pipeline and all metric descriptions are given in the design spec.

## Technology
- Databricks
- Pyspark
- Sql
- Beautiful Soup

#Notes

<a id="note1"></a>1. Harris County has a population of 5 million, the target percentile has a quarter of that population and the average household in the county is 2.5, hence we have 5,000,000/(4*2.5) = 500,000  
<a href="#note2"></a>2. a1 or a2 is the naming convention given in directly from the property information from Harris County
<a href="#note2"></a>3. https://hcad.org/pdata/pdata-property-downloads.html
