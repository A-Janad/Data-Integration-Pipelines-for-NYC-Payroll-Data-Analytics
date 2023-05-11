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






