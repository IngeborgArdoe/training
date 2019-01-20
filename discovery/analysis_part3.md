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
	
1. Copy the analysis made in [Analysis Part Two - Formula editor and data manipulation](http://training.genus.no/discovery/analysis_part2.html) 

2. Keep the tile showing number of trips per payment type, and remove all other tiles.

3. Duplicate the tile, so that you have two identical tiles. 

	![subsetduplicate.png](media/subsetduplicate.png) 


4. Pick a tile and in Data, go to **Value (# Yellow Trip)** and add a subset. Choose the subset "Total amount > $200". 

5. Save and preview your analysis. You should now see the difference between the original tile and the tile using the subset.

6. Go back to the same tile where you added the subset. On **Value (# Yellow Trip)** , open the subset selector and add the subset "Total tip > $50". You now have two subsets on the same tile.

7. Save and preview. 

**Applying subsets using the Subset visualization**

1. Add a new tile, and choose the **Subsets** visualization

	![subsetselectionicon.png](media/subsetselectionicon.png)  


2. In Data, expand **Available** to see the available subsets. Choose the "Weekend" subset.

3. Save and preview the result. In your preview analysis, any user should now be able to add and remove the "Weekday" subset. Verify that the data in your tiles changes when you add and remove the subset.

### Calculated fields

The objective of this exercise is to apply the calculated fields created in the data mart in an analysis. In addition, the section will show how calculations can be done directly in the analysis by combining subsets and calculated fields.

**Add calculated fields**

1. Create a new tile, with visualization **Table**.

2. Under Data, choose "Community District PU" as your data source.

3. Remove all columns except the "Name" column, and add a header to your table.

4. Add a column for each of the calculated fields that were created in the data mart. For all columns, keep the default aggregation.

5. In Format, go to each column (except "Name") and change the value format from zero to two decimals.

6. Save and preview. In your preview analysis, select a weekday in one of the "Number of trips per payment type" tiles. The selection should affect the data in the calculated fields.

**Calculate values using the analysis tool**

1. In the table tile, choose the column showing the calculated field for average trip speed per "Yellow Trip". Under **Aggregation**, choose **Average**. 

2. Save and preview. The altered column should now be identical to the column showing the calculated field for average trip speed per community district.

3. Next, go to the same column, and add the subset for tip > $50. 

4. Save and preview. The altered column should now be identical to the column showing the calculated field for average trip speed per community district with tip > $50.

**Using calculated fields in formulas**

1. Remove any subsets applied to the columns  in your table tile.

2. Add a new column. 

3. Under Data, open the formula editor. Here the existing columns from your table should already be available under Tile values.

4. Create a new formula using the tile values, or by adding new fields, that shows average trip speed divided by total amount paid. 

5. Repeat steps 2-4, but now find average trip speed/amount when tip > $50. 

6. Save and preview. What does the resulting columns tell you?

**Extra work**

1. Add an intial selection to your analysis. Inital selections can be set under the Settings pane in your analysis editor.

