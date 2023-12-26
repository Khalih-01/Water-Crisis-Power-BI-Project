# How I Created the Water Crisis Report

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/intro.png" />

## National page

I started to create the visualization by looking at the stakeholder requirements from the National leader 

Lookng back at the Requirements, we see 3 components; 
- Population : Population affected per province and Population affected per water source
- Improvements: Improvements needed per province and Improvements needed per water source
- Budget : Budget for province and Budget for improvements 

So I split my dashboard into three components, but also reserved some space for slicers somewhere, and reserve some space for the big idea results that are linked to the purpose: "How much do we need to spend in Maji Ndogo, and what will that money do?" 

This is my draft. 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Dashboard%20Build.PNG" />

I also added a map. So now, when we select a province in the slicer, the map highlights where that province is 
I created a new Shape map visual from the Visualisations tab, Since Maji Ndogo isn't well known, we have to use a custom map to visualise the data. Here's the link to download the JSON map file and an image of Maji Ndogo's map we're going to need ().

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/National%20Page%201.PNG" />

I used a bit of DAX to aggregate all of the Install 1 taps – Install 8 taps values into one called Install public tap(s)*, and shortened Diagnose local infrastructure too. This was in an effort to categorize all the improvements, improvement type
Here is the DAX I used in project_progress. 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Aggregated_Improvement%20DAX.PNG" />

Project planners thought through the costs a bit more and realised that rural water sources are much harder to improve than urban ones. So, they suggested that I add 50% to the cost of any rural source's improvement budget. So I needed to increase the Budgeted_improvement_cost by 50%. I called it Rural_adjusted_cost.

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Rural_adjusted_cost%20DAX.PNG" />

Next up, Budgeted_improvement_cost. Now that I know the cost of each improvement, I updated the project_progress table with a new column that calculates the cost of each improvement, based on the type of improvement, and whether it is rural or not. 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Budgeted_improvement_cost%20%20DAX.PNG" />

The next column I needed to create is Basic_water_access. How will I know if the project was successful? 
We can classify water sources according to the UN requirements: 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/UN%20water%20requirement.png" />

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

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Average_queue_time%20DAX.PNG" />


Step 1B, I needed to create the control flow logic to check wells and taps to classify them as being basic or not. 
We classify each source as being basic or below basic. 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Basic_water_access_check%20DAX.PNG" />

Step 2, the final step is to create a new measure that calculates the basic water access level as the number of people who have basic access to water divided by the total number of people in Maji Ndogo. 

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Basic_water_access_level%20DAX.PNG" />

Ok, so now we have calculated two things; how much will all of these upgrades cost (Budgeted_improvement_cost), and what will be the impact (Basic_access_water_level)? 


For the last part of the national page 

-	What will this cost (Budget by province, Budget by improvement type)

Now in the third block I want to give the President all of the financial information needed to make decisions. The president will want to understand the costs at a provincial level, and also understand what the different improvements will cost us 

Since The president will have to send the local provinces some funds, I need to  create a budget table. The downside is that tables struggle toshow a part-of-a-whole story, let's visualise the budget too. 

Instead of trying to cram all of the information into the third block, I made a bookmark! I added a button that will toggle between the Province and Improvements tables. This way the user can choose which data to focus on. 

Here are some images for the buttons:

Province | Improvement
:-------:|:-------:
<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Toggle_button_province.png" /> | <img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/Toggle_button_improvement.png" />

I created two bookmarks, Province and Improvements. For the Province bookmark, I hid the Improvements_table, and for Improvements I hid the Province_table and province pie chart, The buttons will allow me to toggle between these two bookmarks. 
I used the selection and bookmarks panes to add two buttons that toggle between Province and Improvements bookmarks. 
I followed the following steps in order to create the functional buttons
1.	Name the visuals, buttons, and images properly. 
2.	Add two buttons and add the two images into the buttons.
3.	Use the selection pane to display and hide the elements that don’t need to be seen in the  bookmark. 
4.	The button showing in the Province bookmark should open the Improvements bookmark and vice-versa. Use this to set the actions. 
5.	Make sure the buttons are in front of your images. Move elements up and down the selection pane to do this. 
6.	Test buttons to see if they work

Province | Improvement
:-------:|:-------:
<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/National%20Page%202.PNG" /> | <img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/National%20Page%203.PNG" />

Next to our heading, I added a placeholder for some high-impact statistics.  needs to know how much money we will need, and what problem the money will solve. So the total cost is a key metric I wanted to display. 

I added cards with the total cost of upgrades and the current percentage of basic access to water.

<img src="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/How%20I%20created%20the%20Report%20images/National%20Page%204.PNG" />

## Province Info Page

Now we have built the National level report, but we still need to make one for each province. For example, what would the provincial leader of Amanzi need to know? At a minimum, a breakdown of the budget for each town (quantity and cost), the two visuals showing the urban/rural split and the budget are needed.

By using the drill through feature in Power BI, I connected the province info page to the national page which then allows for navigation to the province info page by right clicking on a province. Now, when you're looking at the big picture on the national page and you're curious about a specific province, you can just right-click on it. This magic click takes you straight to the detailed province info page. It's like zooming in to get a closer look at the details you want.

National Page | Province Info Page
:-------:|:-------:
<img src ="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20Image%205.PNG" /> | <img src ="https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/blob/main/Analysis%20of%20the%20water%20crisis%20in%20Maji%20Ndogo/Images/Water%20Crisis%20Viz%20image%207.PNG" />

https://github.com/Khalih-01/Water-Crisis-Power-BI-Project/assets/114422925/559e24ed-9b89-4081-8466-c7faa12836fc

