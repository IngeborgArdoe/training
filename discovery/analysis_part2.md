
**_Øvingsopplegg er under arbeid_**

#Analysis Part Two - Formula editor and data manipulation

### SESSION BY INSTRUCTOR: 
_After the lesson the participants will recreate the analysis made in class._

#### Agenda 

- Formula editor
- Split by category
- Actions 
	- Commands

## Key Values 
This goal of this tile is to show how to use the formula editor and how to display the calculated value in combination with self composed text. More on formula editor [here](https://docs.genus.no/users/analyze-report-and-discover/analysis/designer/formula-designer.html)  

    d. In the tiletype panel write a text for each value in _markdown text_. To insert a parameter write {} and then the number of the parameter, i.e. {1} for average price of a trip calculated in the formula editor.  
	
1. Create a tile. Resize and set title. 

2. Choose tiletype _Text_
	
    a. Create a parameter. Calculate the average price of a trip. To calculate the value using formula editor click on _formula_ in the new parameter. To use formula the data source field must be empty. In the formula editor create two fields for total amount and total number of trips.  When creating fields in the field-editor, choose the data source and field that needs to be summed. When the fields are ready, make the formula for average price in the formula editor view.  
	
    b. Create a new parameter. This parameter should also calculate the average price of a trip, but now by using data source, field and aggregation. 

    c. Create a new parameter. Calculate the average duration of a trip. 
	
3. Save and preview. Check if the two average prices are the same. If any of the value does not show a "correct" value, try changing the number format of the parameter. 


## Number of trips per weekday split by payment category

1. Create a tile. Resize and set title. 

2. Choose tiletype _Columns_

    a. Choose a data source for the horizontal category. 

    b. Choose a data source that should split the horizontal category.

    c. Set the value. What data source/field should be counted/summed? 

3. Save and preview. 
  	
## Links

1. Create a tile. Resize and set title. 

2. 

## Extra

1. Create a new parameter in _Key Values_. Calculate the average price per mile and make it visible in the tile. 

2. Change the column chart from number of trips to total amount. 

2. Create a tile with tiletype _Variable Radius Pie_ that shows _% tip amount per pick up borough_.
