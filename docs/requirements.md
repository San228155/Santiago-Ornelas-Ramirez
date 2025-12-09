<details>
  <summary>Data Requirements</summary>
  - Property information: ZIP File recovered from https://hcad.org/pdata/pdata-property-downloads.html
  - Documents inside ZIP
      real_acct.txt
      - Schema (column_name, data_type, english_name, key)
        - 'acct', (string), account number, primary key
        - 'site_addr_1', (string), street address
        - 'site_addr_2', (string), city
        - 'site_addr_3', (string), zip code
        - 'state_class', (string), zoning
        - 'bld_ar', (string), building area
        - 'land_ar', (string), land area
        - 'tot_mkt_val', (string), total market value
        - 'yr', (string), year of information (gives no indication if consulted during current year, leading to incomplete information at the end of the year)
    - owners.txt
      - Schema
        - 'acct', (string), account_number, primary key
        - 'ln_num', (string), [insert info]
        - 'name', (string), name of owner (can be a person or company)
        - 'aka', (string), [insert_info]
        - 'pct_own', (string), percentage of ownership of property by an owner
       
  -> File size
    - Zip size ~204 MB
    - real_acct.txt size ~135 mb
    - owners.txt size ~22 mb
  
  -> update frequency
    - monthly

  -> Time identifier
    - Inside real_acct.txt column 'yr' identifies the year of the table(s)
       
- ZIP CODES AND CITIES IN HARRIS COUNTY: web site scrapped from https://www.zip-codes.com/county/tx-harris.asp#zipcodes
  - website with table Harris County, TX Covers 240 ZIP Codes
    -  Schema
      - ZIP Code, (string), zip code of property, primary key
      - Classification, (string), type of zip code
      - City, (string), city where property is locaed, primary key
      - Population, (string), amount of people registered to zip code
      - % of Population, (string), percentage of population in country living in zip code
</details>

<details>
  <summary>Pipeline Functional Requirements</summary>
  - Extract ZIP files automatically when they appear
  - Rename files
    - property_records_h_c
    - owners_records_h_c
  - Assign files to a directory structure by year
  - Validate data quality before transformation
  - Medalion transformation
  - Alert on validation failures
  - Automation
  - Reproducability and idempotancy
  - Manual reprocessing of past years
</details>

<details>
  <summary>Non-Functional Requirements</summary>
  - Reliability: Pipeline must run monthly with <1% failure rate.
  - Observability: Must log errors, decisions, file counts
  - Scalability: No singificant increase expected
  - Performance: End-to-end processing must finish under 30 minutes
  - Cost: Free-tier Databricks + low-cost Azure storage
  - Maintainability: CI/CD must enforce formatting, linting, and unit testing
</details>

