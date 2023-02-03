# Revene_Analysis
## Overview:
This project works with revenue analysis, where CPA and CPC are calculated for revenue analysis. Whereas in CPA and CPC are taken from the appcast data and jobs posted data from the database.

## Revenue Folder:
The Revenue folder contains the appcast data for particular dates, Those multiple csv files are merged into a single csv file where it is assigned to the appcast_df data frame.

## Appcast_Companies:
Appcast_companies.csv is a file decrypted from file.crypt(It’s a encrypted file of appcast_companies.csv) where it contains the company name - appcast (company name in appcast data), company name- mongo db (company name in mongoDB), employer id, uri (mongo db connection uri), domain.

## Extraction of DB Data:
All_companies_df is a dataframe of the data extracted from the MONGO DB from the respective uri,domains,employer id, company from the appcast_companies.csv  data.

## Here are the few steps for pre-extraction of Data from MONGO:
1.Taking the individual domains and mapping them to the suitable databases by all_companies_df dataframe where we will get all the DB credentials.
2.For the filter parameters, we extracted the company and employer id from the same dataframe.
3.For the data range, we have to flow a few steps:
  a)Convert the date_time column from the appcast_df data frame in “Year-Month-Date Hours:Minutes” in date column
  b)Extract the minimum and maximum date from the appcast_df data frame.
  c)Convert the min and max dates to IST by adding the 5 Hours to the date column.
  d)To return better results in MongoDB change the min_time by reducing 4 hours from the actual time and assign to min_correct_date for max_time increase it to 4 hours above the actual time and assign it to min_correct_date
4.Assign the “isFromGoogle” column as “True” and the “isBot” column as “False”.
