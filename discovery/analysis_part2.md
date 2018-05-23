
**_Øvingsopplegg er under arbeid_**

# Analysis Part Two - Formula editor and data manipulation

### SESSION BY INSTRUCTOR: 
_After the lesson the participants will recreate the analysis made in class._

#### Agenda 

- Formula editor
- Split by category
- Actions 
	- Commands

## Analysis from class

Try to recreate the analysis shown in class/analysis in the solution environment. These are the steps: 	
	
### Key Values 
The goal of this tile is to show the formula editor and how to display the calculated value in combination with a self composed text. More on formula editor [here](https://docs.genus.no/users/analyze-report-and-discover/analysis/designer/formula-designer.html)  
	
1. Create a tile. Resize the tile and give it a header. 

2. Choose tiletype _Text_
	
    a. Create a parameter. Calculate the average price of a trip using the formula editor. To use formula the data source field must be empty. In the formula editor create two fields for total amount and total number of trips. In the field-editor, choose a data source, field and aggregation and give the field a label. When the fields are ready, make the formula for average price in the formula editor view. To use a field in the formula click on the label for the field. To edit the field push the three dots to the right of the field label.   
	
    b. Create a new parameter. This parameter should also calculate the average price of a trip, but now by using data source, field and aggregation. To use the data source field the formula field must be empty. 

    c. Create a new parameter. Calculate the average duration of a trip in hours. If necessary, change the number format.  

    d. In the tiletype panel write a text for each value in _markdown text_. To insert a parameter write {} and then the number of the parameter, i.e. {1} for average price of a trip calculated in the formula editor. To make line breaks insert <br>. 
	
	e. Change the size and colour of the text in FORMAT. 
	
3. Save and preview. Verify that the two average prices are the same. 

### Number of trips per weekday split by payment category

1. Create a tile. Resize the tile and give it a header.

2. Choose tiletype _Columns_

    a. Choose a data source for the horizontal category. 

    b. Choose a data source that should split the horizontal category. 

    c. Set the value. What data source/field should be counted? 

3. Save and preview. 
  	
### Links

1. Create a tile. Resize the tile and give it a header "Link to Taxi Trips". Change the colour of the header to blue. 

2. In the tile panel click on _Action_ and add an action. _Click on_ decides where the user should click to trigger the command, use _header_ in this example. After creating an action, create a command in the action. The type of command should be "open analysis with same selection" and the analysis should be the first analysis you made. 

3. Save and preview. Does a click on the header open the first analysis? 

4. Create a tile. Resize the tile and do not give the tile a header. 

5. Click on _actions_. Create an action and a command. The action should open a form when clicking on a button with the label "Open Form". 

6. Save and preview. Does a click on the button open the right form? 

### Extra

1. Create a new parameter in _Key Values_. Calculate the average price per mile and make it visible in the tile. 

2. Change the column chart from number of trips to total amount. 

3. In the first analysis, create a new tile that jumps back to analysis two.

4. Create a tile with tiletype _Variable Radius Pie_ that shows _% tip amount per pick up borough_.

