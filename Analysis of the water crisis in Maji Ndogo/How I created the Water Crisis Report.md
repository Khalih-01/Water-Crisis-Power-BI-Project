https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/assets/114422925/559e24ed-9b89-4081-8466-c7faa12836fc

### National page

I started to create the visualization by looking at the stakeholder requirements from the National leader 

Lookng back at the Requirements, we see 3 components; 
- Population/water breakdown: "What do we need to do?", and "How much will it cost?".
- Population : Population affected per province and Population affected per water source
- Improvements: Improvements needed per province and Improvements needed per water source
- Budget : Budget for province and Budget for improvements 

So I split my dashboard into three components, but also reserved some space for slicers somewhere, and reserve some space for the big idea results that are linked to the purpose: "How much do we need to spend in Maji Ndogo, and what will that money do?" 

This is my draft. 

[pic of dashboard build]

I also added a map. So now, when we select a province in the slicer, the map highlights where that province is 
I created a new Shape map visual from the Visualisations tab, Since Maji Ndogo isn't well known, we have to use a custom map to visualise the data. Here's the link to download the JSON map file and an image of Maji Ndogo's map we're going to need ().

[pic of national page]

I used a bit of DAX to aggregate all of the Install l taps – Install 8 taps values into one called Install public tap(s)*, and shortened Diagnose local infrastructure too. This was in an effort to categorize all the improvements, improvement type
Here is the DAX I used in project_progress. 

[Picture of DAX]

Project planners thought through the costs a bit more and realised that rural water sources are much harder to improve than urban ones. So, they suggested that I add 50% to the cost of any rural source's improvement budget. So I needed to increase the Budgeted_improvement_cost by 50%. I called it Rural_adjusted_cost.

[Picture of DAX]

Next up, Budgeted_improvement_cost. Now that I know the cost of each improvement, I updated the project_progress table with a new column that calculates the cost of each improvement, based on the type of improvement, and whether it is rural or not. 

[Picture of DAX]

The next column I needed to create is Basic_water_access. How will I know if the project was successful? 
We can classify water sources according to the UN requirements: 

[pic of UN requirements]

In order for a water source to be classified as basic, it must satisfy these requirements: 
•	Rivers are not improved sources, so they are not included. 
•	Wells are improved, only if they are clean. So all contaminated wells are excluded. 
•	Public taps are improved sources, but only if the queue time is less than 30 min. 
•	Broken infrastructure "taps" are not basic, because they do not work. 
•	All taps installed in homes across Maji Ndogo are at least basic. They are actually safely managed. 

Once I know the water access level, I can estimate how many people's lives we will improve by upgrading all of the water sources. 
So, I needed to first calculate where the basic access level is, and as repairs are made, we will hopefully get that number close to 100% access. This is the goal! So if money is spent on this project, how water access improves can be measured, to make sure what is being done is making a difference. 

Therefore, the idea is to calculate the number of clean wells, the number of public taps with queue times < 30 min, and taps in homes, then use that to calculate how many people have access to basic water.

I broke it into two steps:

1. Classify sources as Basic Access or Below Basic Access in a new column. 
•	To get the queue time of a shared tap, shared taps were visited multiple times, so average
•	For wells, Check if it is polluted from the well_pollution table, using a lookup. 

2. Sum up all of the people using a basic water source, divided by the total population.

Step 1A, Calculate the average queue time for each source. This means I needed to aggregating  per source.

[Picture of DAX]

Step 1B, I needed to create the control flow logic to check wells and taps to classify them as being basic or not. 
We classify each source as being basic or below basic. 

[Picture of DAX]

Step 2, the final step is to create a new measure that calculates the basic water access level as the number of people who have basic access to water divided by the total number of people in Maji Ndogo. 

[Picture of DAX]


