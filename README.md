# Carnot-Satellite-Intelligence-Assignment
Below is my step-by-step process for this assignment.
---------------------------------------------------------------------------------------------------------------------

## Project Overview
This solution was implemented in Databricks using PySpark following a medallion architecture approach
I used a simple layered approach:
- Bronze: load raw CSV files
- Silver: clean and prepare the data
- Gold: create the final analysis output

The goal was to keep the pipeline clear, easy to follow, and close to how a real data pipeline would be structured.

--------------------------------------------------------------------------------------------------------------------
#This Repo Files Included
      3 Notebooks 
- 01_bronze_ingestion.py → load raw source files
- 02_silver_transformation.py → data cleaning and joining
- 03_gold_analysis.py → analysis logic

    2 Output Files
- cleaned_parcel_timeseries.csv → final cleaned dataset
- analysis_output.csv → final analysis result
- -------------------------------------------------------------------------------------------------------------------



## Data Quality Audit
|Issue|Count|Percentage|Decision|Reason|
|---|---|---|---|---|
|Mixed date formats|0|0|Repair|Needed for correct date analysis|
|Invalid NDVI values|104|3|Remove|NDVI should be between -1 and 1|
|Duplicate parcel-date records|8|0.2|Remove|One parcel should have one reading per day|
|Bad sensor status|340|9.9|Flag|Bad sensor data not used in analysis|
|Orphan parcel IDs|2|0.1|Remove|No matching metadata found|
|Invalid area values|0|0|Remove|Area should be greater than 0|


---------------------------------------------------------------





