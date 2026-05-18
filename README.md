# Carnot-Satellite-Intelligence-Assignment
Below is my step-by-step process for this assignment.
---------------------------------------------------------------------------------------------------------------------

# Project Overview
This solution was implemented in Databricks using PySpark following a medallion architecture approach
I used a simple layered approach:
- Bronze: load raw CSV files
- Silver: clean and prepare the data
- Gold: create the final analysis output

The goal was to keep the pipeline clear, easy to follow, and close to how a real data pipeline would be structured.

--------------------------------------------------------------------------------------------------------------------



# This Repo Files Included
 3 Notebooks
- 01 Bronze.ipynb → load raw source files
- 02 Silver.ipynb → data cleaning and joining
- 03 Gold.ipynb → analysis logic

    2 Output Files
- cleaned_parcel_timeseries_csv.csv → final cleaned dataset
- Final_crop_ndvi_analysis_csv.csv → final analysis result
- -------------------------------------------------------------------------------------------------------------------



# Data Quality Audit
|Issue|Count|Percentage|Decision|Reason|
|---|---|---|---|---|
|Mixed date formats|0|0|Repair|Needed for correct date analysis|
|Invalid ndvi values|104|3|Remove|ndvi should be between -1 and 1|
|Duplicate parcel-date records|8|0.2|Remove|One parcel should have one reading per day|
|Bad sensor status|340|9.9|Flag|Bad sensor data not used in analysis|
|Orphan parcel IDs|2|0.1|Remove|No matching metadata found|
|Invalid area values|0|0|Remove|Area should be greater than 0|


--------------------------------------------------------------------------------------------------
# Cleaning Steps
- Fixed mixed date formats in parcel readings
- Converted sowing date into standard date format
- Standardized sensor status values 
- Removed invalid ndvi values
- Removed duplicate parcel/day records
- Removed invalid metadata rows
- Joined readings and metadata ON parcel_id

So, created one clean time-series dataset with one row per parcel per date


--------------------------------------------------------------------------------

# Analysis Output

The analysis compares ndvi values before and after sowing for each crop type.
 So,Here i take data based on below condition
- only good sensor data was used
- 30 days before sowing
- 30 days after sowing

Output columns is
- crop_type
- mean_ndvi_before
- mean_ndvi_after
- n_parcels

|crop_type|mean_ndvi_before|mean_ndvi_after|n_parcels|
|---|---|---|---|
|sugarcane|0.177|0.336|19|
|soybean|0.171|0.313|4|
|wheat|0.176|0.31|2|


# Quick Observation**

For all crop types, ndvi is higher after sowing than before sowing. This is expected because crops start growing after planting.
Sugarcane has the most data (19%), so this result looks more reliable.
Soybean 4%  and wheat 2% have fewer %, so their numbers may change if more data is available.


----------------------------------------------------------------------------------------------------------

# Production-readiness reflection

If this pipeline runs daily with much larger data

 - Use incremental loading instead of full reload
 - Add automatic data quality checks
 - Schedule the pipeline instead of running manually



---------------------------------------------------------------------------
# Most Likely Silent Issue

If the source date format changes unexpectedly, date parsing may fail and some records may be skipped.

-------------------------------------------------------------------------------------------

# Monitoring
Basic and important things nneed to Monitor 
- record count changes
- invalid date records
- bad sensor records
- duplicate records
- missing values
- pipeline failures

------------------------------------------------------

#Loom Walkthrough

Loom link -  




