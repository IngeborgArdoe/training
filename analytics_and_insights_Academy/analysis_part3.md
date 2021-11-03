# Analysis Part Three - Applying subsets and calculated fields to analyses

#### Session by instructor
_In this section the participants will learn how the subsets and calculated fields made in the previous section can be applied in different analyses._

#### Agenda

- Subsets
- Calculated fields
- Combining subsets and calculated fields
- Initial selections

## Exercise

Try to recreate the analysis shown in class. 	

### Subsets
The objective of this exercise is to use the subsets created in the data mart in the analysis tool.

**Applying subsets on Value**

1. Create a new dasboard and create a column-based tile similar to that from your "Analysis 2" (Split by month and Category)

3. Duplicate the tile, so that you have two identical tiles.

	![subsetduplicate.png](media/subsetduplicate.jpg)


4. Pick a tile and in Data, go to **Value (# No of Task)** and add a subset. Choose the subset "Cost > $6 000".

5. Save and preview your analysis. You should now see the difference between the original tile and the tile using the subset.

6. Go back to the same tile where you added the subset. On **Value (# No of Task)** , open the subset selector and add the subset "Duration > 13 Days". You now have two subsets on the same tile.

7. Save and preview.

**Applying subsets using the Subset visualization**

1. Add a new tile, and choose the **Subsets** visualization

	![subsetselectionicon.png](media/subsetselectionicon.png)  


2. In Data, expand **Available** to see the available subsets. Choose the "Completed" subset.

3. Save and preview the result. In your preview analysis, any user should now be able to add and remove the "Completed" subset. Verify that the data in your tiles changes when you add and remove the subset.

### Calculated fields

The objective of this exercise is to apply the calculated fields created in the data mart in an analysis. In addition, the section will show how calculations can be done directly in the analysis by combining subsets and calculated fields.

**Add calculated fields**

1. Create a new tile, with visualization **Table**.

2. Under Data, choose "Task Category" as your data source and add a header to your table.

4. Add a column for each of the calculated fields that were created in the data mart. For all columns, keep the default aggregation.

5. In Format, go to each column (except "Name") and change the value format from zero to two decimals.

6. Save and preview. In your preview tile, select a the "Completed Task"-subset in the Subsets-selector. The selection should affect the data in the calculated fields.

**Calculate values using the analysis tool**

1. In the table tile, add another column showing the calculated field for average time to resolve per Task. Under **Aggregation**, choose **Average**.

2. Save and preview. The altered column should now be identical to the column showing the original.

3. Next, go to the same column, and add the subset for Cost > 6 000.

4. Save and preview. The altered column should now be identical to the column showing the calculated field for average time to resolve for tasks with cost > 6 000.
<!--
**Using calculated fields in formulas**

1. Remove any subsets applied to the columns in your table tile.

2. Add a new column.

3. Under Data, open the formula editor. Here the existing columns from your table should already be available under Tile values.

4. Create a new formula using the tile values, or by adding new fields, that shows average duration divided by total cost.

5. Repeat steps 2-4, but now find average trip speed/amount when tip > $50.

6. Save and preview. What does the resulting columns tell you? -->

**Extra work**

1. Add an intial selection to your analysis. Inital selections can be set under the Settings pane in your analysis editor.
