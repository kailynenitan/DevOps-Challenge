# NBADataLake
This repository contains the setup_nhl_data_lake.py script, which automates the creation of a data lake for NHL analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena, and sets up the infrastructure needed to store and query NBA-related data.
This project was made in order to complete [Day 3 of the DevOpsAllStarsChallenge.](https://www.youtube.com/watch?v=RAkMac2QgjM)
The code that this project is built from was made by Alicia Ahl at her [NBADataLake](https://github.com/alahl1/NBADataLake.git) repository.

# Overview
The setup_nhl_data_lake.py script performs the following actions:
- Creates an Amazon S3 bucket to store raw and processed data.
- Uploads sample NHL data (JSON format) to the S3 bucket.
- Creates an AWS Glue database and an external table for querying the data.
- Configures Amazon Athena for querying data stored in the S3 bucket.

# Project File Structure
```
NHLDataLake/
|-- src/
|   |-- .env
|   |-- setup_nhl_data_lake.py
|-- policies/
|   |-- IAM_Role
|-- delete_aws_resources
|-- README.md
```

# Prerequisites
Before running the script, ensure you have the following:

Go to Sportsdata.io and create a free account

At the top left, you should see "Developers", if you hover over it you should see "API Resources"
Click on "Introduction & Testing"

Click on "SportsDataIO API Free Trial" and fill out the information & be sure to select NBA for this tutorial

You will get an email and at the bottom it says "Launch Developer Portal"

By default it takes you to the NFL, on the left click on NHL

Scroll down until you see "Standings"

You'll "Query String Parameters", the value in the drop down box is your API key. 

Copy this string because you will need to paste it later in the script

IAM Role/Permissions: Ensure the user or role running the script has the following permissions:

S3: s3:CreateBucket, s3:PutObject, s3:DeleteBucket, s3:ListBucket
Glue: glue:CreateDatabase, glue:CreateTable, glue:DeleteDatabase, glue:DeleteTable
Athena: athena:StartQueryExecution, athena:GetQueryResults

# Configuration
### Configuring Environment Variables
1. Within src/ create a .env file using the touch command
```
touch .env
```
2. Within the .env file, create a SPORTS_DATA_API_KEY and NHL_ENDPOINT
```
SPORTS_DATA_API_KEY=your api key here
NHL_ENDPOINT=https://api.sportsdata.io/v3/nhl/scores/json/Players
```

# Running the Scripts
### Creating the Data Lake
```
python3 setup_nhl_data_lake.py
```
This command creates all of the resources required for the data lake. This command must be run in src/.
You should see the resources were successfully created, the sample data was uploaded successfully and the Data Lake Setup Completed.

### Deleting the Data Lake
```
python3 delete_aws_resources
```
Run this command in the parent directory. 
This command deletes all of the resources that were created in order to make the data lake.

# Manually Checking Resources
1. In the Search Bar, type S3 and click blue hyper link name

- You should see 2 General purpose bucket named "Sports-analytics-data-lake"
- When you click the bucket name you will see 3 objects are in the bucket

2. Click on raw-data and you will see it contains "nhl_player_data.json"

3. Click the file name and at the top you will see the option to Open the file

- You'll see a long string of various NHL data

4. Head over to Amazon Athena and paste the following sample query into the editor:
```
SELECT FirstName, LastName, Position, Team
FROM nhl_players
WHERE Position = 'LW';
```
Ensure that the database drop down menu on the left sidebar says "glue_nhl_data_lake"
- Click Run
- You should see an output if you scroll down under "Query Results