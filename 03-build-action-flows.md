# Build Action Flows
url: https://academy.celonis.com/learn/learning-path/build-action-flows
access: https://fox57xlh-2026-02-04.training.celonis.cloud/package-manager/ui/views/ui/spaces

## Introduction to Action Flows
- Which processes can I automate?
- Why should I automate my processes?

### What is an Action Flow?
- Celonis Studio allow you to automate your business processes
- Used in Celonis Apps along with Knowledge Models, Views, and Analyses
- In simple terms, an Action Flow is a way to define an automated process flow. 
- It consists of multiple **events**, **decision points** and **alternative routes**
- It can involve an arbitrary number of different applications.
- Action Flows are here to bridge gap of **multi-system workflows**, e.g saleforce, teams, calendly
  
### Things to automate in action flows
- certain extent of **repetitiveness** but are carried out **manually**?
- certain pattern that you could easily **write down** in a manual or documentation?
- executed **multiple times** per day but don’t involve any **decision-making**?


### Action Flow Usecases
- Smart Goods Receipts: Requisitioners can post Goods Receipts right from the Celonis interface 
- Block duplicate invoices: 
- Update delivery date for sales orders: Identify sales orders whose delivery date is at risk => calculates a realistic delivery => notify customer

### Approaches
- Process Mining First
  - 1. Real-Time Data ingestion, 2. Process & Task Mining, 3. Automation, 4. Visual and Daily management
  - can be thought of as a circular process.
- Automation First
  - 1. Automation, 2. Real-Time Data ingestion, 3. Process & Task Mining, 4. Analytics

#### Process & Task Mining
- **transform** raw data into a Knowledge Model 
- View the as-is end to end business process to identify an area to automate.
- **Prioritize automations** according to impact on KPIs or the frequency of a task.

#### Automation
- Configure a **sensor** to **continuously monitor** the life cycle of a business process.
- Configure and test the workflow using the drag-and-drop functionality and **low-code rule editor**.
- Maintain your **Connections** and On-prem Agents in **one spot**.
- **Use variables** to make automation workflows **reusable** and simplify collaboration.

#### Visual and Daily management
- Govern and **monitor** your automation in real-time.
- Create analyses in Celonis Studio using a low or even no code editor.

#### Analytics
- Create **analyses** using a drag & drop editor.
- Monitor complete **audit trail** of every execution.
- **Monitor** your automation initiative to ensure it **runs as expected**.
- **Measure and observe** your **success**, for example by calculating the **value of resources saved** through your automation.

### Action Flow Building blocks
- module: **descision point** or **action**, receives input, produces output, **processes** each **bundle one-by-one**
- bundle: **inputs/outputs**, contains any type of data
- tools ARE MODULES: 
  - filters: apply filtering between any two modules
  - routers: routing and multiplexing

### Types of modules
- action module: 
- trigger:
  - instant trigger
  - polling trigger: e.g watch worksheet row and do something
- search: returning results after a search
- Tools:
  - iterator-type: iterates through multiple, e.g. email attachments (IS A TOOL?)
  - aggregator: opposite of an Iterator, accumulates multiple bundles into a single one, e.g. zip emails (IS A TOOL?)

### Connections
- user connections: to **connect** to particular application (username/password / token)
- **connections are personal** user connections, only you can view them
- **maintain** all your connections on the **global page Connections**.

### Agents
-  installed in the **customer's server environment**
-  **selectively access** customer-authorized **on-premises apps**
- one Celonis Agent to connect to an **arbitrary number of on-prem systems** int the **same network**

### How to come up with automation ideas
- REFLECT | What are your recurring tasks?
- OBSERVE | Is there some more?
- IDEATE | How can you improve?

## Action Flow Templates

### Blueprints
- easier to get started
- reusing best practices 
- simplify how you can share Action Flows (import of a .json file)

### Action Flow Templates Types (exist in the marketplace)
- snippets: generic templates, inserted into an existing Action Flow OR inspire a completely new Action Flow automation
- use cases: more specific, end-to-end Action Flow automation


### Wrap up 1. Action
- Data and mapping (putting template vars into slack template)
- function, e.g format date
- connections (slack autrh)

### Debugging
- **History** (right) and **Statistics** (bottom) helps you 

## Schedule an Action Flow
- editabel only in "view mode"
- At regular intervals is leveraged. 
  - Using this option you can set up a trigger to execute on different days and times in different months. 
- Advanced Settings to set up an overall start date and end date 
  -  These settings will override any individual configuration you have set up. Meaning: If one of your schedule items has a date outside this date range, it will not be triggered.

## Trigger Action Flows from Knowledge Models

### Triggers in Knowledgemodels (Watch Trigger)
- **detect the relevant results** and can be used to **automatically execute Action Flows**. 
- Triggers that listen for new insights based on Knowledge Model
- conditions and properties can be shared across Triggers
- All attributes of the record are available in the action flow
  
### Knowledgemodel key elements
- records: core item that is tracked in Process Mining analysis
- filters: describe business conditions
- triggers: objects you want to detect and automate for


## RPA
### Robotic Processing Automation:
- emulates click path
- automates repetitive rule-based tasks
- not the same as AI. RPAs only perform tasks

### Why
- Increading number of automation use cases. Multiple use cases require automation actions in the front end UI
- Maximize a single Action Flow to combine API-led automation of Action Flows with UI;led automation of RPAs

### How
- Query Data Module - > Trigger the bot (RPA app) -> Router


## Set up Actions for Attended Automation in Views
Actions: Actions are **links between an Action Flow and a button** in the Celonis interface. The configuration of these **Action buttons** is **stored** in the **Knowledge Model** and connects the button to an Action Flow which can be triggered manually. Once created, Actions can be added to **Celonis Tables** and **Profiles Views**.

### types of automations
- attended: Actions
- unattended:  Action Flow Triggers.

### Attended
- when human judgment is needed. 
- Some Actions require the user
- created via the Knowledge Model
- The end goal of building Actions in Views is to enable the business user to apply an automated action to an item that they see in their front-end View

### Actions
- build in Knowledge Model by Analyst
- linked to only **one record** and **one Action Flow**


### Send http requests in Action Flows
set vars with "set variables tool" 


## Receive and Respond to Webhooks in Action Flows

### What are webhooks
- "instant" is always a good indicator
- Webhooks actively inform you about events happening in a particular system
- they actively inform you about events in the system
- for push notifications
- In most use cases, Action Flows act as the receiver
- Alternative you can do polling

### How to
- create cutom webhook
- determine datastrcuture by calling the webhook
- create a webhook response for custom response data
- If you use HTML tags in your body response, make sure to tick "Show advanced settings" and to add a new custom header item with the key Content-type and the value text/html

### Validate Incoming Data
- create data structure
- strict / vs non strict


## Error Handling

### Main errors in Action Flows are
- A service is temporarily unavailable.
- A service responds with unexpected data.
- The validation of input data failed.

### Type of errors
- Bundle Validation Error: input validation
- ConnectionError:
- DataError: incorrect mapping
- Timeout Errors 
- Invalid Configuration Errors
- RuntimeError: if none of the others apply

### Directives
- special types of modules that are only executed when an error occurs.
- Rollback is default

### Types of directives
https://docs.celonis.com/en/using-error-handlers-in-action-flows.html
- continue
  - resume: allows you to specify a substitute output for the module with the error and the Action Flow execution status is marked as a success. 
  - ignore: simply ignores the error and the Action Flow execution status is marked as a success
  - break: stores the input to the queue of incomplete executions and the Action Flow execution status is marked as a warning. The the warnings have to be resolved manually
- stop
  - rollback: stops the Action Flow execution immediately and marks its status as an error
  - commit: stops the Action Flow execution immediately and marks its status as a success
