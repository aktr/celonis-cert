# Build Views
url: https://academy.celonis.com/learning-paths/build-dashboards-basic
access: https://fox57xlh-2026-02-04.training.celonis.cloud/package-manager/ui/views/ui/spaces

## Getting Started: Build Views

## Introduction to Celonis Studio
Core Services:

- Data: Data Source, Data Models
  - For Data Engineers: Data Integration, Objects and Events, Machine Learning, Task Mining
  - Bring in  data, shape it into data models
  - Get it ready for value discovery

- Studio
 - For Data Analysts: build and customize celnonis Apps 
 - Knowkedge Models: Centrally stored business definitions
 - Views: Visualize and explore data
 - Action Flows
 - Process Copilots

- Apps
  - For Business Users and ENd Users: Use Celonis Apps to discover insights and take action

- Marketplace
  - All users can browse the marketplace

- Transformation Hub
  - ? 

- Admin & Settings
  - Permissions, security, user management, API keys, licenses, etc.

### If you don’t want to create apps from scratch
Business Miner
- simplified and guided experience to deliver process insights
Markeplace
- pre-built content available


### Spaces
- Spaces help you to organize Packages
- Spaces have linked to Data Models
  - Suggested Data Models: are recommendations provided to analysts creating Packages within the Space. They establish the “default” Data Models for Spaces, streamlining the selection process for other analysts working within the same Space.

### Packages
- each Package is meant to focus on a specific use case
- typically build one app per Packagehttps://academy.celonis.com/learning-paths/build-dashboards-basic
- package contains all assets needed for the app
  - Views
  - Knowledge Models (only seen in studio, not in app)
  - Action Flows
  - etc.

### Permissions
- On Space Level, Packages Level, and Asset Level
- Template Roles
  - Admin
  - Editor
  - Viewer
- Permission options
  - use package
  - edit package
  - delete package
  - manage permissions

### Examples of Studio Structure
- By Process / Opertating Model: e.g. order management, procurement, etc.
- By Subsidary / Department: e.g. Celonis Germany, Celonis US, etc.

General recommendation: 
- 1 Space for 1 Data Model
- 1 Package for 1 app or use case
- Folders to separate/group the different types of Assets

## Fundamentals of a View

### Knowledge Model
- semantic layer between the Data Model (DM) and View
- Knowledge Model interacts with Data Models,
- Knowledge Model stores all the reusable business definitions and knowledge on the App (Package) level.
- In order for all these assets to have a coherent language, you’d need a central repository of all the knowledge on an App level 
- common knowledge is shared throughout the App.
- storing and reusing business logic across different Views.
- You can utilize both the Knowledge Model and Data Model to build View components.
- View can be connected to more than one knwoledge model, but typically you would have one knowledge model per package/app.

### PQL 
You can use
  - Data (more or less the Data Model)
  - Knowledge Model
    - metrics
    - filter
    - variables
  
### Knowledge Model vs Data Model
- Data Model: technical layer, how data is stored in the system, tables, columns
- Knowledge Model: semantic layer, business definitions, reusable logic, how you want to talk about your data in the app
- Knowledge Model Records = Data Model Tables
- Knowledge Model Attributes = Data Model Table Columns 

### The Component Settings
- common layout options
- component information
- menu option

## Configure Charts and Tables in a View

### Dimensions and Metrics
Dimensions
- attributes or characteristics of the data that provide context and allow for categorization and analysis.
- Examples: time, location, product type, customer segment
- dimensions define the possible level of metrics for your data
- For example, if the dimension is a date that has been rounded by the months of the year, there will be a maximum of 12 possible metrics visualized in the component.
Metrics
- Metrics = KPIs
- Metrics are the quantitative measures that you want analyzed
- They are aggregated values
- e.g. number of sales orders, order rejection rates, throughput time.

### Category Charts: Bar Chart
- Comparing multiple categories of data within a dataset.
- Tracking performance metrics across different groups.
- Identifying patterns and outliers within categorical data.
- Communicating insights and findings to stakeholders in a clear and concise manner.

### Time Series Charts: Line Chart
- Detecting trends and seasonality in time-based data.
- Identifying patterns, cycles, and anomalies.
- Making forecasts and predictions based on historical data.
- Analyzing the impact of interventions or changes over time.
- Communicating temporal trends and insights to stakeholders effectively.

### Table
- Presenting detailed data with multiple attributes in an organized manner.
- Facilitating comparison of values across different categories or dimensions.
- Allowing users to search, sort, and filter data to find specific information.
- Supporting data exploration and analysis by providing an overview of dataset contents.
- Providing a structured layout for displaying data that complements other visualizations on the dashboard.

Technically, the table component treats attributes and metrics equally - consolidating all data columns without distinction.
-  breakdown selector can help - allowing you to switch between various attributes in the leftmost column of the table! 


## Visualize Processes in a View

### Use Case Briefing
- In process mining, you analyze business processes using data that has been transformed into event logs. 
- Process Explorer, Variant Explorer, and Case Explorer components in Views to visualize your business processes and their details.


### Configuring the Process Explorer
- The Process Explorer is a component in Views that uses event logs to visualize business processes
- Multiple Event Logs (i.e., objects) and their relationships can be visualized in the Process Explorer natively if you’re building on an Object-Centric Data Model
- using the Process Explorer, business users can add the most frequent events and connections to explore how their processes function.

### The following are the standard KPI Groups available out of the box
- Object and Event counts: Providing an overview of the number of objects and events within a process, highlighting their relationships and occurrences. It helps in understanding the fundamental structure and flow of the process.
- Throughput Time (Average): Calculating the average time taken between events. It helps in identifying general efficiency and areas where time can be optimized.
- Throughput Time (Median): Measuring the median time taken between events, which is the middle value of all affected objects. It helps in understanding typical process duration, minimizing the impact of outliers on the analysis.
- Throughput Time (Trimmed Mean): Calculating the mean throughput time after removing a specified percentage of the shortest and longest times from the dataset. It provides a more robust average by reducing the influence of extreme values, giving a clearer picture of process performance.

- Take note that the default process graph (upon creation of the Process Explorer) is the most common variant of the process that starts with the most common start event and ends with the most common end event. After that, your business users can only discover their processes through the addition of the most frequent events or connections individually.

### Configuring the Variant Explorer

Process Explorer vs Variant Explorer
- By using the Process Explorer, business users can gain insights into the overall structure and functionality of their business process.
- By using the Variant Explorer, they can gain insights into all the different ways an individual process has been executed in the field.

### Configuring the Case Explorer
- The Case Explorer is essentially a pre-made table with default columns and a case detail panel (on the right). You can view specific case details such as number of activities, throughput time, timestamps of activities, and other information related to the case.
- Case Explorer is also helpful to deep dive into the specific cases involved in or to validate particular process flows.
- main event log should be of the highest granularity 

### Customizing Event Logs in Studio


## Build Filters in a View
- 4 possible levels of filtering available
  - component level
  - tab level
  - view level
  - package level

### Component Filter

- predefined filters can’t be seen by business users in App
- Component filters are typically applied for specific use cases, such as benchmarking using components with different Knowledge Models 
- here is no clear indication that components have filters configured in them to business users -> consider communicating

### Tab Filters
- predefined filters can’t be seen by business users in App
- influence all components within their respective tabs.

### View filters 

View filters affect all tabs and components within the tabs of a View. You can apply View filters in three ways:
- Setting up predefined filters in Studio
- Filtering using components in Apps
- Using advanced filters in Apps

Options
- Read-only for user: user can not enable disable the filter, it is always on
- Hide from user: Filter is not shown in the app (but applied)

### Filtering using Components
- apply to the entire View.

Filter components are:
- Filter Dropdown
- Date range
- Quick Filters
- Search

Into the filterbar you can only put:
- filter components,
- input components
- buttons
- and other design elements.

### Components
- components to apply View filters (e.g., charts, table, process explorer). 
- this can be disabled
  - Exclude from user filtering: excludes the component from being subjected to View filters applied by the business user. Predefined filters will still affect the component.
  - Can’t be used to set filters: stops any filtering possibility from the component. Most of the time, this prevents business user interaction on the component.

### Global Filters
- predefined “package filters” that you can apply using the Knowledge Model.
- filters that have been applied to all Knowledge Entities in the Knowledge Model