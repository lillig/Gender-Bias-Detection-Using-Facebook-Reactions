# Software for Gender Bias Detection Using Facebook Reactions
### Author: Lillian Gray

## Dependencies
This project relies on the facebook crawler published by Rugantio Costa located at https://github.com/rugantio/fbcrawl. 

This project also relies on multiple python libraries, which can be installed using:
`pip3 install <library> --user`

The libraries are:
* argparse
* os
* psycopg2
* scipy

## Project Layout
This project is divided into two main folders, which contain scripts run on separate machines. The first folder, `crawline_machine`, is where the crawler scripts are. They are intended to run within the downloaded fbcrawl repository. The second folder, `storage_machine`, is where the scripts to convert the crawler output, make database tables, and generate results are located.

### crawling_machine
The majority of the code depends on fbcrawl, outlined in the dependencies above. The files owned by me are outlined below.

* `candidate_data.csv`: A csv file containing page data for each politician. Copied to the storage machine.
* `csv_data`: A folder containing all the csv data generated by the crawler. Copied to the storage machine.
* `collect_data.py` A python script to run the crawler for each valid row in `candidate_data.csv`

### storage_machine
The files that were run on the cluster are outlined below. Make sure to edit directory variables in .sh files before attempting to run.

* `pageData`: Contains candidate_data.csv copied from the crawling machine. Also contains converted version copied into database.
* `postData`: Contains all the csv data generated by the crawler copied from the crawling machine. Also contains converted versions copied into database.
* `calcEntropy.py`: Calculates the entropy for all posts in the posts table, and updates the database with those calculations.
* `convertCSVFiles.sh`: Converts all csv files to be copied into the database
* `convertPageFile.py`: Python script to convert `candidate_data.csv` for copying into the database
* `convertPostFile.py`: Python script to convert a file generated by the crawler for copying into the database
* `generateResultsByPage.sh`: Generates tables of the average entropy values for each page
* `generateResults.sh`: Generates average results over all collected posts overall and by gender
* `makePagesTable.sh`: Creates pages table in database
* `makePostsTable.sh`: Creates posts table in database
* `runCSVConversionAndTableCreation.sh`: Runs scripts to convert all files and create database tables. Also generates output in .txt files for each script.
* `runResults.sh`: Runs scripts to generate results from database. Also generates output in .txt files for each script.