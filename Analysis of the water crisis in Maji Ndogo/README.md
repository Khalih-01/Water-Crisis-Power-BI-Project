# Analysis of the water crisis in Maji Ndogo

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/title.png"/>

## Introduction 
In Maji Ndogo and across the world, access to clean and reliable water sources is a fundamental aspect of daily life. This project aims to create a report to showcase insight into the Maji Ndogo water crisis to stakeholders.

## Problem Statement

A terrible drought made clean water a luxury, Every day is a struggle as people queue for hours often in vain for their share of life’s most basic necessity, A legacy of mismanagement and corruption choked off Maji Ndogo’s lifeblood, leaving its water infrastructure in ruins. But dawn followed the darkest night , This government is guided by the principles of transparency embracing a future driven by data and truth. Thus giving me a mission to help restore the flow of water in Maji Ndogo.

Data needed to inform our decisions, a sweeping water survey across provinces, towns and countless water sources will map out Maji Ndogo’s thirst.

#### Stakeholder Requirements
Our first user is a **President**.

Their user story is: As a leader of a nation  I want to understand the costs at a provincial level, and also understand what the different improvements will cost us.

1. See the key points of the survey results so I understand the overall status of water access in Maji Ndogo.
2. Know how many people are affected by water access challenges in Maji Ndogo and what those challenges are. 
3. Know how much money we will need to complete the upgrades, and where that money needs to be spent.
4. Understand this data on a national level and a provincial level.

Our second user is a **provincial leader**. 

Their user story is: As a leader of a particular province, I want to see data only relevant to my province. I need to understand the state of water access in my province, the scope of work we have to complete, and understand the financial aspects related to the improvements.

1. Total people served for each water source type in a province. 
2. Number of water sources, their type, and whether it is rural or urban.
3. Show the relevant stats for towns in that province.
4. Add relevant provincial data. Queues, gender compositions and crime, broken taps by town, etc., in provinces where it is relevant. 
5. Summary of improvements and costs.

## Skills Demonstrated
The following power Bi features were incorporated 
-	DAX
-	Measures
-	Bookmarks
-	Page Navigation
-	Data Modelling
-	Filters and Slicers 
-	Tooltips
-	Buttons

## Data Sourcing 
The data collected on water sources and water collection in Maji Ndogo provide us with a deeper understanding of the daily life of its inhabitants and the critical role water plays in their lives.

Data was sourced from ALX Africa/ExploreAI.

[Link to dataset](https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Md_water_services_data.xlsx)

It contains 8 sheets/tables
- well_pollution
- water_source
- visits
- queue_composition
- project_progress
- location
- infrastructure_cost
- water_source_related_crimes

**_Disclaimer_**: _All datasets and reports do not represent any company, institution or country, just a dummy dataset._ 

## Data Modelling


Automatically derived relationships are adjusted to remove and replace unwanted relationships with the required

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Model.png" />

The model is a multi star schema 
There are 4 dimension tables and 3 fact table, the dimension tables are all joined to their related fact table with a one to many relationship 


## Visualisation

I created a report that followed the stakeholder requirements.

The report comprises of two pages 
1.	National
2.	Province info (which one can navigate to using the drill through feature by right clicking province on the national page)

National | Province info
:-----:|:-----:
<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20image%204.PNG"  />|  <img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20Image%206.PNG" /> 
<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20Image%205.PNG" /> | <img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20image%207.PNG" /> 

Here is a video showing how to interact with the visualization


https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/assets/114422925/559e24ed-9b89-4081-8466-c7faa12836fc


[Click Here to see how i created the visualization](https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/How%20I%20created%20the%20visualization)






