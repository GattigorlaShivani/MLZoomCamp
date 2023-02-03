# Revene_Analysis
## Overview:
This project works with revenue analysis, where CPA and CPC are calculated for revenue analysis. Whereas in CPA and CPC are taken from the appcast data and jobs posted data from the database.

## Revenue Folder:
The Revenue folder contains the appcast data for particular dates, Those multiple CSV files are merged into a single CSV  file where it is assigned to the appcast_df data frame.

## Appcast_Companies:
Appcast_companies.csv is a file decrypted from file.crypt(It’s a encrypted file of appcast_companies.csv) where it contains the company name - appcast (company name in appcast data), company name- mongo db (company name in MongoDB), employer id, uri (mongo db connection uri), domain.

## Extraction of DB Data:
All_companies_df is a dataframe of the data extracted from the MONGO DB from the respective uri,domains,employer id, company from the appcast_companies.csv data.

## Here are the few steps for pre-extraction of Data from Mongo:
1.Taking the individual domains and mapping them to the suitable databases by all_companies_df dataframe where we will get all the DB credentials.

2.For the filter parameters, we extracted the company and employer id from the same dataframe.

3.For the data range, we have to flow a few steps:
* Convert the date_time column from the appcast_df data frame in “**Year-Month-Date Hours:Minutes**” in date column.
* Extract the minimum and maximum date from the appcast_df data frame.
* Convert the min and max dates to IST by adding the 5 Hours to the date column.
* To return better results in MongoDB change the min_time by reducing 4 hours from the actual time and assign to min_correct_date for max_time increase it to 4 hours above the actual time and assign it to min_correct_date.

4.Assign the “**isFromGoogle**” column as “**True**” and the “**isBot**” column as “**False**”.

## Appcast Data Modifications:
To create the primary key in the appcast_df data frame concat the date_time column and IP address in formate of “**ipaddress<>date_time**” and name the result column as primary_key.

## Database Data Modifications:
All_company_df is the data frame fetched from the MongoDB by the filters which are mentioned above.

## Here are the few steps for post-extraction of Data from MONGO:
1.To remove the duplicates from the all_company_df concat the column which contains the date in the format of “**Year-Month-Date**”, IP address, and jobpubjobid in the formate of “**date<>ipaddress<>jobpubjobid**” drop the rows with the same value of concat column.

2.Modify the IP address by replacing the HostID with 0 eg:127.168.0.1 → 127.168.0.0.

3.Convert the date to “**Year-Month-Date Hours: Minutes**” format and assign it to the converted_date column.

4.Convert the converted_date column from IST to EST Zone by reducing the 5 hours from actual time and assigning it to the final_time column.

## Mapping the Appcast Data and Database Data:
### 1.Extracting the Revenue of CPC (Cost Per Click):
Perform the merge operation for appcast_df and all_company_df  where both primary key got matched assign that to df_merge_cpc
### 2.Extracting the Revenue of CPA (Cost Per Apply):
Perform the merge operation for appcast_df and all_company_df  where both ipaddress got matched then assign that to df_merge_cpa

Concat the both df_merge_cpa and df_merge_cpc data frame and assign to df_merge where complete revenue is mapped with jobs posted.

## Extract the Top Titles by their Revenue:
Perform the groupby operation to revenue data (df_merge) by grouping job title with the price(revenue) and jobpubjobid. Where jobpubjobid count represents the jobs posted for the particular title and assigns that to the jobs_posted column and the unique_jobs_posted column represents the unique jobpubjobid count.

## Extract the Top Titles with locations by their Revenue:
Perform the groupby operation to revenue data (df_merge) by grouping job title and location(location_y is job posted location) with the price(revenue) and jobpubjobid. Where jobpubjobid count represents the jobs posted for the particular title and assigns that to the jobs_posted column and the unique_jobs_posted column represents the unique jobpubjobid count.

## Extract the Top Locations by their Revenue:
Perform the groupby operation to revenue data (df_merge) by grouping location (location_y is job posted location) with the price(revenue) and jobpubjobid. Where jobpubjobid count represents the jobs posted for the particular title and assigns that to the jobs_posted column and the unique_jobs_posted column represents the unique jobpubjobid count.
