# Get Data Into Celonis
url: https://academy.celonis.com/learn/learning-path/get-data-into-the-ems-1
access: https://fox57xlh-2026-02-04.training.celonis.cloud

flat: JMLEUQCTIZZRCBWXANRM
flat: HOPGUESJZWOGBEDVYSKOLDSBHITWHMYWIVSZZZKI
nested: AGXDBNMYCZGXUCQLCABA  
nested: XFHELQGBVZRDAECTMZUAFEHEXMSWNRBCSZEQEVCI

REST id: 9b38a250-525b-42d6-95aa-a68ce848ad14
REST secret: fd64skZtraiM0BzPHuVHfx5gIHwEB88wI308xKRgKsu2ItejG7mXaDAhthkpYItv

## Data Integration Basics
- Process Data is a set of connected activities with timestamps following one specific case = tracking steps 
- Data Model connects
  - one or more activity tables
  - case tables
  - and master data tables

### Data Integration Methods
- **C** connect to source systems
- **E** extract the relevant data
- **T** transform it to your needs
- **L** load 

### Process Connectors = prebuilt data integrations
- Process Connectors contain templates and scripts that support you in the connect, extract, transform, load, and scheduling steps of building your data pipeline

### Real-Time
- frequently replicate **incremental** changes in data from source systems 
- **non-real-time** data pipelines are typically mostly based on **scheduled full loads**
- real-time data integration only for E and T step not for Data Model Load. L relies always on a scheduled jobs

### Advantages of real-time
- Extract
  - Faster performance
  - Smaller burden on source systems as changes are tracked and extracted using native capabilities of source systems.
  - Close to no need for full extractions except at the very start of your integration.
- Transform
  - Faster performance of transformations
  - Highly reduced need for full table transformations

### Data Model
- Data Model connects
  - one or more activity tables
  - case tables
  - and master data tables

- Operational Data Model
  - Celonis recommends creating smaller, operational Data Models
  - **restricted data scope** examining only the most recent, prevalent cases
  - Model is smaller, loads faster and is the one business users use in day-to-day business

- Analytical Data Model
  - analysts can drill down into processes, look for patterns, filter and so on. 
  - do not necessarily require real-time data.
  - regular complete loads of the data

## Connect to Systems
### Main Connection Methods
- Process Connectors (from the market place) **most common method**
- Extractors (Data Connections)
- Extractor Builder
- File Uploads
- Data Ingestion API
- Celoxtractor


### Extractors 
- blank data connections with no reference to a process
- connect to source systems and then have to build your data pipeline from scratch
- for on-prem you need an uplink client (on-prem connector)
- Only **read-only** operations on data
- Categories:
  - On Prem
  - Cloud
  - Custom 
  
### Extractor Builder
- find it under "Create custom REST API extractor" when connecting new data sources
- specific to your data pool, but you can export it. But connection details are not included in the export
- Setup an extractor with the extractor builder
  1. Variable: e.g. API URL
  2. Authentication: e.g. OAuth2, Baisc AUth
  3. Data Connection
  4. Add Endpoint: e.g. /users
     -  req params
     -  header
     -  pagination
     -  response configuration
     -  response rules: e.g. skip 500 status
  
 More to come in this course: https://academy.celonis.com/learn/course/extractor-builder-basics-q6vs/extractor-builder-basics/basics?client=partner

### File Upload
- 1GB max size
- multiple files can be uploaded at once in one table, but they need to have the same structure


### Data Ingestion API
- push data into Celonis from Kafka or other tools
- need basic programming skills to use it

- Data Ingestion API Spec
  - One API call per table: Every table you create or update requires one API call.
  - Built on S3 API: It's built on top of the S3 API with the same methods and error codes. It uses primarily this S3 PUT object endpoint.
  - Continuous load: The load is continuous. So as soon as you ping the API, your data is loaded into Celonis. It operates on a First In First Out (FIFO) principle.
  - Auto-delta load: All pushed records are loaded as delta records automatically and compared to existing records. 
  - Nested data possible: The API can handle nested (json) data out-of-the-box and unnest it into tables and columns.
  - UI schema configuration: It supports a UI based configuration for table schema, i.e. table names, keys, age columns.
  - Parquet files only: As of today, the API only supports parquet files and requires you to convert to parquet before pushes.


### Celoxtractor
- The Celoxtractor is a Python package designed to let you develop your own Celonis Extractor easily.
  - complete control over your data,
  - feature parity to native Celonis extractors,
  - and full flexibility in adjusting all aspects of your extractions.


#### Connection and Extraction
- Closed Hosting Environments
  1. Extractor establishes connection to Data Integration.
  2. Data Engineer defines which tables to extract in Data Integration.
  3. Extractor informs source system of what data to extract.
  4. Data extraction is performed.
  5. The extracted data is sent to the Extractor Server.
  6. The Extractor Server transforms the files into parquet files.
  7. The Extractor Server sends the transformed to the Celonis data Storage.

- Open Hosting Environments
  1. Extractor establishes connection to the Cloud system and requests data.
  2. Data Engineer defines which tables to extract in Data Integration.
  3. Cloud system extracts data and sends it to the Cloud Extractor.
  4. Cloud Extractor transforms the files into parquet files.
  5. Cloud Extractor sends the transformed files to the Celonis Data Storage.

### Real-Time Connections/Extarctions 
  1. Create Change Log tables to store changes
  2. Install Triggers to monitor and capture changes
  3. Activate a cleanup background job to clean up the Log tables (SAP-specific)
![trigger-realtime](05-trigger-realtime.png)


### Data Pools Introduction
https://academy.celonis.com/learn/course/connect/structure-your-data-pools/structure-data-to-your-needs?client=partner&page=2
####  Analogy
- Data Pool = Database
  - Data Connection = Schema
    - Data Job = Stored Procedure
      - Extraction
      - Transformation
      - Load Data Model
- Data Model = Star Schema  
![data-pool-strcuture](05-data-pool-strcuture.png)

- DATA POOLS	Host one or more Data Connections
- DATA CONNECTIONS	Contain one or more Data Jobs
- DATA JOBS	Contain "tasks" for extraction, transformation, and Data Model load
- DATA MODELS	Pull data from all connections in one Data Pool

#### Best practices for Data Pools
- keep all **related** processes and systems within one Data Pool
- In some cases, it also makes sense to create separate Data Pools for different regional or legal entities to restrict access to the data for certain users or user groups.

## Extract Data
### Extractions can be done by
- Data Jobs
- or Replication Cockpit

Questions to ask on picking the tool
- Is the Process Connector / Extractor real-time?
- Is the data needed for operational use cases (day-to-day actions)?
  
### Data Jobs
- schedule-based 
- full and delta extractions
- used for analytical Data Model
- if there is no rush to always have the freshest data, then data jobs are sufficient.
- extractions make use of filters (not change logs)

### Task Parameters
- private/public
  - A private parameter is only visible and editable for admins of the data pool, whereas a public parameter is visible to everyone who can access the task. Both are static, which means that their value doesn’t change until you enter a new one.
- Dynamic
  - generated from existing data and only visible for admins
- Data Pool parameters: As opposed to Task Parameters, you can use Data Pool parameters across an entire Data Pool.

### Table types in SAP
### Data Jobs
- core tables: essential information
- change tables
- name mapping tables

### Replication Cockpit
- real-time based
- full and delta extractions
- used for operational use cases
- extractions with Replication Cockpit make use of change logs

### Delta Extraction
- new, and updated table rows.
- difference between Full Loads and Delta Loads is that the two filters: "Delta Filter" and the "Enable change date Time filter" are considered.

#### Using Change Date
- table contains a “Change Date" column.
- Celonis automatically identifies duplicates based on the primary key and inserts the new rows, overwriting the old existing rows 
- Alternative: using a dynamic parameter and adding it to the Delta Filter:

#### Using Consecutive Numbers
- using a dynamic parameter FIND_MAX of CHANGENR

#### Using the Creation Date
- if no Change Date available use Creation Date + offset
- so most of the changes will be extracted

### Metadata changes
- To avoid delta load failures after metadata changes, you can activate the “include metadata changes” (added or removed columns in source system tables)
- if the extraction does not include all columns of a table, metadata additions will not be extracted even if the option is selected.
- When should you activate this option?
  - NULL values: Activating the option to include metadata changes may result in NULL values in your data. Let's imagine adding a new column to the table EKPO. This column provides information for each purchase order item, specifically if the item will be used internally or for an end product. However, this information will only be filled after the new column is added and will not be backfilled for past purchases. This may result in an inconsistency in the source system and will be reflected in the extracted data within Celonis.
  - Data type changes not handled: Also, note that if a metadata change is to the data type, the functionality will not handle the updates. For example, if a column’s data type changes from integers to a string the table will not correctly load. In this instance, a full load is required to remove the conflict.
  - Delta Loads are faster: If you are extracting tables that are continuously growing and extending, enabling this functionality will keep your delta loads running. In the end, Delta loads decrease your load time and are faster than full loads

### Performance Optimization
- Deselect irrelevant columns
- Apply filters to extract only the data you need
- Adjust the "Maximum number of parallel extractions"

## Extractions with Replication Cockpit
- Benefits
  - Real-time connectivity: Extractions are orchestrated automatically without user-defined schedules.
  - Automatic self-recovery: Extractions will correct and re-execute in case of temporary failures.
  - Speed & stability: Extractions run faster and are less error-prone because they are separated from transformations.
- Recommended: Transactional Tables (full and delta loads), not for Metadata Tables
  - Transactional Tables = typically change very frequently.


- Need a connection that supports change logs and triggers in the source system, e.g. SAP ECC or S/4HANA
- If an added table does not have a trigger/change log, you'll see a warning that these objects don't exist in the source system.
- You can use a replication template to easily set it up
- deleted records: you can decide to keep them in a separate table or delete them right away
- you can use data pool parameter (but not create ne local parameters)
- Initilazation join configuration = (Full Extraction) -> only on full load
- You have to Initizalize the table (initial load), but you can skip it if you want by clicking "replicate (all)
- In Scope setting: replication frequency, on error, calender
- you can set up emails whenever a table goes into a degraded state
- RC replication = DJ delta extraction
- RC initialization = DJ full extractions 

## Transform Data
1. building one or more Activity Table(s) with all relevant process activities
2. reworking as necessary your Case Table(s) and other relevant master data tables.

### Activity Tables
- possible additional columns user type, sorting, activity key (parent), 

### Case Table
- EKPO

### Master Data Table
-  more detailed information on vendors.

### Templates
- create by converting transformation into template. 
  - manage centrally, changes effect all
  - you can use parameter in templates

### Performant Transformation Basics
- Avoid SELECT * if possible and select only the columns you need to reduce system load.
- Avoid SELECT DISTINCT if possible as it is a taxing statement. The need for DISTINCT usually means something in your query or source system data is causing duplicates. More information on alternatives in the SQL Best Practices course.
- Move conditions into **Extractions** where possible. E.g. in our simple use case, the EKKO.BSTYP = "F" could have been moved to the EKKO table extraction.
- Move WHERE conditions directly into JOINS. This is what with did with EKKO.BSTYP = 'F'. It could have been applied using a WHERE statement at the end of our scripts but we added it directly in the JOIN:
- Use WHERE EXISTS instead of JOIN where possible. Don't use a JOIN if you only need to filter on another table.


### Tables vs Views in Transformations
- Tables
  - when needs to be accessed in transformations
  - create tmp tables when you join theses tables frequently in transformations
- Views
  - A view is a stored query
  - tables that are **not** used in our other transformation could be view (e.g. P2P_EKPO, P2P_EKKO)
  
### Real-Time Transformations
Steps:
1. Identify the trigger table
2. Define the transformation(s) on this Trigger Table
3. Define dependent tables


- Multiple activity tables are created
- initilazation could run weekly or monthly. Im Gegensatz zu Extraction where it should only run oce

How does it works:
1. Delta Extraction creates a staging table with delta records. 
2. Records are processed from Trasnformations. 
3. The staging table is automatically emptied.

- Delta Extraction use delete and insert instead of drop and create
- Delta Extraction use tables not views
- Initialization scripts should create empty tables. Adding a "LIMIT 0"
- Select all columns specifically
- Move Temp Tables into queries or use triggered Temp Tables


### Script Real-Time Transformations for Activities
https://academy.celonis.com/learn/course/transform/replication-cockpit-set-up-transformations/set-up-delta-real-time-transformations?client=partner&page=6
- Data Model Tables
  1. Identify the Trigger Table
  2. Select the Staging Table in query
  3. Use tables instead of views
  4. Use Delete + Insert approach
  5. Move Temp Tables into queries or use triggered Temp Tables
  6. Select all columns specifically
  7. Define dependencies
- Add Activities   
  1. Identify the Trigger Table
  2. Split the Activity Table into many based on Trigger Tables
  3. Use INSERT + WHERE NOT EXISTS in most cases (adjust based on effect of updates in Trigger Tables on your Activity Table)
  4. Move Temp Tables into queries or use triggered Temp Tables
  5. Define Dependencies



## Data Model

### Link Tables Correctly
- The Fact (N) table is always the table with multiple rows for one row in the (1) table. So in the Activity to Case table relationship, the Activity table is the Fact table (N), and the Case table is the Dimension table(1). In other words there are always multiple activities for one Case ID
- A Fact (N) table can have multiple 1 relationships with other tables, but a 1 table should not have multiple N relationships in your Data Model. Avoiding this is important for working within Analyses and the Process Query Language (PQL) later on.
- The Data Model only works with 1:N or 1:1 relationships. Cyclic relationships or M:N relationships should be avoided as they cause issues in the Data Model load and Analyses.

### How to
1. create Activity Table
2. Create case table and master data tables
3. Create relationships between tables in the Data Model (foreign key)
4. explicit assign case table

- Dimension table (1) and the Fact table (N)
- Data Storage + Query Engine = Process Data Engine

### Data Flow
1. Extraction: The first step is an extraction from a source system. As per an extraction configuration, Celonis calls the requested data from a source system directly or from an Extractor server installed in a closed hosting environment. This data lands in a transactional database known as the Celonis Data Storage.
2. Transformation: Next, the data is transformed according to your transformations and all new tables and results are also stored in the Data Storage.
3. Data Model Load: Once you’ve defined your Data Model and load it, Celonis pulls the data from Data Storage, transforms it into several parquet files (here is a good parquet definition), and using metadata information on your Data Model’s schema, stores it into the Query Engine. The Query Engine is an analytical database best suited for Analyses.
4. Downstream Activities in Studio: From here, you can now use this Data Model to create Analyses and other Celonis objects in the Studio.

### Partial Data Model Loads
- setup Data Job and configure the needed tables

### Capacity Recommendations
- Per table, aim to have no more than 800 million rows per table.
- Per individual case, aim to have an average case length of 20 activities or less.
- In the Activity Table, aim to have no more than 1000 distinct activities.

### Troubleshooting
- clearly sorted timestamps for your activities
- accurate case keys
- accurate joins between your tables
- clean and matching data in your activity and case table
- no data job running on your tables while you are loading your data model
- no delta extractions when no primary keys were defined


### Model Permissions
- Usage Permissions: who can use the model for downstream activities in the Studio such as an Analyses.
- Data Permissions: who can see which part of the data in the Data Model. Data Permissions allow you to restrict access to your Data Model for certain users. As an example, you could restrict the access of user A, in a way that the user could only see data for a specific company code when opening an analysis that builds on the respective data model.

## Schedule Data Jobs

### Schedules
- they only apply to entire Data Jobs, not to single tasks
- if a Data Job runs Extractions and Transformations, consider adding the applicable Data Model Load task
  - **Without a Data Model Load, your Data Job will have no effect on your Data Model**
  - if you use the Replication Cockpit for certain transactional tables (both full and delta extractions and transformations), you will still need scheduled Data Jobs for: Data Model Loads, the Delta and Full loads of tables you choose not to include in your Replication setup.
- Trigger-based schedule: Trigger the next schedule after the last finished


### Smart ETL
- before extractions and transformations run sequentially
- Celonis runs your extractions and transformations in Data Jobs in the optimal way
- turned on by default on task level
- you can activate Smart ETL at the schedule level.
- Note that Smart ETL for schedules works with frequency-based schedules but not with trigger-based schedules.

1. Calculates the optimal extraction and transformation order: Before each Data Job execution, Celonis calculates the optimal execution order of table extractions and transformations based on the dependencies in a Data Job. For extractions, it takes into account the allowed parallel extractions on a connection, i.e. how many tables Celonis can extract in parallel from a source system. 
2. Creates a DAG (Directed Acyclic Graph) representing the most efficient execution order to optimize for parallelism.
3. Uses DAG to trigger all extraction and transformation tasks based on the optimal calculated execution order. For example, once a table is extracted, the related transformations start automatically (while independent tables might still be in extraction).


## Monitor and Validate your Data Pipeline (optional)

## Connect Multiple Systems
#### parallel scenario: one system per country
- set up n connections, and then one Data Job for each connection.
- you should now have n activity tables and every raw data table n times.
- you can reuse extractions and transformations
- resuse: Use Templates and Parameters
- Merge with Global Data Jobs
  - A Global Data Job can access all the tables in your data pool and isn’t limited to one specific data connection.
  - n+1 datajob: n for each country + 1 Global Data Job for merging
  - create one transformation per table
  - use UNION ALL for merging

#### Sequential Scenario: different source systems with different structures, which run different steps of the process
- separate Data Jobs with different extractions and transformations, since they are different per system.
- merge only activity table into one table. Do not merge raw data tables, since they are different per system.

#### Global Data Jobs
- own schema
- access all data from the different schemas
- can’t create extraction tasks in it,
- use UNION ALL for merging

#### Unrelated Processes from One System
- e.g. Purchase-to-Pay data as well as the Accounts Payable in on esystem. But they are unrelated processes, so they should be kept separate.
- apart from the extraction job, you can keep the rest of your work separate in one Data Pool.

#### Multiple Related Processes
- use multiple Activity and Case Tables in one Data Pool =  Multi event log
- first Activity Table you define is the Default Activity Table. 
- Eventlog can be autommerged in PQL, but they are not merged in the Data Model. So you can keep them separate in the Data Model and merge them in Analyses and PQL when needed.
- cases for Multi-Event Log:
  - To put independent processes into context (filter across processes). 
  - To analyze parallel processes by linking multiple hierarchical Event Logs.
  - To reduce transformation script efforts (no joins) by merging Event Logs.
  - To visualize end-to-end processes by linking multiple Event Logs.

### Working with Data Pools
- you can sharing Data Connection between pools, if enabled
- you can version your datapool 
  - Data Jobs,
  - Process Data Models,
  - Data Parameters,
  - Task Templates,
  - Schedules.
  - NOT Data permissions
  - NOT Data Connection details,
  - NOT actual data
- you can copy a data pool
- you can copy datat jobs
  - Extractions
  - Transformations
  - Local parameters
  - Templates
  - NOT Data Pool parameters
  - NOT Data Model Load tasks
  - NOT Job alerts
  - NOT The tables and data  


## Extraction Performance Best Practices (optional)
- Enables data consistency for delta extractions, enables resumable/restartable extractions, increases performance.

## Boost your SQL Transformations
### Extract only the Necessary Data
- adjust process connectors, to make sure they extract only necessary tables]
- trim large tables (do you need all columns?)
- use extraction filters

### EXPLAIN plan
- written **before** SELECT statement
- estimated query cost:
- join type: 
  - merge join: If both tables are pre-sorted on the join column(s), the Vertica optimizer chooses a merge join, which is faster and uses considerably fewer resources than a hash join.
  - hash join: If tables are NOT sorted on the join column(s), the optimizer chooses a hash join
- A merge join will always be more efficient and use considerably less memory than a hash join. But it's not necessarily faster. If the data set is very small, a hash join may process faster but this is very rare.
- How to sort to get a merge join?
  - place key columns at the beginning (e.g., MANDT, VBELN, POSNR) of the CREATE TABLE statement,
  - Or add an explicit ORDER BY { key columns } clause at the end of the CREATE TABLE statement.

### Table Statistics
- summaries of tables that assist the query optimizer in making better decisions
- **source** table statistics are automatically gathered for each table after the extraction.
- For additional tables created during the transformation phase—e.g., the temporary join table TMP_CDHDR_CDPOS, or data model tables you create—it's necessary to create statistics explicitly. In general, we recommend you add statistics to all tables created and used in your transformations.
- Also, if you significantly change existing tables with INSERTs, DELETEs, or UPDATES, we advise you refresh statistics.
- For tables that have less than 10K records, we do not recommend creating statistics.  This is because the effort to create the statistics for these small tables in Vertica outweighs the time saved by the statistics.
- Why are table statistics so important: Among many benefits, table statistics are especially crucial for query execution plans with hash joins. They enable the query optimizer to choose the smaller table to build the hash table (instead of the bigger one). In most scenarios, this prevents an “inner join did not fit into memory” error and improves performance.
- How  to create statistics : `SELECT ANALYZE_STATISTICS ('TABLE_NAME');`
- how to check if there are statistics:
```
SELECT anchor_table_name AS TableName
FROM projections
WHERE has_statistics = FALSE ;
```

### General Best Practices
- WHERE EXISTS instead of JOIN: when you just filter and do not need the column
- do not use DISTINCT
- Use UNION ALL instead of UNION
- Use BETWEEN instead of AND for Ranges

### Temporary Join Tables
- Auto-projections: all table columns and are sorted by the first 8 fields
- you can add custom projections

- Common Table Expressions
  - for OCPM Transformations
  - "WITH ... AS" statement

### RECAP
- CREATE TABLE	
  - If the query contains complex definitions (e.g., multiple joins and conditions)
  - If other transformations (e.g., Activity scripts) are accessing the query result
- CREATE TEMPORARY TABLE	
  - If you use similar joins multiple times within one transformation task
- CREATE VIEW	
  - If the query simply selects the records from a single table (e.g., VBAP) and applies simple conditions.
  - In general, should be mostly limited to data model tables
- WITH ... AS ()
  - Common Table Expression (CTE)	
  - [Used in OCPM transformations] If the query contains complex definitions and/or repetitive joins.
  - Unlike a temporary table, CTE is not stored in memory or on disk. It's meant to improve readability and can be referenced multiple times within the same query.

https://academy.celonis.com/learn/course/sql-best-practices/transformation-best-practices/course-recap-and-next-steps?client=partner&page=1

### Staging Tables
- Best practice for **Data Model** in CCMP
- One staging table with all joins. View on top of this tabel which use only one join with the staging table

### Table Terminology
https://academy.celonis.com/learn/course/sql-best-practices/transformation-best-practices/usage-of-tables-temporary-tables-views-and-ctes?client=partner&page=4


### DELETE and UPDATE Statements
- Avoiding DELETE and UPDATE
- Rebuild Tables instead of DELETE and UPDATE
  - create new table and drop old one (and add table statistics)
- if you really neddd DELETE/UPDATE use smaller parts/chunks `DELETE FROM BSEG WHERE GJAHR=2020;` 
- When limiting the query through a condition, select a field that appears at the beginning of the table field 

### Avoid Business Logic in Transformations
- Business logic (KPI calculations, formulas, analyses, statistical evaluations, if/then/else) belong in the knowledge model


## Data Model Load Performance Best Practices (Optional)
- On top of delta extractions and delta transformations, you can set up delta data model loads
  - Each table needs an identifier (primary key) in the data model
  - Add the "epoch" column to each view in your data model. This column is available hidden in each table.
- Partial Data Model Load
  - selectively reload individual tables of a data model.
- Reduce or Disable Cache Preheating
  - Prheating cache for PQL. Mayeb makes no sense when fast data model load has a higher priority than a fast frontend performance
  

## General ETL Pipeline Performance Best Practices (Optional)
- Split the ETL Pipeline Based on the Type of Use
  - Analytics use-cases 
  - Operational use-cases
- Parallel ETL Based on Target Group
  - reating dedicated data pipelines for each region, country, business unit, or factory
- Use Trigger Based Schedules
  - based on the successful execution
  - avoids unnecessary waiting
  - using trigger-based schedules, For sequential data jobs **across** data pools. Within Datapool use "optimized schedule execution"
- Optimize Data Pool Architecture
  - Every table is only extracted once(exceptions possible) from a source system.
  - Extracted tables can be used by all projects (data pools) simultaneously.
  - Not every user can access every table and every record.
  - Data preparation, business logic, formatting, consolidations, etc. should be managed centrally and consumed by all projects.

## Push Data into Celonis (Data Ingestion API's )
### Specifications
- One API call per table: Every table you create or update requires one API call.
- Built on S3 API: It's built on top of the S3 API with the same methods and error codes. It uses primarily this S3 PUT object endpoint.
- Continuous load: The load is continuous. So as soon as you ping the API, your data is loaded into Celonis. It operates on a First In First Out (FIFO) principle.
- Auto-delta load: All pushed records are loaded as delta records automatically and compared to existing records.
- Nested data possible: The API can handle nested (json) data out-of-the-box and unnest it into tables and columns.
- UI schema configuration: It supports a UI based configuration for table schema, i.e. table names, keys, age columns.
- Parquet files only: As of today, the API only supports parquet files and requires you to convert to parquet before pushes.

### Usecases
- Existing data applications: data resides or is processed through other data applications such as:
  - ETL tools (e.g. Informatica)
  - Streaming Applications (e.g. Kafka)
  - IPaaS (e.g. Mulesoft)
  - Other scripts or Action Flows that rely on the older Data Push API or Continuous Data Push API
  - Ongoing file pushes
- Security concerns: data needs to be pushed into Celonis for security reasons, e.g. access to the underlying source cannot be granted.

- Replacement for Scripts and Actions Flows based on older APIs: much simpler Data Ingestion API.
- Ongoing file pushes: Many projects initially start with file pushes for a quick data check. This initial push is normally done using the file uploader. That said if pushing files (parquet) should be the long-term approach, then the Data Ingestion API is the right way to go.

### FAQ
- it's push, so no schedules
- Schema changes: As long as the primary key remains the same, a push with new columns will simply add the columns to the existing table and enter Null values if an older column is excluded.
- Delta loads
  - Delta loads (updates or new records) rely on the Primary Key and the Age field. The Age field is typically a date column that indicates when a record was created or updated.
  - If a new record is inserted with the same Primary Key value, then the one with the latest date is retained.
  - If no Age field is defined, then the new push's record is kept and updates the existing one.
  - Note that you can only define the Age column at the top table level. Nested tables rely solely on their primary keys and the parent table's fields for delta logic.

## Extractor Builder Basics
### When to use it
1. No existing extractor: There is no existing extractor for your source system and your source system allows access to source data via REST APIs.
2. Customize existing extractor: There is an existing extractor but you would like to customize it to your needs. You could for example:

### Extractor Templates
- you can only customize custom templates.
- Celonis-built template are copied and the customized

### Filters
- static
- use the parameter as a filter

### Dependent Endpoints
- dependent endpoint takes another endpoint’s output as its input.




----- 
Build an Object-Centric Data Model

## Object-Centric Process Mining: Foundations
### CCMP  
- tracks one object (case) per process and maps all process events into a sequential event log
- Value:
  - providing insight into processes based on the chosen case perspective.
  - allowing businesses to uncover and fix process inefficiencies.
  - helping businesses to track process performance against specific KPIs.
  - allowing businesses to fully or partially automate actions based on process data.
Limitation:
  - restricted perspective
  - Incomplete information, like Duplicates events or missing events


### OCMP
- case
  - Restricted perspective: A limited, fragmented, and fixed perspective	
  - Incomplete information: Missing information and context based on selected case in event logs
  - High Effort: Higher start and update effort due to SQL-based event logs	
  - System dependence: Low scaling due to source system dependent scripts	
- object
  - Flexible multiple perspectives based on a single standardized model
  - More accuracy thanks to object modeling
  - Lower start and update effort thanks to UI-based modeling
  - Better scaling thanks to standardized and system-agnostic objects

#### Objects
Expense Report
Expense Line
Expense Category
User
#### Events
Create Report
Send to Approver
Send Back to Creator for Correction
Change Amount
Approve Report
Reject Report


### Create Objects
- Manually create the objects, relationships, and transformations.
- OR import your objects from tables

- Each object has
  - a name
  - attributes (including an ID)
  - relationships
  - transformation scripts 
  - To put it simply, the goal of your work with objects is to create their shell (name and attributes), identify how they relate to each other (relationships), and fill the object shells and relationships with data (transformations).

#### Relationships
   m:1 relationships" a foreign key is added as an attribute to the object on the m side.


- Handling m:n relationships
  - an extra join table needs to be created to map the relationship.
  
### Tables and Table Names
https://academy.celonis.com/learn/course/build-object-centric-data-models/build-object-centric-data-models/build-your-object-centric-data-model?client=partner&page=12
- t_c_o_custom_Category
  - t = dev env, c = changes, o = object, custom = for types you create

o_custom = same as data input model
c_o_custom = objects and there state through the process (joined with changes)
e_custom = events
r_e_custom_Eventname_Object = r_e_custom_SendToApprover__Expense = event relationships for one 2 many


- As stated above, for events, all "involves many" relationships lead to relationship scripts.
- Your relationship script will create an extra table in the database to map every event instance to every related expense line. A sample table would look like this:

Perspective:
- In the case-centric approach, we define data tables, link them and then load them into a data model.
- In the object-centric approach, we define objects, events, and their relationships. We then choose which objects to include in a perspective. Each defined perspective becomes a data model we can load and use.



### Eventlog in Perspective
- For each object in your perspective an event log is automatically created

Define your own when:
- if you want to define a default event log to use in the Studio (e.g., in a Process Explorer). For custom processes, we recommend you define a default event log.
- if you want to create an event log that only includes certain events
- if you want to create an event log on a lead object and include events indirectly connected. E.g., You could add the "Change amount" event to the Report object. This is indirect as the "Change amount" event is only directly related to the Expense object.

Perspective =  create a sliced datamodel


### CCMP vs OCMP
- Extract - There is no difference here for now. Both approaches require a connection to systems and extraction of data.
- Transform - Whereas the case-centric approach requires you to create and populate your tables entirely with SQL, the object-centric approach eases the SQL burden on a few fronts:
  - Modeling of objects and events is click-based and automates table creation.
  - Populating (matching source data to objects and events) is simplified.
  - It only requires simple SELECT statements.
  - It is guided either through the import or with sample scripts in the editor.
  - Final scripts are automated and remove SQL complexity (temp table creation and deletion, performance pitfalls, syntax issues, etc.)
- Load - The workload here is reduced in the object-centric approach.
  - There is no need to link tables in the data model as relationships already exist.
  - You can create new data models (perspectives) and event logs with a few clicks based on your existing objects and events.
  - No need to rework transformations to create new event logs. The system handles this if you've defined the needed objects and events.

Can I use more than one system in one transformation script?
- Yes you can. Each transformation has a main data source by default. To point to a different source in the transformation, use the data connection parameters. Here is a simple example with two databases in one transformation: