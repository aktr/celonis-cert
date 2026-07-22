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
- Increasing number of automation use cases. Multiple use cases require automation actions in the front end UI
- Maximize a single Action Flow to combine API-led automation of Action Flows with UI;led automation of RPAs

### How
- Query Data Module - > Trigger the bot (RPA app) -> Router


## Set up Actions for Attended Automation in Views
Actions: Actions are **links between an Action Flow and a button** in the Celonis interface. The configuration of these **Action buttons** is **stored** in the **Knowledge Model** and connects the button to an Action Flow which can be triggered manually. Once created, Actions can be added to **Celonis Tables** and **Profiles Views**.

### types of automations
- attended: Actions
- unattended: Action Flow Triggers.

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


## SAP

### Action Types
- Out of the box SAP actions: Out-of-the-box SAP actions are configured easily by both business users and SAP experts regardless of their experience with SAP. Similar to any other action (e.g. Weather - Get current weather, Slack - Create a message) in Action Flows.
- Advanced SAP actions: Your keyword being: Generic Remote Function Call (RFC). 

[//]: # (UPDATE EXAM START)
## Defining Action Flows: The "What" of Automation
_**Hint:** Possible Questions: Identify where Action Flows fit in the Celonis platform and explain how they differ from the Orchestration Engine.

Architecturally, Action Flows are a specialized iPaaS (Integration Platform as a Service) built directly into Celonis. They provide a secure, high-speed bridge between your process intelligence and your tech stack. By using a low-code interface, they remove the need for complex custom coding, allowing you to turn insights into system-level reality in seconds.

Why "Transactional"?

In the world of automation, "transactional" refers to discrete, short-burst units of work. Action Flows are built for precision and speed, handling tasks such as:

- Automatically updating specific records in an ERP.
- Sending a targeted alert to a team member based on a live condition.
- Triggering a bot to download a specific document.

Three Ways to Close the Loop
- Action Flows aren't just for "autopilot" automation; they are flexible enough to support various business strategies. Depending on the complexity of the task, you will typically build one of three types of flows:
  - Full Automation: Identify issue -> execute workflow -> 
  - Human-in-the-loop: Identify issue -> Validate -> fix issue
  - Intelligent Reporting: Identify issue -> summarize -> acknowledge
  
### Action Flows vs. Process Orchestrations
As you explore the Celonis Platform, you will encounter two primary ways to drive action: Action Flows and the Orchestration Engine (referred to in Studio as a Process Orchestration asset). While they often work together, they serve different purposes.
While it is important to understand how these two engines complement each other, this course focuses exclusively on Action Flows. If you are completing this as part of the "Build Action Flows" training track, you will find a deeper dive into the relationship between these assets in a later asset.

| Category | Action Flow | Process Orchestration                                                                                                                                                                                                                           |
|----------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Analogy** | **The Musician** — Think of an Action Flow as a specialized musician. A violinist is an expert at one specific task: playing the violin. They are fast, precise, and transactional. | **The Conductor** — The Orchestration Engine (or Process Orchestration asset in Studio) is the Conductor. The Conductor doesn't play an instrument; instead, they manage the entire performance. They know which musician should play and when. |
| **State** | **Stateless** — When the song ends, the musician doesn't need to "remember" the notes to perform the next task. | **Stateful** — The Conductor must remember the "state" of the entire symphony—where we are in the music and what happens next.                                                                                                                  |
| **Focus** | Built for **Task Automation**. Executes a specific system update or notification in seconds and then finishes its job. | Built for **Process Orchestration**. Manages long-running processes that span days or weeks, coordinating multiple Action Flows and human tasks over time.                                                                                      |

### Technical Capabilities and Connectivity
Now that you understand what an Action Flow is and how it differs from Process Orchestration, it's time to look under the hood. Action Flows are built for the modern enterprise, providing high-speed integration across your entire digital ecosystem.

#### Global Connectivity
Action Flows aren't limited to the Celonis platform; they are your bridge to the rest of the world.

- **1,000+ System Connectors**: Native, "plug-and-play" support for cloud and on-prem giants like SAP, Oracle, and Salesforce.
- **Universal HTTP**: If it has an API, you can connect to it. Use standard calls to trigger custom scripts in ML Workbench or any external web service.
- **On-Prem Agent**: Security is paramount. The On-Prem agent creates a secure "tunnel" to private networks, allowing you to reach systems behind corporate firewalls without compromising safety.

#### Enterprise Intelligence
A connection is only as good as the logic behind it. Action Flows process data with professional-grade intelligence.

- **Celonis Native**: This isn't just an "add-on." Action Flows can query Data Models, interact with Knowledge Models, or write back to Data Pools in real-time.
- **Native GenAI**: Stop building isolated bots. Embed intelligent reasoning, categorization, and summarization directly into any process step.
- **IT Governance**: Built for scale. Full SSO support, professional-grade monitoring, and comprehensive audit logs ensure every execution is accounted for.

Technical specs like 1,000+ connectors and GenAI logic are impressive on paper, but they exist for one reason: to solve complex business friction. Let's move from the *how* to the *where* and explore how this connectivity creates measurable value in real-life enterprise scenarios.


### outbound-connectivity
_**Hint:** Possible Questions: Explain the security and audit risks of using "Master Connections" versus Personal Dynamic Connections.

### Authentication, Authorization & Dynamic Connections
While Authentication and Authorization are general IT concepts, understanding the difference is key to building a secure architecture in Celonis.

#### The Definition
- **Authentication (Identity)**: Proving *who you are* (e.g., "I am Nicole, here is my password/token").
- **Authorization (Permission)**: Determining *what you are allowed to do* (e.g., "Nicole is allowed to read tickets, but not to act on them").

#### The Error Decoder
While building Action Flows, these terms help you debug instantly:

- **401 Unauthorized**: An **Authentication** failure. Your "key" is wrong, expired, or mistyped.
- **403 Forbidden**: An **Authorization** failure. Your "key" is valid, but you aren't allowed to perform that specific action or see that specific data.

Keep in mind, we'll have an entire course coming up on Error Handling in Action Flows!

#### Taking it Further: Static vs. (Personal) Dynamic Connections
In Action Flows, your choice of Connection is actually a choice in how you handle Authorization:

**Static Connections (The Service Account)**
- You authenticate once as a "System User." Every time the flow runs, it has the exact same permissions, regardless of who triggered it.
- **Best for**: Background automations and system-to-system syncs.
- **Note**: Even though we call it "System User", this could still mean that you use a personal account in your Action Flow setup, which the flow is using every time it executes. This also means that the person / the user whose account is used is logged every time as the "executing instance". This behaviour may not always be desirable, which is why you can also create… 👇

**Personal Dynamic Connections (User-Level Authentication)**
- The Action Flow requires the specific authorization of the person triggering it. It uses the **OAuth 2.0** handshake to act on behalf of that individual user.
- **Best for use cases where**: A clear audit log is required, and/or where manual actions are required, and security is strict. E.g., if a user isn't authorized to see "Salary Data" in the target system, the Action Flow will be blocked for them, too.


## Implement Multi-Select Table Actions
_**Hint:** Possible Questions: Contrast the behavior of "Collection" vs. "Single" input types to explain how Array Inputs enable an Action Flow to receive multiple records in a single execution.


## Establish a Connection between a View and an Action Flow
At this stage, you (should) have two assets in your Studio package:
- A **View** with a customer table.
- An **Action Flow** that already contains a basic "currency conversion engine".

### Our Use Case
For very peculiar reporting purposes, our View's business users would like to select one or multiple customers and, with the click of a button, convert each of the selected customers' total revenues into their (the customer's) local currencies.

The conversion results should, along with the values in the original currency (Euro), be sent via email to a given email address (your email address). This email should contain all of the initially selected customer revenues and their conversion results, no matter how many rows have been selected.

All we need to implement this use case are the two assets we already have in our training environment: the View and the Action Flow. Right now, no connection exists yet between our two assets, and they don't know how to communicate with one another. So let's start by building out exactly this connection.

### Step 1: Preparing the Action Flow
We will need to make adjustments on both sides to establish the connection between our two assets:
- The table inside the **View** requires an **Action** to be set up, which in this case will trigger an Action Flow.
- The **Action Flow** needs to know what data to expect from the "outside". We will leverage **Action Flow Inputs** for that purpose.

Inside the imported Action Flow, you'll find three predefined inputs:

| Input | Type |
|-------|------|
| CustomerName | Text |
| Country | Text |
| TotalRevenue | Number |

While the inputs are already mapped to the respective modules, make sure to still **initialize the modules** where needed. That includes:
- Setting up an **email connection**.
- Specifying **your own email address** to receive the test emails later on.

**Save, version, deploy, and activate** the Flow. Furthermore, ensure your Action Flow is scheduled to run **on-demand**. "Active" and "On-demand" are the two necessary conditions that need to be fulfilled for an Action Flow for it to be "visible" for other Studio assets like our View.

### Step 2: Adding the Table Action
Now, we head back to the View to create the Action button inside the table.

1. Enter **Edit Mode** in your View and select your **Table** component.
2. In the right-hand settings panel, look for a section labeled **Interactions** and add a new Action **'Run Action Flow'**.
3. Select the prepared Action Flow.
4. **Map the Action Flow Inputs.** We want the Action Flow to run using the data the user selects from the table. To make that happen, we need to map which column values fill which Action Flow input (automatically).
5. Give your Action Button a proper name.
   - This is what will be displayed in the table later on. As a best practice, always add a short **tooltip text** such that users of your View (and the table) easily understand what is happening when they click the action button.
6. Take note of the **filters** that can be applied to an action.
   - In this case, we don't need to configure a filter.
7. Click **Add** to finish the action setup.

Note that the appearance of the table has slightly changed: you can now **select multiple rows** from the table. Upon selecting at least one row, the new action button will appear.

### The First Test: Push the Button!
With the connection established, let's push the (action) button and see what happens…

1. Select some rows of your choice in your table and click your new action button. Upon execution, you should see a **"success"** message displayed on the screen.
2. **Check the Execution History:** Navigate back to your Action Flow and look at the history tab.
3. Also, open your **email inbox** to see what you have received.

If everything worked out as planned, you'll see **multiple executions** in the history list—one for every row you selected. And: Instead of a consolidated report, your inbox looks a little spammed with **one email having been received per row selected**…

**Every selected row has been treated as an independent trigger event.** While this may be desired for other use cases, our objective is to send a **single consolidated report**.

Let's see how we can change our approach (and our Action Flow) to get closer to our goal.

## Batch Processing with Array Inputs
To send a single, consolidated report and avoid spamming our inboxes, we need the Action Flow to **"collect" all selected data first** and process it as a single unit.

In the case of our Action Flow-View combination, we can achieve this by replacing our individual inputs with an **Array Input**.

> **Tip:** Bookmark the relevant documentation page for future reference on array inputs.

### Step 1: Updating the Input Architecture
An **Array Input** allows the View to pass all selected rows as an **array of collections** in one single execution cycle, where one collection reflects one row selected.

To switch to Array Inputs, let's:

1. Open your Action Flow and navigate back to the **Action Flow Inputs**.
2. **Delete** the three individual inputs.
3. Add a new Input of type **"Array"**: Name it `CustomerInformation`.
4. Configure the **"Item Specification"**:
   - Set the nested type to **Collection**.
   - Inside this collection, recreate our three data fields as three distinct items: `CustomerName` (Text), `Country` (Text), and `TotalRevenue` (Number).
5. **Save, Version, and Deploy:** Ensure the Action Flow is active so the View can "see" the new structure.

### Step 2: Enabling Batch Mode in the View
Of course, when we change the input structure of our Action Flow, we also need to make adjustments on "the other side", the View.

1. Go back to your View and edit the **Table Action**.
2. Notice that the three individual slots are gone. In their place is the `CustomerInformation` array. The individual revenue, country, and name inputs have now become **Array attributes**. Mapping these to the respective table columns is no different than before.

### Step 3: Iterator & Aggregator – The Logical Bookends
Because the Action Flow now receives **one "bundle" containing multiple packages** with customer information, we somehow need to account for this in our Action Flow logic. We still want to open and process every package (every collection) individually and only aggregate the processed results again into a single, consolidated output.

We will make use of two tools in Action Flows that usually work closely together: **Iterators** and **Aggregators**. Let's look at these two advanced flow control modules in more detail on the next page.

> **Tip:** Bookmark the documentation for future reference on Iterators and Aggregators.

## Control the Flow with Iterators and Aggregators
If you try pushing the button right now, it probably still works. However, when you open the hood and take a closer look, you will quickly notice that it doesn't give you the outputs (and emails) you would expect.

Since you're already somewhat experienced in building Action Flows, you will have a suspicion of what the issue is: Our previous inputs are no longer there, which means that the **mappings in our modules are broken**. You might just want to replace the previous mappings with the new array inputs, but that doesn't work. All you have at your disposal is just the `CustomerInformation` array...

When we use an Array Input, the Action Flow receives all selected rows wrapped in a **single consolidated batch of bundles**. However, processing modules—like our AI prompt and the HTTP currency converter—are designed to work on **one bundle at a time**.

To bridge this gap and access individual items in our `CustomerInformation` collection, we use two modules that act as the logical bookends of our process: the **Iterator** and the **Aggregator**.

### The "Exploder": The Iterator
The Iterator takes in an array with a series of bundles and outputs **every array item as a separate bundle**. In our case, it takes the `CustomerInformation` array received from the View and "explodes" it into individual bundles—in this case, individual customer information packages. If you select, for example, 5 rows in your table, the Iterator will produce 5 separate bundles.

To make the Array Input work for our Action Flow, let's add the "opening bookend":

1. **Add the Iterator:** Place it as the very first module in the Action Flow.
2. **Configuration:** In the "Array" field, map the `CustomerInformation` array from your Inputs.
3. **The Result:** Every module placed after the Iterator will now run once for every item in that list.

Now you can finally re-map the affected data pills in your Action Flow's modules with the outputs of the Iterator module.

> **Tip:** Remember to "Run the new Iterator module only" to make its outputs visible and available to map in the succeeding modules. A panel will open up that lets you insert dummy values for that purpose.

If you were pushing the button in the View right now (after you versioned and deployed the Action Flow again), you would still receive **two separate emails** (assuming two rows selected in the table). This is because so far we've only "exploded" the input array, but haven't yet tied the resulting individual bundles back together.

This is what we'll achieve with an aggregator tool in just a few moments. For practical purposes, though, we'll first do an intermediate data "clean up" step to make our lives easier once we get to the aggregator.

### The "Refiner": Set Multiple Variables
Inside the loop, our HTTP module fetches live exchange rates. However, API responses are sometimes "messy"—the value we need can, as in this case, be buried deep inside a complex JSON structure (e.g., `data -> rates -> GBP`).

To make our final report in our consolidated email clean, we use a **Set Multiple Variables** module to "catch" both the converted value as well as the identified currency and give them simple names.

**Why do this?**
- It allows the Aggregator to look for **clear variables** (like `Customer_Currency` and `Converted_Amount`) rather than trying to dig through raw API code for every single row.
- An alternative would be to create a single variable only and just map the converted value. The customer's currency, we technically already get from the AI module. We, however, deem the Action Flow logic to be a little more intuitive and easier to reverse engineer later on if needed.

Go ahead and add a "Set Multiple Variables" module in between your JSON and email module. Define two new variables, `Customer_Currency` and `Converted_Amount`. Try to figure out how to calculate the values.

> 👉🏼 **Tip:** Always feel free to version and deploy the current setup of the Action Flow and trigger an action from the View to fully comprehend what every adjustment we make results in! This is pretty much what you would do in reality, too.

### The "Collector": The Aggregator
Once the data is processed and refined, we (still) have multiple individual results floating through the flow. We need to **"re-pack"** them into a single summary that we can then push into a single email.

Let's put up the "closing bookend":

1. **Add the Aggregator:** Place a **Text Aggregator** after your "Set Multiple Variables" module. A text aggregator is a special type of aggregator that works best for our use case to pass its result on to the email module.
2. **The Source Module (Crucial):** Set the Source Module to your **Iterator**. This tells the Aggregator: *"Wait here until the Iterator has finished every item in the batch before moving forward."*
3. **Text:** We're going to map the "Clean" variables we just created (e.g., `Converted_Amount`, `Customer_Currency`) as well as two other data points we also want to include in our final email: the customer name and the original amount (both right away from the Iterator module).

For formatting purposes in our email later on, you should specify the following logic in the text field:

```
{{Iterator.CustomerName}}</td><td>{{formatNumber(Iterator.amount; 2; "."; ",")}}</td><td>{{formatNumber(SetMultipleVariables.ConvertedValue; 2; "."; ",")}}</td><td>{{SetMultipleVariables.CustomerCurrency}}
```

Also, just for formatting purposes, enable advanced settings, select **"Other"** as the Row separator, and specify the following as the separator:

``` 
</td></tr><tr style="border-bottom: 1px solid #eee;"><td style="padding: 12px;">
```

### Recap
Phew, this was quite a lot! Before we move on to the final edits, let's quickly recap what we did:

1. **The Start:** Receive 1 Consolidated Batch (Array Input).
2. **The Expansion:** The Iterator breaks it into individual rows.
3. **The Refining:** AI, HTTP, and Variable modules process and clean each row.
4. **The Collapse:** The Aggregator catches everything and turns it back into 1 text block.
5. **The End:** The Email module sends 1 consolidated report.

### Moving to the Final Result
Now that the data is being processed correctly, it's time to see the final output. On the next page, we will finalize the Email module and take a closer look at the "hidden" logic we included in the blueprint (like the JSON module and the Resume module) to handle those tricky data inconsistencies.

## The Masterpiece – A Resilient Batch Report
It's time to look at the final result! We're about to map your Text Aggregator output into your Email module! Once done, you should be receiving a **single, professional email** regardless of how many rows you select in the View.

1. **Open the Email Module:** Locate the "Body" or "Content" field.
2. **HTML Wrapping:** As we are building a modern table, paste the following HTML structure. Notice how we "wrap" the text aggregator result to complete the table:

```html
<h3>Converted Revenue Report</h3>
<table>
  <thead>
    <tr>
      <th>Customer</th>
      <th>Original (EUR)</th>
      <th>Converted</th>
      <th>Currency</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>
      {{Text Aggregator.text}} </td></tr>
  </tbody>
</table>
```

### Behind the Scenes: What Makes it Work? 🕵️
While you focused on the connection and the batch architecture, the blueprint you imported contains "hidden" logic designed to handle real-world data issues. Let's look "under the hood" at why this flow is so resilient:

#### 1. AI-Powered Data Enrichment
In your table, "Country" might be a full name like "United States" or a code like "US." Our Currency API, however, strictly requires **3-letter ISO Currency Codes** (like USD or GBP).

**The Logic:** The AI Prompt acts as a **translator**. It takes whatever "raw" country text comes from the View and converts it into the specific currency code the API expects. A very precise instruction on the expected output is key in the prompt here.

#### 2. Handling "Same-Currency" Errors
A common "trap" in automation is trying to convert a currency into itself (e.g., EUR to EUR). The Frankfurter API will, in this case, throw an error and stop the entire flow.

**The Logic:** We implemented an **Error Handler** (the Resume module) on the HTTP module. If the API fails because no conversion is needed, the flow doesn't crash. It simply bypasses the error and uses the original Revenue value for the report.

#### 3. Establishing common grounds with the JSON module
Notice how we kept the "Parse response" option in the HTTP module to **"No"**. This is mainly due to the Resume module and the kind of "stand-in" output it produces. To continue the flow based on common grounds, no matter whether the HTTP module or the Resume module was executed, we outsource the parsing of either one of the outputs to a **separate JSON module**. If this is a little hard to grasp, we recommend you experiment a bit yourself with different setups (set "Parse response" to yes, then trigger an error, etc.). This way, you will probably come to the same result we present to you in the blueprint.

### The Final Verification 👀
It is about time! Go to your View and select a mix of customers: some who need conversion (e.g., Canada, UK) and some who don't (e.g., Belgium).

1. **Push the Button.**
2. **Check your Inbox:** You should receive a **single email** with a perfectly formatted, clean table where every row - even the "errors" - has been processed successfully.

## Summary & Best Practices
Congratulations! You have moved from simple triggers to a sophisticated **Batch Processing Engine**.

**Key Takeaways:**
- **Table Actions** turn static insights into immediate execution without leaving the Celonis View.
- **Array Inputs** are the "consolidated package" of Action Flows. They allow you to process multiple rows as a single unit, preventing, e.g., inbox spam.
- The logic of **Iterator → Processing → Aggregator** is the gold standard for handling batch data (think "diamond shape").
- **Data Refinement:** Using a Set Multiple Variables module makes your logic easier to read and maintain.

### Pro-Tip: Controlling Access to Table Actions
Not every View user should necessarily be able to trigger the underlying Action Flow. You can control the visibility of your Table Actions by managing **(Action Flow) Asset Permissions**.

A Table Action button will only appear for users who have the explicit right to **"Use"** the connected Action Flow. If a user lacks this permission, the button is automatically hidden from their View, ensuring that sensitive actions (like updating an ERP system or sending an email) are restricted to authorized personnel.

To review or restrict access:

1. In Studio, click the three dots (⋮) next to your Action Flow asset.
2. Select **Permissions**.
3. Assign the **"Use"** permission only to the specific users, groups, or applications that require it.

For example, in the "Use" Asset Permissions settings for an Action Flow called "Currency conversion service", the application "Call Process Copilot" and the user "Nicole Wendler" have the "Use" Asset Permission enabled. In contrast, the user "Celonis Training" would not be able to see or use a button in a View that is linked to this particular Action Flow.

> **Note:** The above sample permission assignment cannot be performed in the central training team.

### 💡 Outlook: Beyond the Table
While we focused on triggering flows from specific rows in a table, Celonis Studio offers two primary ways to engage with your automations:
- **Table Actions**
- **View Actions**

**Table-Specific:** As you've seen, these are perfect for when you need to "pass" specific data points (like Customer Name or Revenue) from a selected row directly into your flow.

## Trigger Action Flows based on Process Insights

### Celonis Triggered Use Cases in Action
Let's look at how native integration transforms process insights into immediate business value. These examples move from foundational automation to sophisticated, cross-process synchronization.

### Stop Duplicate Invoices in Accounts Payable
There is a broad spectrum of use cases in the Accounts Payable process where automation with Action Flows adds substantial value. Action Flows, for example, help to:
- Increase **on-time payment** by addressing inefficiencies like late vendor invoices or payment blocks.
- Maximize gains through **cash discounts** by acting on lacks of invoice prioritization.

What we are going to take a closer look at is how Action Flows serve as the **"Automated Responder"** in the Duplicate Invoice Checker App. While other components "think" and "detect," the Action Flow is the only part that **"acts"** by reaching into your ERP system to prevent a financial loss.

It is critical to distinguish between the **Detection Logic** that identifies a potential duplicate and the **Operational Response** that follows.

**How is a duplicate identified?**
In the object-centric version, the "brain" uses an **AI Annotation service** to process your data in two layers:
- **The Algorithm Layer:** Using predefined search patterns (like Similar Reference or Vendor Fuzzy), Celonis groups invoices that look like duplicates.
- **The Intelligence Layer:** A built-in Machine Learning model assigns a **Confidence Score** to each group, predicting how likely it is to be a true duplicate.

These signals are attached to your Invoice objects as **Augmented Attributes**.

> For additional information on the Duplicate Invoice Checker app, feel free to check out our course on Celonis Academy!

### Optimizing Master Data Lead Times in Procurement
While the Duplicate Invoice Checker is about financial precision, Action Flows can also be used to improve **Supply Chain Reliability**. Supply planning relies heavily on master data assumptions - specifically, the **"Planned Lead Time"** or how long it takes to receive a product. When these assumptions don't match reality, it causes stockouts and production delays.

**Analyzing Performance & Syncing the System**
The "intelligence" here is driven by **Object-Centric Logic** that automatically tracks a supplier's actual delivery performance over time. By comparing the "Planned Lead Time" in the ERP to the actual "Goods Receipt" dates, the system detects when a vendor repeatedly misses expectations.

Instead of a manual audit, Celonis can calculate a new, accurate lead time based on historical data and required safety buffers, **annotating the vendor record with a suggested update**.

### AI Credit Blocks Manager & Order Management
While updating lead times ensures that your internal planning is reliable, Action Flows are equally vital for **customer-facing acceleration**. In Order Management, the goal shifts from maintaining data integrity to **removing friction** to speed up the flow of goods.

A perfect illustration of this is the **AI Credit Blocks Manager**. Here, instead of updating a date or stopping a payment, we are focused on **releasing a Sales Order** that has been held at the credit check stage.

**Evaluating the Risk**
The "logic" in this app analyzes the **credit risk** of a customer in real-time. It looks at the Accounts Receivable data - such as recent payments or credit limit utilization - to determine if a block is still justified.

**Executing the Release**
Once the intelligence indicates an order is safe to ship, the Action Flow takes over to handle the manual overhead of updating the ERP. Its role is to bridge the gap between a "cleared" credit status and the actual shipping process:
- **Automated Status Update:** It writes directly back to the ERP to remove the credit hold, enabling the order to move to the next stage of fulfillment.
- **Instant Communication:** It can trigger notifications to Sales and Logistics teams via email or Slack, confirming that the order is back on track.
- **Process Continuity:** It ensures that once a decision is made in Celonis, it is reflected globally across all systems without delay.

The **AI Recommendation engine** then flags orders that are safe to proceed. It provides the **"Go/No-Go" decision** based on the most up-to-date financial data, ensuring that credit managers only spend time on truly high-risk cases.

### The Brain: Implementing the Intelligence
You didn't click on this course by accident; your brain signaled your hand to move. In Celonis, **Action Flows are the muscles**: they handle the heavy lifting and execution, but they don't decide when to act. They require a **"brain"** to analyze the data and send a trigger signal. Let's look at the technical components that make this brain-muscle connection possible.

If you want the muscle comparison even further: Action Flows are like our **"type II", fast-twitching muscles**, which are specialized for short, high-intensity, and explosive movements like sprinting or jumping.

The counterpart, **"type I", slow-twitching muscles** specialized for long-duration activities, would in the Celonis universe be **Process Orchestrations** powered by the Orchestration Engine.

#### The Modes of Logical Processing
Depending on the complexity of your process, the "Brain" uses different levels of logic to reach a conclusion:

**The Reflexive Brain** *(i.e., Filtered Data Model)*

This is the most straightforward form of "thought." It uses standard **PQL filters** to identify specific data states.
- **How it works:** The system identifies rows that meet a basic criterion - for example, "An invoice where the Net Payment Date is in the past and the status is still 'Open'."
- **The Conclusion:** It concludes: "This record is overdue and requires an immediate follow-up."

#### Beyond Augmented Attributes
Above, we're referring to the MLWB writing back to Augmented Attributes since this is a common pattern for integrated apps. It is important to recognize that, depending on data volume, performance requirements, and the actual use case, the MLWB could, for example, also send an **HTTP request directly to an Action Flow's webhook URL**, triggering it immediately with a specific payload. In this scenario, any information sent exists only for the duration of the Action Flow's execution and is **not persisted in the Data Model**.

#### 💡 Why separate the "Brain" from the "Muscle"?
- **Efficiency:** Your Action Flow muscle only consumes energy once a conclusion is already reached and a contraction is necessary.
- **Consistency:** Multiple Action Flows can listen to the same "Conclusion." One flow might block a payment, while another sends a Slack alert - both reacting to the same signal.
- **Auditability:** You can look at your Data Model and see exactly why a muscle contracted by reviewing, e.g., the assigned confidence score or an annotation flag.

#### Up Next: The Receptor
Now that the Brain has concluded, we need to configure the **"Receptor"** that feels that change and carries the impulse forward.

### The Receptor: Defining the Trigger
If the brain is where the conclusion is reached, the **Trigger** defined in the Knowledge Model is the **receptor**. It is a specialized sensor sitting directly on top of your Data Model, waiting to "feel" the specific signal - the surgical instruction - that the brain just wrote.

We define the Trigger in the **Knowledge Model** to ensure that the logic for *when to act* is governed in the same place as your KPIs and other business rules.

To create new Triggers, simply navigate to the section labelled **'Triggers'** in the Knowledge Model. You can choose between two different types of triggers:
- **Data Model Triggers** — based on the Data Model.
- **Record-based Triggers** — based on a given Record.

> Whenever possible, go for **Data Model Triggers** as Record-based Triggers are only maintained to support legacy functionality.

When configuring a Trigger, you establish the bridge to the brain by selecting, for example, the specific **augmented attributes** or a **"log" table** that your logic (like a MLWB script) generates. For simpler use cases, you might just select a regular table from the Data Model.

Whether or not you add a **filter** to your Trigger depends, as always, on your use case as well as the logic built, for example, in the MLWB script and its resulting table(s) or attribute(s).

Once a new trigger is created, **versioned, and deployed**, it can already be connected in an Action Flow!

#### The Anatomy Recap
- **The Brain:** Decides a lead time should be 14 days and writes it to an attribute.
- **The Receptor:** Feels the value "14" appear in that attribute and sends an electrical impulse forward.

#### Next Step: Move the Muscle
Now that the receptor is tuned and deployed, we move into the Action Flow editor to set up the **"muscle"** that will receive this impulse and execute the work.

### The Muscle: Executing the Action Flow
Now that the signal has been sensed and passed through the nervous system, it reaches the Action Flow. In our anatomy, the Action Flow is the **Muscle**. It doesn't "think" about whether to act - it simply receives the impulse and executes the physical work.

#### Step 1: The 'Watch Trigger' module
This module is the connection point where the Action Flow connects to the Knowledge Model.
- **The Impulse:** The moment the Receptor fires, this module wakes up the Action Flow.
- **The Payload:** It receives a small packet of data, usually containing the **Unique ID** (e.g., Invoice Number) of the object that needs attention.

Based on your experience with building Action Flows, you already know that you usually want to **"Run a module once"** to be able to map its outputs in succeeding modules. To do this for the "Watch Trigger" module, initialize it so its outputs become available for mapping.

#### Step 2: The 'Get Rows' module
At this point, the muscle knows which data to act on, but it doesn't necessarily always have all the data it needs from the Data Model - this directly depends on how you've configured the trigger and whether it sends only a table record's ID or additional data.

For the most common case that the trigger only receives a **partial payload** (like just the ID), we use a **Get Rows** module to pull the specific attributes we need for our Action Flow to fulfill its purpose.

#### Step 3: Running the remaining Action Flow
This is the **physical work**. With correct data in hand, the Action Flow executes whatever has been defined for it, like pushing the update to the ERP system or blocking a payment. The cycle is complete: an analytical conclusion has become a real-world result.

#### The Anatomy Recap
- **The Brain (MLWB/Annotation):** Decides the lead time should be 14 days and writes it down.
- **The Receptor (Trigger):** "Feels" the update and fires an impulse.
- **The Muscle (Action Flow):** Receives the impulse, grabs the "14 days" instruction, and updates the ERP.

### Closing the Loop
Congratulations! You have successfully mapped the journey from a raw data point to a real-world execution. By separating the **Brain**, the **Receptor**, and the **Muscle**, you have moved away from "Standalone Automations" toward **Integrated Process Intelligence**.

#### The Integrated Architecture at a Glance
| Component | Responsibility | Technical Location |
|-----------|----------------|--------------------|
| **The Brain** | Analyze data and reach a conclusion. | MLWB / Annotation Builder |
| **The Synapse** | Store the "Surgical Instructions." | Augmented Attributes / Signal Tables |
| **The Receptor** | Sense the conclusion and fire an impulse. | Knowledge Model Trigger |
| **The Muscle** | Receive the impulse and execute the action. | Action Flow |

You are no longer just "building Action Flows." You are designing an **integrated, intelligent system**. By keeping the Logic in the Brain (KM/MLWB) and the Action in the Muscle (Action Flow), you create a system that is:
- **Transparent:** Everyone can see why an action happened.
- **Scalable:** One Brain can feed multiple Muscles.
- **Resilient:** If one part of the system is paused, the data remains safely stored in the Synapse.

#### What's Next?
Now that you've mastered **Autonomous Intelligence**, it is time to keep exploring with Action Flows for your own business use cases! Make sure you've completed all materials from the **"Build Action Flows"** Training Track to make sure you're equipped with all the skills and tools you need to get started in the real world.


## Integrate Action Flows with Process Orchestration

### Welcome!
Automated business processes are rarely single, isolated events. In complex business environments, a task like "Vendor Onboarding" might span several days, involve multiple documents, and require updates across various systems.

To manage these long-running sequences, we use **Process Orchestration**. In these setups, the Process Orchestration asset manages the **overall timeline**, while Action Flows execute **specific, automated steps** when called upon.

This microcourse focuses on how to technically prepare an Action Flow to function as a reliable step within an orchestrated process.

### The Role of Action Flows: GC Contenders vs. Sprinters 🚴
To understand how these assets work together, think of a professional cycling team in a Grand Tour like the Tour de France:

- **Process Orchestration is the "GC Contender":** This rider is focused on the General Classification - the overall marathon. They maintain a steady, high-performance state over 21 days of racing. They are **stateful**, meaning they manage the overall journey and "remember" the progress from start to finish.
- **Action Flows are the "Sprinters":** For most of the race, these riders are "invisible," tucked away in the peloton to save their energy. They only move to the front when a specific milestone or finish line appears. They provide an explosive, high-wattage burst of speed to complete a task - like updating an ERP or running a risk check - and then they immediately retreat. They are **stateless**, built for speed and specific outcomes, not for the long haul.

### What you will learn
By the end of this microcourse, you will be able to:
- **Create** an Action Flow from inside a Process Orchestration and explain the auto-generated Action Flow setup.
- **Retrofit** existing Action Flows to manually establish the technical handshake to a Process Orchestration asset.
- **Launch** a Process Orchestration flow with the help of Action Flows.

### Build Orchestration-Ready Action Flows
Imagine we're automating a **Vendor Onboarding Process** with Celonis - more precisely, using a Process Orchestration asset.

Its first major milestone is a **Form step**, where it is currently waiting for a prospective vendor to submit their tax and banking details. This is the "endurance" phase of the process: the Orchestration asset maintains the **state** of this specific onboarding instance for hours or even days.

However, the moment the vendor clicks "Submit," the process reaches a point that requires an immediate, automated action: a **Risk Check**.

To handle this, the Orchestration triggers an Action Flow. This flow acts as a **"sprinter"** - it powers up to execute a high-speed task, verifies the Tax ID against an external database in seconds, and passes the result back to the process. Once the task is complete, the Action Flow shuts down, and the Orchestration continues its steady pace toward the final manager approval.

#### The Fast Track: Creating New Action Flows as Process Orchestration Steps
The most efficient way to build this Risk Check Action Flow is to **create it directly from the Process Orchestration editor**. When following the regular flow to add a new Process Step, you're automatically guided towards an option to create a **"New Action Flow"**.

An Action Flow that is created from within a Process Orchestration asset is **not empty** but comes with prepopulated modules that are essential for the Process Orchestration asset to be able to communicate with the Action Flow asset:

- **Get Process Context:** This module allows the Action Flow to "pull" data from the running process instance - specifically, the `Tax_ID` submitted in the vendor's form.
- **Completion Event:** This is the signal that the Action Flow has completed its task and that the Process Orchestration can proceed to the next process step. In our example, once the risk check is finished, the Action Flow uses this module to send the risk score back and tell the Orchestration to move to the next step.

What if you want to connect an **already existing** Action Flow, though? It is, of course, possible, but you'll need to add those modules above manually, along with an input reflecting the **Digital Process Instance ID**.

Let's look at those details on the next page.

### Retrofitting Existing Action Flows for Process Orchestration
If you want to use an existing Action Flow, you need to manually **"retrofit"** it to join the orchestrated process. Because this flow wasn't created inside the Orchestration editor, it lacks the necessary **"handshake"** configuration.

#### The dpInstanceId Input
If you look closely at an Action Flow that has been created directly from inside a Process Orchestration asset, you will notice it comes with an Input called `dpInstanceId` (Type: Text). This is the technical name for the **Digital Process Instance ID**. It can be found in the regular Inputs section and is auto-mapped to the 'Get Process Context' and 'Completion Event' modules.

As this name suggests, this Digital Process Instance ID identifies the **specific process instance** that triggers a given Action Flow. It acts as the "handshake" that bridges the gap between the two assets. Without this ID, the Get Process Context module cannot locate the correct data, and the Completion Event won't know which process instance to update.

> **Note:** Correct spelling is critical. Ensure the variable is named exactly `dpInstanceId`.

#### The Get Process Context and Completion Event modules
The two modules, which are by default added to any Action Flow that you create from within a Process Orchestration, also need to be added to **any existing Action Flow** that you want to use in conjunction with a Process Orchestration. Both modules leverage the Digital Process Instance ID in their configurations.

Both modules `Get Process Context` and `Completion Event` have a dedicated configuration field called **'Digital Instance Process ID'** to map the `dpInstanceId` variable to.

Without the `dpInstanceId` and the Completion Event, the Action Flow has no way to signal back to the Orchestration that its task is finished. The process would simply hang in a **"Waiting" state forever**, even if the Action Flow successfully performed the risk check.

> For additional information on these modules, check out the documentation as well as our online course **Orchestration Engine Fundamentals**.

#### Scheduling and Activation Requirements
An Action Flow will only be **visible and selectable** within the Process Orchestration UI if it meets these three requirements:

1. **Scheduled to On Demand:** The flow cannot run on a schedule. It must be set to **On Demand** so the Orchestration can trigger it exactly when the form is submitted.
2. **Versioned and Deployed:** The Orchestration Engine only interacts with versioned and deployed (previously "Published") versions. Drafts will not appear in the selection menu.
3. **Active:** Only an active Action Flow can be added as an action in Process Orchestration. Any versioned and deployed Action Flow can be activated from within the Process Orchestration editor, too.

### The Grand Départ
We have explored how to configure Action Flows as steps within a process, but how does the **GC Contender** actually begin its race?

A Process Orchestration asset requires a **trigger** to create a new instance. While there are several ways to kick off an orchestrated process flow — such as an **Event Endpoint** call for system-to-system triggers or the outcomes of an **AI Annotation Builder** — a common method for building a **human-in-the-loop** bridge is a dedicated Action Flow.

#### The "Start New Orchestration" Module
To allow a user to kick off a process directly from a Celonis View, you build a **"Trigger Flow."** This is a simple Action Flow that acts as the bridge between a manual action in a Celonis View and the Process Orchestration asset.

- **The Action Button:** You place a button in a Celonis View (e.g., "Start Vendor Onboarding").
- **The Action Flow:** This button is linked to an Action Flow that contains the **Start New Orchestration** module.
- **The Action:** When the user clicks the button, the Action Flow executes, and the module tells the connected Process Orchestration to create and launch a new process instance immediately.

#### Why use an Action Flow for the Grand Départ?
Using an Action Flow as the starting mechanism provides two major advantages:

- **Initial Data Mapping:** You can take data from the Celonis View (like a `Vendor_Name` or `User_Email`) and pass it through the Action Flow directly into the Process Orchestration's initial variables.
- **Pre-Run Validation:** The Action Flow can perform a quick check (e.g., "Does this vendor already have a pending application?") before deciding whether to actually launch the full orchestration.

#### Alternatives to Trigger Process Orchestrations
While we focus on the Action Flow bridge here, it is worth noting two other ways an orchestration can begin:

- **AI Annotation Builder:** You can link an AI Annotation Builder asset directly to the start event of a Process Orchestration asset. As the AI Annotation Builder analyzes and classifies objects such as incoming customer emails or support tickets, its annotations can automatically launch a new process instance.
- **Event Endpoints:** This is the technical entry point for external systems. It allows a webhook signal from a third-party application (like an ERP or CRM) to act as the trigger that initiates the orchestration.

### The Finish Line
Congratulations! You've successfully navigated the technical journey of connecting the **GC Contender** (Process Orchestration) with the **Sprinter** (Action Flow). By mastering the handshake between these two assets, you've moved from building isolated automations to designing **resilient, long-running business processes**.

#### Reviewing Our Objectives
Let's look back at the goals we set at the beginning of this micro course:

- **Create and explain the Auto-Generated Setup:** You've seen how the "Fast Track" creation method automatically provides the `Get Process Context` and `Completion Event` modules, serving as the essential technical handshake for your automation.
- **Retrofit Existing Action Flows:** You can now manually establish the technical handshake by adding the `dpInstanceId` input and mandatory modules, ensuring any existing Action Flow can join the orchestrated process.
- **Launch a Process Orchestration Flow:** You understand how to use the `Start New Orchestration` module in an Action Flow to act as the **"Grand Départ"** - bridging the gap between a manual click in a View and the beginning of the Process Orchestration.

#### Final Checklist for Your Next Build
Before you launch your next orchestrated process, run through this quick pre-race check:

- [ ] Is your Action Flow **Active**? (The toggle on the overview page must be set to Active).
- [ ] Is it **On Demand**? (Scheduled flows cannot be used as orchestration steps).
- [ ] Is the **latest version deployed**? (The Orchestration Engine only sees versioned and deployed versions).
- [ ] Is `dpInstanceId` **spelled correctly**? (Case sensitivity matters!).

> Last but not least, remember to pay our Celonis Academy another visit to learn everything about **Orchestration Engine Fundamentals**!
