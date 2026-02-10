# Write PQL queries
url: https://academy.celonis.com/learning-paths/build-analyses-advanced
access: https://fox57xlh-2026-02-04.training.celonis.cloud/package-manager/ui/views/ui/spaces

## PQL Engine

- a domain-specific language,
- tailored towards a particular process data model, and 
- designed for business users.

- formalize the  process questions as executable queries and calculate KPI
- translates process-related business questions into queries and executes them on a custom-built query engine

### PQL engine design goals
- simplicity
  - easy to use
  - translate complex process queistions into data queries
  - make process mining accessible to every Celonis user
- flexibility
  - set of generic functions and operators
  - wide range of combinations
  - formulate any question, regardless of the process
- event log centered
  - supports process mining functionalities
  - associates cases to events
  - dedicated process functions operate centered on the given event log
- business focused
  - combines process mining and business intelligence capabilities
  - augments event data with additional business information
  - variety of SQL functions
- frontend interaction
  - support if a graphical user interface
  - leads to high accpetance, usage and user adoption


### History
- 2014
  - SQL extension
  - commands to query and filter porcess flows and patterns
  - executed in the source DB system
- 2016
  - Patented independent language
  - optimized for Process mining
- 2018
  - cloud solution


### SQL VS PQL
- PQL does NOT support all operators that are available in SQL. (Language Scope)
  - only operators needed for the target use cases are implemented
-  PQL is NOT supported by a data manipulation language (DML)
   - all updates in the Process Mining scenario should come from the source systems,
-  PQL does NOT provide any data definition language (DDL).
   -  As the data model is created by a visual data model editor and stored internally, there has not been any need for creating and modifying database objects.
- PQL is domain-specific 
  - and offers a wide range of Process Mining operators not available in SQL.

### Foundations of Process Mining
- Process Mining comprises data-driven methods to discover, enhance, and monitor processes based on such data
- The heart of Process Mining are the Event Logs. Those Event Logs are a collection of process events that can be described by the following attributes:

### Attributes (these attributes are mandatory for an Event Log)
- Case: indicates which process instance the event belongs to, consisting of multiple events
  - example: Order Number is the unique case ID, and all related activities are assigned to this ID
- activity: action that is captured by the event.
  - Example: all the steps an order has passed through, from receiving the order, to cooking the meal, delivery, and payment.
- timestamp: indicating precisely when each event took place.

### Language Overview
#### View before examen:
https://academy.celonis.com/learn/course/pql-and-the-celonis-pql-engine-an-introduction/introduction-to-pql-and-the-celonis-pql-engine/celonis-process-query-language?client=partner&page=3

### PQL is used in applications
- knowledge model: the cental place
- action flows: as filters
- ML workbench: to query data

## Basic Coding with PQL
### PQL operators
- aggregation: counting, evaluating, stochastic
- data flow: CASE WHEN, REMAP_VALUES, COALESCE
- Predicate Functions: BETWEEN, IN, IN_LIKE, LIKE, IS NULL, ISNULL, <>, =, !=, NOT
- String modification
- Window functions: perform calculations in a partitioned table / LEAD, LAG

- activity table = event log

### Aggregations
counting: COUNT, COUNT_TABLE, COUNT DISTINCT
evaluating: AVG| MEAN | TRIMMED_MEAN, MIN | MAX, SUM, 
stochastic: QUANTILE, STDEV, VAR

- NULL values, they are ignored in all of the aggregation functions | The only exception is COUNT_TABLE
- TRIMMED_MEAN ("Matchbox"."Price", 20, 20) =>  takes the lower and upper cutoffs as parameters. Here, 20 % of the total rows
- Nesting of standard aggregations (e.g. SUM and COUNT_TABLE) is not possible. like SUM(COUNT_TABLE("Activities"."Activity")) is not allowed.

#### Counting:
- default grouping
COUNT (DISTINCT "Matchbox"."Type")
- this is automatically grouped by Type = Streetcar, Construction. Racing Car

#### gloabl grouping
- GLOBAL ignores the gouping and calculates the aggregation over the entire result set
SUM(Matchbox."Price") / GLOBAL (SUM(Matchbox."Price"))


### Data Flow 

#### REMAP_VALUES with default value
- CASE WHEN: If else statement. Evaluates a list of conditions and returns one of multiple possible result expressions.
- REMAP_VALUES ("EKKO"."BSART",  ['StPuOr', 'Standard Purchase Order'], ['PlPuOr', 'Planned Purchase Order'], Other Purchase Order')
- REMAP_INTS: same as before juts with ints
- COALESCE: returns the first non-null value in the list of arguments.


### Predicate Functions
LIKE: Implicit %x% => then search becomes case insenitive
ISNULL: 1 | 0
IS NULL: true | false

### String Modifications
- LOWER, UPPER, REVERSE
- LEFT, RIGHT, LTRIM, RTRIM, SUBSTRING, CONCAT, REPLACE
SUBSTRING: ("EKKO"."BSART", 1 START, 2 SIZE)

### Datetime Modifications
- ADD_X
- ROUND_X = FLOOR_X

### CONVERISIONS
- if conversion not possible then NULL
- TO_DATE
%Y: 4 digit year.
%m: 1-2 digit month of the year. A leading zero is permitted, but not required.
%d: 1-2 digit day of month. Leading zero is permitted, but not required.
%H: 1-2 digit hour of the day in 24-hour format. A leading zero is permitted, but not required.
%M: 1-2 digit minutes per hour. Leading zero is permitted, but not required.
%S: 1-2 digit seconds per minute. Leading zero is permitted, but not required.
%%: A literal "%" character.


## Process-Related Functions in PQL

#### PROCESS EQAULS
PROCESS EQAULS 'Scan Incvoice'
to (ANY TO) 'Create Invoice'
to (ANY TO) 'Post Goods Receipt'

#### MATCH_PROCESS_REGEX 
MATCH_PROCESS_REGEX 
("ActivityTable"."String Column", Regular expression)
MATCH_PROCESS_REGEX 
("ActivityTable"."Activity Column", ^ 'A' >> ['B','C'] >> (ANY)* >> Y >> 'Z' $)

#### CALC_THROUGHPUT 
AVG(CALC_THROUGHPUT 
(FIRST_OCCURRENCE [ 'Create Purchase Order Item' ] 
TO LAST_OCCURRENCE ['Scan Invoice'] , 
REMAP_TIMESTAMPS ( "ACTIVITIES"."EVENTTIME", DAYS)))

CASE_START, CASE_END are possible for FIRST_OCCURRENCE | LAST_OCCURRENCE

#### CALC_REWORK
- how often a specific activity occurred
- How often has changed quantity per case?
CALC_REWORK ( "ACTIVITIES"."ACTIVITY" = 'Change Quantity' )

#### CALC_CROP
CALC_CROP(CASE_START TO FIRST_OCCURRENCE['Receive Goods'],"ACTIVITIES"."ACTIVITY")
- use CALC_CROP_TO_NULL if the name should remain. Otherwise it results to 1 or null


### Process Index Functions
INDEX_ACTIVITY_ORDER
INDEX_ACTIVITY_ORDER_REVERSE
INDEX_ACTIVITY_TYPE: Grouped by type starts by one for each new activity
INDEX_ACTIVITY_TYPE_REVERSE
INDEX_ACTIVITY_LOOP: activity has occurred in direct succession 
INDEX_ACTIVITY_LOOP_REVERSE


### Aggregations and Execution Times
max/min => sum/avg => median/quantiles => var/stdev => trimmed_mean
- If you have the choice between AVG and MEDIAN, choose AVG
- If you can choose between COUNT and COUNT DISTINCT, choose COUNT.
- use REMAP_VALUES instead of CASE_WHEN


## Joins & Filters in PQL
### Relationship
- Celonis supports 1:N relationships
- n side always on the left side of the join
- Activity Table is the snowflake table
- implicit joins: left-outer join: all rows from left side and matching rows from the right side. If no match, then NULL values for the right side
- common table is the table on the most N-side.
- There is no common table when you have to go from n -> 1 to get to this table


### Execution Order
1. Joins and regular PQL functions (not aggregations). The common table is defined after joining the required tables.
2. Filters are applied (if there are filters defined). We will learn more about filters in chapter 4.
3. Standard Aggregations (AVG, COUNT, SUM, etc.).

### Filter
- filters will be connected one to another following the AND logic

### Filter propagation
- Filters are propagated along the foreign keys

## Use PU-Functions in PQL (Pull-Up Functions)
- PU functions are used to pull up values from the N-side to the 1-side in. Results in a cloumn on the 1-side table
- add a column in the target table
- Start with AGG type PU_SUM, TARGET TABLE = table on the 1-side
- PU_SUM(TARGET TABLE, SOURCE TABLE.COLUMN)

### Specifics of PU-functions
- all AGG functions + PU_STRING_AGG, PU_FIRST, PU_LAST
- can be nested (unlike aggregations)
- can be used inside filter statements (unlike aggregations)
- use filter as argument e.g. PU_COUNT ( "Cases", "Activities"."Activity", "Activities"."Activity" LIKE 'A' )
- NEVER introduces a new 1:N relation
- we always aggregate from the N-side to the 1-side.
- We can also aggregate data across multiple tables as long as the 1:N relations build a row
- minimize joins by using PU functions
- PU function can be used as CASE WHEN condition
   CASE WHEN PU_SUM("Books", "Chapters"."Pages") > 500 THEN 'Long Book' ELSE 'Short Book' END

### Using PU-functions inside filters
- can be used inside filters: FILTER PU_COUNT("Cases", "Activities"."Activity") > 3;
- PU-Functions do not consider FILTER statements. e.g. FILTER "Cases".Value > 20 is not applied when PU_SUM() is used All itmes go into the sum calculation, even those with value <= 20.
- use Filters inside a PU-Function

### Error messages
PU_FUNCTIONS: N:1:N relationship
BIND: 1:N:1 relationship
- PU_SUM("Authors", BIND("BookAuthorMapping", PU_SUM("Books","Chapters"."NumberOfPages")))

## Use Domain Tables in PU-Functions
- Can only be used as TARGET table in PU_FUNCTIONS: TRAGET = 1 side of the relationship, SOURCE = N side of the relationship
- Temporary table
- Table to Domain table has always n:1 relationship
- can only be used within PU_FUNCTIONS
- use if target and source table in the PU_FUNCTION are the same
PU_COUNT ( DOMAIN_TABLE ( "People"."Country Code" ) , "People"."Name" )
PU_COUNT ( DOMAIN_TABLE ( ROUND_DAY ( "People"."Date of Birth" ) ) , "People"."Name" )
PU_COUNT ( DOMAIN_TABLE ( "People"."Country Code", "OtherTable"."Stuff" ) , "People"."Name" ): for this a common table is created


### Performance Optimization in PQL

### Cache
- The time taken to respond decreases for queries answered from the cache.
- The number of answerable queries increases due to better resource utilization.

### What is cached?
- the results of any standard aggregation are NOT cached.
- filter-independent calculations are cached
- results of the PU-function WITHOUT filters are cached.