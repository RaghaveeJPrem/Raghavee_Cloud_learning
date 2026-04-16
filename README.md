# ADVENTURE WORKS DATA ENGINEERING PROJECT

**Project Summary**
This project implements an end-to-end data processing and analytics solution using Azure services.

**Data Ingestion:**
Data is collected from external sources (like HTTP APIs) using Azure Data Factory. This service orchestrates and automates data movement. In this case, data has been sourced from my Github account.

**Raw Data Storage (Bronze Layer):**
The ingested data is stored in its original form in Azure Data Lake Storage Gen2, ensuring scalability and cost efficiency.
    1.  A dynamic pipeline was created  in Azure Data Factory which uses Lookup, For each with Copy data to copy all the required files from Git to Bronze storage container.
    2.  Two Linked services were created one to connect to the Git URL and the other one to connect to ADLS Gen 2.
    3. A json file with all the list of the folders and files in Git was created and read via the Loop activity andf the output of the activity is fed to the foreach to perform the copy activity for each and every folder. The result is stored in Bronze.

**Data Transformation (Silver Layer):**
Azure Databricks processes and transforms raw data into a cleaner, structured format. This step includes data cleansing, enrichment, and business logic application.
  1. Initial Credential setup was done using Service Principle
  2. The required datasets (Calendar,Customer,Sales, Products, Product SubCategories etc) were read using Pyspark
  3. Transformations were done for the required data.
         a. Month an dYear was extracted from Calendar data
         b. Concatenation of First and Last name was done for Customer data
         c. Few of the column values were spilt for readbility in Products data
         d. Few Calculations anad converstions were made in Sales data. Sales analysis was done by calculating Total sales per order.
     
**Transformed Data Storage:**
The processed data is stored again in Data Lake Gen2 in Silver layer, now optimized for analytics and querying.

**Data Serving (Gold Layer):**
The curated data is loaded into Azure Synapse Analytics for high-performance querying and serving to downstream applications.
  1. Views and External tables were created in Azure synapse analytics and stored in Serverless SQL pool in Azure synapse studio
  2. Creation of DB schema, views, external tables and understanding the concepts such as using managed identity,creating credentials, creating external data source, creating external file formats were handled in this stage.
  3. 
**Reporting & Visualization:**
Finally, Microsoft Power BI connects to Synapse to create dashboards and reports for business users.


<img width="1536" height="1024" alt="End to End flow" src="https://github.com/user-attachments/assets/969d7603-a5a6-49c3-be2d-8b3e24e92381" />
