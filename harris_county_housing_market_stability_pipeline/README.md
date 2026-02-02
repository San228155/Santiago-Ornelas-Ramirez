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
- There are enough available houses for this population for the year 2025. We wanted at least 500 thousand houses and there are over 600 thousand available homes in this bracket.
- The 2nd quartile of earnes have a very stable market (having the median house having between 4 and 8 years since its last bracket change). Although this is not the most stable (1st quartile has the medain house have more than 8 years change), but it is more stable than the 4th quartile (whose median house has between 2 and 4 years sincce last bracket change).
- We see that the median bracket changes per house is 1, where only houses in the 1st bracket has a different median with 0.

We determine that the Housing Market in Harris County for 2nd quartile, in earnings, in is stable. 

## How to Use
This project is built on data bricks. It uses job orchestration from the job runs tab in databricks using notebooks to execute all parts of the medallion architecture. 


## Technology
- Databricks
- Pyspark
- Sql

#Notes

<a id="note1"></a>1. Harris County has a population of 5 million, the target percentile has a quarter of that population and the average household in the county is 2.5, hence we have 5,000,000/(4*2.5) = 500,000  
<a href="#note2"></a>2. a1 or a2 is the naming convention given in directly from the property information from Harris County
<a href="#note2"></a>3. https://hcad.org/pdata/pdata-property-downloads.html
