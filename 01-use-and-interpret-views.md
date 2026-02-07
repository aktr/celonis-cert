# Use and interpret views
url: https://academy.celonis.com/learn/learning-path/use-and-interpret-views
access: https://business-user.training.celonis.cloud/

## Introduction to Celonis Apps & Views

### Types of Apps
- Analytic Apps 
  - insights how your process is performing data visualizations and KPIs.
- Operational Apps
  - support and streamline day-to-day operations (e.g. duplicate invoice checker app, unshipped orders app)


### Views
- asset visualizes the data within an App. Like a page or a dashboard

#### View components
- KPI List
- Variant/Process Explorer
- Charts
- Tables

#### Navigation Components
- Tabs
- Bookmark
- Export
- restore default view
- Object Count (Percentage of data you are viewing)
- Filter
- Filter Bar
- Linked Views



## Interact with Charts and Tables in Views

### What are Process Metrics?
- quantitative measures used to evaluate the efficiency and quality of a specific business process. These are often the key performance indicators (KPIs) 
- In Views, process metrics or KPIs can appear as a standalone number or in charts and tables.

Examples:
Order: Blocked Orders
Accounts Payable: Cost-per Invoice
Account Receivable: Days Sales Outstanding (DSO)
Inventory Management: Material Availability
Procurement: Open Requisitions


### What is a Dimension?
- attribute or characteristic of the data that provides context and allows for categorization and analysis.
- Examples: time, location, product type, customer segment

### Charts and Tables
#### Types
- Category Chart
- Time Series Chart
- Distribution Chart
- Tables


## Process Mining Key Concepts  
### Process Mining Types
- Case-Centric Process Mining (CCPM) .
- Object-Centric Process Mining (OCPM)

### What is a process?
- A process is a series of steps and decisions to complete a task.
- Every step of a business process leaves a digital footprint in transactional systems in the form of event log data
- Process mining software works by using this event log data to create a living picture of what actual processes look like

### Case-Centric Process Mining (CCPM) 
- tracks a single type of object as it moves through a process
- All events, like creating or changing an item, are tied to that one object.
- These events are stored in an event log, which records timestamps, activities, and the relevant case ID
- Case-Centric Process Mining focuses on isolated perspectives (e.g., analyzing only tires)

#### Problems with this approach
- For example, if an order contains five different line items, an event like “Order Cancelled” might be repeated once for each line item, which can lead to duplicate events even though the event only happened once at the order header level.


### Object-Centric Process Mining (OCPM) - 3D view
- The ability to capture multiple objects, events, and their relationships.
- The ability to dynamically choose the right perspectives to look at your business from any angle.
- Identify interdependencies between objects.
- Choose specific perspectives based on your analysis goals (e.g., focusing on the car, the tires, or the pit crew).

### Defintions
Objects: sales order
Events: order shipped
Relationships: object to object and event to object relations. These can be one to one/many
  In order management event to object relationship:
  The event "order shipped" affects multiple object types: shipment, invoice, and sales order.
  One instance of the event "order shipped" will most likely have a one to one relationship with invoice and sales order respectively.
  But one instance of the event could have a one to many relationship with shipment if the order is split into multiple shipments.

  In order management object to object relationship:
  One sales order can relate to multiple shipments and one shipment can also relate to multiple orders. This is a many to many relationship (m:n).

## Variant Explorer in Views
- Which exact paths do cases take, and how often?

With the Variant Explorer, you can:

- Review variants individually.
- Compare multiple variants to one another.
- Review the variants with process metrics or the Key Performance Indicators (KPIs) available in your dataset.
- Use the various filtering options.

### VE
- show by default the most common variant: this means largest group of objects going through the same set of events


## Process Explorer in Views
- What does the overall process look like?
  
With the Process Explorer, you can:
- review events, connections, and objects types.
- explore how multiple object types relate to each other and connect across events.
- switch between different KPIs.
- use the various filtering options.

### Value of PE
- untangle the complexity of processes
- focus on parts that require attention

### Graph Controls
- Panel: both direct and indirect connections between events are considered
- Slider: only direct connections between one event to another are considered

#### Events vs Connections
- the numbers on events represent event counts (how many times that event was performed in total)
- numbers on connections represent object counts (how many objects moved from one displayed event to another).


### Process Exploration
- Global Slider: add the next most frequent event from across all object types at once
- Hide Events: hide specific events , but it does not filter out the objects associated with it
- Connecting Multi-Object Process: adjusts all your sliders to the minimum state required to connect all the objects. If it's not possible to connect all objects, the button will adjust the process graph to the state with the fewest disconnected objects.
- Process Animation

### Filters in the Process Explorer
- objects using events and connections
- filter bar
- built-in filters

### built-in filters
- attribute filters
- process flow filters: e.g object is directly followed by another event
- event filters: Include or exclude objects that contain one or more events. Using multiple events you have to apply ANY or ALL logic.
- event count filter: e.g. events like the paying of an invoice happened more than once.
- throughput time filter: processing time between two selected events is within the specified throughput time range

## Process Explorer and Variant Explorer in Views
Object types: Sales Order Sales Order Item, Delivery
In Process Explorer you can select multiple, in Variant Explorer you can select single
When selecting only one object type and including all its events and connections, you get the same picture in the Process Explorer as you do in the Variant Explorer when all process variants are selected. => TRUE


## Discover the Process Adherence Manager
Why?
delay, bottelnecks, inefficency effcts production and customer satisfaction.
- find root cuases of late delivery


### Task Inbox
- The View focuses and filters on each record. Records can contain several different tasks.
- The Task Inbox focuses and filters on the same task types. It provides details for one task.