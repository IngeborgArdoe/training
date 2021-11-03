
# Analysis Part Two - Formula editor and data manipulation

#### SESSION BY INSTRUCTOR
_The instructor will start of by giving you an introduction to the Formula Editor and Actions. After the lesson, the participants will recreate the analysis made in class._

#### Agenda

- Formula editor
- Split by category
- Actions
	- Commands

## Exercise

Try to recreate the analysis shown in class/analysis in the solution environment. These are the steps: 	

### Key Values
The goal of this tile is to show the formula editor and how to display the calculated value in combination with a self composed text. More on formula editor [here](https://docs.genus.no/users/analyze-report-and-discover/analysis/designer/formula-designer.html).  

1. Create a tile with visualization **Text**. Resize the tile and give it a header.

a. Create a parameter. Calculate the average amount of days to complete a task using the formula editor. To use formula, the data source field must be empty. In the formula editor, create two fields for total amount of days and total number of **completed** tasks. To create a field, click on **new field**. In the field-editor, choose a data source, field and aggregation and give the field a label. In this case the fields should represent total amount of days and total number of tasks.  

When the fields are ready, create the formula for average price in the formula editor view. To use a field in the formula click on the label for the field in **Formula values**. To edit the field click the three dots to the right of the field label.

Field 1       						 |  Field 2
:-----------------------------------:|:------------------------------------:
![Exc2fig8.JPG](media/a_field1.JPG)  | ![Exc2fig9.JPG](media/a_field2.JPG)

![Exc2fig8.JPG](media/a_formula.JPG)

  b. Create a new parameter. This parameter should also calculate the average completion time for a task, but now by using data source, field and built in aggregation. To use the data source field referencing the calculated fields, formula field must be empty.



  c. In the tile panel write a text for each value in **markdown text**. To insert a parameter write {} and then the number of the parameter, i.e. {1} for average time to resolve calculated in the formula editor. To make line breaks insert < br > without the extra spaces.

![tile_markdown.jpg](media/a_text.jpg)

e. Change the colour of the text in Format, and adjust padding.

3. Save and preview.
<!-- Verify that the two average prices are the same. -->

### Number of tasks per month split by category

1. Create a tile with visualization **Columns**. Resize the tile and give it a header.

    a. Choose a data source for the horizontal category.

    b. Choose a data source that should split the horizontal category.

    c. Set the value. What data source/field should be counted?

3. Save and preview.


###  Actions
Actions allows you to define events in the analysis. An action can be connected to either a header or a button in the footer. An action can be defined to open a form, open a view, add selections, remove selections, etc.

1. Return to the Exercise 1 - analysis. In the Completed Tasks - tile, add a Command of type "Open Dashboard with New Selection" and Click type "Button". Give it an appropriate name, and make sure to set Task Selection to Subset -> Completed

2. Also add a button on another tile without the "Completed"-subset, but send along for instance "Month" or "Category".

4. In "Analysis 2", create a new tile that goes back to "Analysis 1".

Remember that you can always determine whether the analysis is opened in another tab or not.

<!-- ### Actions
Actions allows you to define events in the analysis. An action can be connected to either a header or a button in the footer. An action can be defined to open a form, open a view, add selections, remove selections, etc.

1. Create a tile. Resize the tile and give it a header "Link to Task". Change the colour of the header to blue.

2. In the tile panel click on **Actions** and add an action. **Click on** decides where the user should click to trigger the command, use **Header** in this example. After creating an action, create a command in the action. The type of command should be "Open analysis with same selection" and the analysis should be the first analysis you made.

3. Save and preview. Does a click on the header open the first analysis?

4. Create a tile. Resize the tile and do not give the tile a header.

5. TODO: Click on Actions. Create an action and a command. The action should open a table when clicking on a button with the label "Open Pick Up Zones". The mapping must use "Pick up zone" as the source and **Selected** as filter.

6. Save and preview. Does a click on the button open the right table? -->


<!-- 1. Create a new parameter in "Key Values". Calculate the average response time per category and make it visible in the tile.

2. Change the column chart from number of tasks to total for all tasks. -->



<!-- TODO 5. Create a tile with visualization **Word Cloud** that show the names of _community districts in relation to average price_ per community district. The larger names have a higher average price than the smaller names.

6. Create a tile with visualization **Variable Radius Pie** that shows _% tip amount and toll amount per pick up community district_. -->
