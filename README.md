# Big Data Engineering Project on Azure

### Project Overview

This project is a Big Data Engineering initiative hosted on Azure. 

- Firstly, data will be **extracted** from two different sources and ingested into the Azure Data Lake. This extraction phase involves retrieving data from its source systems while ensuring its integrity and completeness.

- Following extraction, the data will undergo **transformation** to make it suitable for analysis and model training. This transformation step involves cleaning, filtering, aggregating, and enriching the data as necessary. Additionally, any necessary data wrangling or feature engineering required for the machine learning model will be performed during this phase.

- Once the data is transformed, it will be **loaded** back into the Azure Data Lake, where it will be stored alongside the raw data. This loading phase involves storing the processed data in a structured format that is optimized for querying and analysis.


![bd_diagram1](https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/8e0688f9-45bf-4010-84b4-48316a416acc)


### About Data

The dataset used in this project is sourced from StackOverflow, a popular online community for IT developers. The dataset includes daily posts, covering post types and user information.
The 3 tables are located in 2 data sources, RDS and Azure Storage Blob Container.
<img width="595" alt="Screenshot 1445-11-20 at 7 00 41 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/87be1e1f-f7e3-40e0-9429-2dd0830dc3f1">


### Part One: Data Ingestion ( **Exract** )

<img width="1018" alt="Screenshot 1445-11-20 at 7 02 10 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/d115099d-97fa-48e7-b647-99fd27624cb8">

### 1. Create azure data factory to ingest data from 2 data sources
- a postgres database on RDS,ingestion frequency(once a week)
- a public Azure storage container, Ingestion Frequency(Daily)

##### 1.1 create two pipelines 
<img width="308" alt="Screenshot 1445-11-20 at 7 38 17 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/e8559bba-b8a0-4045-83d7-b28344ffad4b">


##### 1.2 create 2 copy activities in the copyOnceWeek pipeline to copy both tables from the Postgres, and create 2 delete activities to empty the folder used to accept the posttypes and Users files every week.

- we need to create linked service to link to the RDS postgres database

- the first copy activity is for coping the user table, the source is RDS postgres database and the destination is our data lake

<img width="511" alt="Screenshot 1445-11-20 at 7 47 57 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/a42785f8-12a7-47e2-ad1c-8b7bcc11fda6">

<img width="513" alt="Screenshot 1445-11-20 at 7 48 21 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/1fd55bc9-b577-4de6-bbbc-28e3277d89fd">

- the second copy activity is for coping the post type table, the source is RDS postgres database and the destination is our data lake
<img width="513" alt="Screenshot 1445-11-20 at 7 52 13 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/d7c2c55e-57f7-4717-a854-e840820692fe">

<img width="518" alt="Screenshot 1445-11-20 at 7 52 35 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/c7d8f369-3b9f-45ac-8679-6ea1e6cab9b6">

##### 1.3 create 1 copy activities in the copyPostsEveryday pipeline to copy Posts parquet files from WCD's blob storage to our data lake, also we need to create a delete activity to empty the folder used to accept the Posts files everyday.
<img width="754" alt="Screenshot 1445-11-20 at 8 19 50 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/2a29e4e5-919c-4bc6-b88a-014fd8f6acdc">

<img width="734" alt="Screenshot 1445-11-20 at 8 20 14 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/0ef7e0d3-4e61-4edd-b3d1-c1bb3bddb3eb">

<img width="748" alt="Screenshot 1445-11-20 at 8 20 34 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/4d260eec-9182-4ee1-89a9-c22001af2213">


### 2. Create data lake on azure to store the ingested data files in the data lake.



### 3. Set schedule for both of the pipelines.
<img width="1512" alt="Screenshot 1445-11-20 at 8 25 11 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/62a5bbeb-4227-41e7-9242-041222bd4faa">

<img width="1512" alt="Screenshot 1445-11-20 at 8 25 42 PM" src="https://github.com/shaden-2000/SDA-Capstone2/assets/100734021/b8f75243-b2bb-4ecb-8fdd-bc9c0f2e9993">

