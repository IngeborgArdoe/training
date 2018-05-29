
# Analysis Part Two - Formula editor and data manipulation

#### SESSION BY INSTRUCTOR: 
_The instructor will start of by giving you an introduction to the topic. After the lesson the participants will recreate the analysis made in class._

#### Agenda 

- Formula editor
- Split by category
- Actions 
	- Commands

## Exercise 

Try to recreate the analysis shown in class/analysis in the solution environment. These are the steps: 	
	
### Key Values 
The goal of this tile is to show the formula editor and how to display the calculated value in combination with a self composed text. More on formula editor [here](https://docs.genus.no/users/analyze-report-and-discover/analysis/designer/formula-designer.html).  
	
1. Create a tile. Resize the tile and give it a header. 

2. Choose visualization **Text**
	
    a. Create a parameter. Calculate the average price of a trip using the formula editor. To use formula the data source field must be empty. In the formula editor create two fields for total amount and total number of trips. To create a field click on **new field**. In the field-editor, choose a data source, field and aggregation and give the field a label. In this case the fields should represent total amount and total number of yellow trips.  
	
	When the fields are ready, make the formula for average price in the formula editor view. To use a field in the formula click on the label for the field in **Formula values**. To edit the field click the three dots to the right of the field label.   
	
	![tile_formula_avgprice.jpg](media/tile_formula_avgprice.jpg)
	
    b. Create a new parameter. This parameter should also calculate the average price of a trip, but now by using data source, field and built in aggregation. To use the data source field the formula field must be empty. 

    c. Create a new parameter. Calculate the average duration of a trip in hours. If necessary, change the number format. Hint - the duration may be less than zero hours.  

    d. In the tile panel write a text for each value in **markdown text**. To insert a parameter write {} and then the number of the parameter, i.e. {1} for average price of a trip calculated in the formula editor. To make line breaks insert <br>. 
	
	![tile_markdown.jpg](media/tile_markdown.jpg)
	
	e. Change the size and colour of the text in FORMAT. 
	
3. Save and preview. Verify that the two average prices are the same. 

### Number of trips per weekday split by payment category

1. Create a tile. Resize the tile and give it a header.

2. Choose visualization **Columns**

    a. Choose a data source for the horizontal category. 

    b. Choose a data source that should split the horizontal category. 

    c. Set the value. What data source/field should be counted? 

3. Save and preview. 
  	
### Actions
Actions allows you to define events in the analysis. An action can be connected to either a header or a button in the footer. An action can be defined to open a form, open a table, add selections, remove selections, etc. 

1. Create a tile. Resize the tile and give it a header "Link to Taxi Trips". Change the colour of the header to blue. 

2. In the tile panel click on **Action** and add an action. **Click on** decides where the user should click to trigger the command, use **header** in this example. After creating an action, create a command in the action. The type of command should be "Open analysis with same selection" and the analysis should be the first analysis you made. 

3. Save and preview. Does a click on the header open the first analysis? 

4. Create a tile. Resize the tile and do not give the tile a header. 

5. Click on **Actions**. Create an action and a command. The action should open a table when clicking on a button with the label "Open Pick Up Zones". The mapping must use "Pick up zone" as the source and "Selected" as filter. 

6. Save and preview. Does a click on the button open the right table? 

### Extra

1. Create a new parameter in **Key Values**. Calculate the average price per mile and make it visible in the tile. 

2. Change the column chart from number of trips to total amount. 

3. Make the header to tile one "Key Values" a link to analysis one. Delete the tile that is only a link to analysis one. 

4. In the first analysis, create a new tile that goes back to analysis two.

5. Create a tile with visualization **Variable Radius Pie** that shows _% tip amount per pick up community district_.

