
# Analysis Part One - Trips and visualization of data

#### SESSION BY INSTRUCTOR: 
_The instructor will start of by giving you an introduction to the topic. After the lesson the participants will recreate the analysis made in class._

#### Agenda 

- How to create and preview analysis
- Tiles: create, scale, customize appearance (header, background, etc.)
	- Visualization
		- Data
		- Format 
- Set up tile with selections (to filter data)

## Create, edit and preview analysis

To create an analysis open Genus Desktop and choose the portal **Discovery**. This is where both **Data Marts** and **Analysis** are available. In the Discovery-panel click on **Analysis** and **New**. Remember to save. To reopen an analysis in edit mode, right click the analysis and choose **Edit**.  

To preview an analysis either: 

- double click on the saved analysis in Discovery Desktop
- in the analysis editor click on **Action**. In the action dropdown there are two preview choices, one for Genus Desktop preview and one for internet browser preview.   

## Analysis 

An **Analysis** is a set of **Tiles** where each tile uses one of many **Visualizations**. The tile has a header, body and footer. The header contains a title, subtitle and/or background and is only visible if any of these are set. The body consists of the visualization, while the footer contains actions.  

In the analysis, tiles are located in the grey area to the left, while the tile pane is located to the right. The different visualizations are located on top of the tile pane, while configurations to the visualization are made in the bottom part of the tile pane. The tile pane configuration part consists of **Data**, **Format** and **Actions** sections. 

Visualizations and Data, Format and Actions:   
![tile_pane.jpg](media/tile_pane.jpg) 

The visualization decides what type of configurations can be made to the tile. Read more on visualizations in [Analysis concepts](https://docs.genus.no/users/analyze-report-and-discover/analysis/concepts.html).  

#### Useful links:
- [Analysis concepts](https://docs.genus.no/users/analyze-report-and-discover/analysis/concepts.html) 
- [Analysis visualizations](https://docs.genus.no/users/analyze-report-and-discover/analysis/visualizations.html)
- [Design an analysis](https://docs.genus.no/users/analyze-report-and-discover/analysis/designer/index.html) 

## Exercise  
Try to recreate the analysis shown in class/analysis in the solution environment. The steps for each tile are listed below.  

### Total number of trips

1. In the Discovery-panel click **Analysis** and create a new analysis. Remember to save.  

2. In the analysis edit mode, create a new tile by clicking the red circular plus button on the bottom right. 

3. Scale the tile to match the solution environment and give the tile a header. The header can be 		configured in **Format**. Click on Header -> Title.  

4. Choose visualization **Measure**.
	
    a. In DATA - Value - choose a data source and aggregation. A value can be a count of objects in a data source, a field (or function) of an object in a data source, an aggregated numeric property of a set of objects, or the result of a formula. In this case we want to count the number of objects in the data source Yellow Trip.  
	
    b. In FORMAT - Body - change font size and colour.

5. Save and preview.

### Number of trips per weekday

1. Create a new tile. Scale tile and give it a header. 

2. Choose visualization **Lines**.

    a. In DATA - Horizontal category - choose a data source. A category is a data source binding, and defines how the data is displayed. A visualization can contain one or more categories. In this case we want to show the weekdays as the horizontal category.  

    b. In DATA - Values - choose a data source. In this case we want to know how many Yellow Trips are made per category weekday.

    c. In FORMAT - Legend - set a legend position. 

    d. In FORMAT - Axes - Primary Value Axis - Change number format to zero decimals.

    e. In FORMAT - Values - change number format to zero decimals and change data series colour. Also set data point label to **custom** and write **{value}**. This will make the values of each datapoint visible. 

3. Save and preview. 

### Selections with dropdown

1. Create a new tile. Scale tile and give it a header. 

2. Choose a visualization **Dropdown**
	
    a. Create a dropdown and choose a data source. The data source will appear in the analysis and be available for selections.  

    b. Create two additional dropdowns in the same dropdown tile.  

3. Save and preview. While previewing, do a selection in the dropdown. Notice how the numbers in the different tiles change as selections are made. 

### Ignore selections

1. In the first tile with total number of trips, open the value and chose weekday in ignore selection. 

2. Save and preview. Do selections on weekday and check if number of trips changes with the selection. 

## Extra work 

- Create a tile that shows _% trips per borough PU_ 
- Create a tile that shows _total amount per payment type_

