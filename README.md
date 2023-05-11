# Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics
Project Introduction
The City of New York would like to develop a Data Analytics platform on Azure Synapse Analytics to accomplish two primary objectives:

Analyze how the City's financial resources are allocated and how much of the City's budget is being devoted to overtime.
Make the data available to the interested public to show how the City’s budget is being spent on salary and overtime pay for all municipal employees.
As a Data Engineer, I have to create high-quality data pipelines that are dynamic, can be automated, and monitored for efficient operation. The project team also includes the city’s quality assurance experts who will test the pipelines to find any errors and improve overall data quality.

The source data resides in Azure Data Lake and needs to be processed in a NYC data warehouse in Azure Synapse Analytics. The source datasets consist of CSV files with Employee master data and monthly payroll data entered by various City agencies.


**For this project, we will do our work in the Azure Portal, using several Azure resources including:**

Azure Data Lake Gen2
Azure SQL DB
Azure Data Factory
Azure Synapse Analytics
Step 1: Prepare the Data Infrastructure
Setup Data and Resources in Azure

1.Create the data lake and upload data
Create an Azure Data Lake Storage Gen2 (storage account) with three directories in this storage container named

dirpayrollfiles

dirhistoryfiles

dirstaging

<img width="960" alt="storage_contianers" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/5b7c9f81-8249-4331-8f98-a0ee8c375350">

**Upload data from the project data to the dirpayrollfiles folderp**

<img width="960" alt="csv_files" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/4faf3a2d-5858-4172-a412-254cbbd69b4e">

**Upload `nycpayroll_2020.csv` file (historical data) from the project data to the dirhistoryfiles folder**

<img width="960" alt="csv_file_payroll_2020" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/40a9744f-f949-47e8-9bde-feef012d9b0a">

## 2- Create an Azure Data Factory Resource,SQL Database to store the current year of the payroll data, A Synapse Analytics workspace


<img width="960" alt="All_resources" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/36cff27b-6bd3-4825-8a0a-4a9b8326abca">

Create a table called NYC_Payroll_Data in db_nycpayroll in the Azure Query Editor with SQL Script:

<img width="960" alt="create_table_payrolll_data" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/42165f8c-db5f-43db-a1e6-5bd193c18ee2">


Create a SQL dedicated pool in the Synapse Analytics workspace

- Select DW100c as performance level.

<img width="960" alt="dedicatedDW100c" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/250cdb32-75ff-4953-965e-85208a7f3cc0">

In the SQL dedicated pool, Create master data tables and payroll transaction tables:

<img width="960" alt="create_master_tables" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/2bfa26db-c8de-4a91-9869-d118cde69a7f">

The table are successfully created in the SQL Database

<img width="535" alt="master_tables_successful " src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/29baf872-2bac-4e2e-a6e4-7c7f1dff2889">


# Step 2: Create Linked Services


<img width="960" alt="linked_services" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/613d367f-2452-4a68-8407-937a8ed66ca0">



# Step 3: Create Datasets in Azure Data Factory

## 1.Create the datasets for the 2021 Payroll file on Azure Data Lake Gen2

- Select DelimitedText
- Set the path to the `nycpayroll_2021.csv` in the Data Lake
- Preview the data to make sure it is correctly parsed

<img width="960" alt="preview_data" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/0a7b63ef-11e4-4894-bace-2391a69013d7">

<img width="960" alt="Create_datasets" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/8a03b6d5-4444-4a49-8ced-51acbc5fd1fe">


## 2. Repeat the same process to create datasets for the rest of the data files in the Data Lake
-EmpMaster.csv
-TitleMaster.csv
-AgencyMaster.csv
Remember to publish all the datasets

## 3- Create the dataset for transaction data table that should contain current (2021) data in SQL DB

<img width="960" alt="create_transaction_table" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/2fe94b70-f99c-4e59-bada-0c221e46cc9c">


# Step 4: Create Data Flows

## 1 .In Azure Data Factory, create the data flow to load 2021 Payroll Data to SQL DB transaction table (in the future NYC will load all the transaction data into this table).

- Create a new data flow

- Select the dataset for the 2021 payroll file as the source


<img width="960" alt="dataflow_2021" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/727a9906-cbab-4c70-a031-8cc3b6d1a766">

**Monitor the pipeline**

<img width="960" alt="Mointor_dataflow" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/beebe342-18e2-46be-b330-de35bffbd76c">

**Take a screenshot of the Azure Data Factory screen pipeline run after it has finished.**

<img width="960" alt="ADF_pipeline" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/c4682c7e-d565-4f78-b28e-7f2a53f48340">

**Make sure the data is successfully loaded into the SQL DB table**

<img width="935" alt="loaded_to_sql" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/aae9699a-3cef-4dc0-a655-8495e242e3f8">

## 3. Create data flows to load the data from the data lake files into the Synapse Analytics data tables
Create the data flows for loading Employee, Title, and Agency files into corresponding SQL pool tables on Synapse Analytics

For each Employee, Title, and Agency file data flow, sink the data into each target Synaspe table

<img width="960" alt="data flows for loadingm agency" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/8b2c8d9f-ff61-4593-9f60-72f0ff9e50a2">

<img width="960" alt="data flows for loading title" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/4e368d75-06d5-4bae-b6ab-a413d2eb85a3">

<img width="960" alt="data flows for loading Employee" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/f777bb87-866b-4515-bf4e-5638b001c8a7">


## 4. Create a data flow to load 2021 data from SQL DB to Synapse Analytics


![sql_synapse](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/867e1252-3cb6-40cb-ad0e-d0f3c28b6d88)

![sql_synapse2](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/dea3badd-4f88-4b5d-9f21-e56473a5f2eb)



## 5. Create pipelines for Employee, Title, Agency, and year 2021 Payroll transaction data to Synapse Analytics containing the data flows.

-Select the dirstaging folder in the data lake storage for staging

-Optionally you can also create one master pipeline to invoke all the Data Flows

-Validate and publish the pipelines

**Employee, title, Agence, and Year 2021**

![pipeline_emp](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/e80e1573-d471-457d-803b-adbc41181806)

![pipeline_title](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/58302119-109a-4c56-980d-f178ea0966bb)

![pipeline_year2021](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/41fcc90f-b71b-4001-8e6c-f3248cf11125)

![pipeline_agency](https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/132cd5b3-31c2-42ca-8d31-262a49b03c88)



**Load all to synapse**

<img width="960" alt="Load_all_to_synapse" src="https://github.com/A-Janad/Data-Integration-Pipelines-for-NYC-Payroll-Data-Analytics/assets/126161000/cf03550c-970d-4fbd-b9b4-32ef7caf0d8e">

