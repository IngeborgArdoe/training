# Analysis Part Three - Applying subsets and calculated fields to analyses 

### SESSION BY INSTRUCTOR: 
In this section the participants will learn how the subsets and calculated fields made in the previous section can be applied in different analyses.

#### Agenda 

- Subsets
- Calculated fields
- Combining subsets and calculated fields

## Exercise

Try to recreate the analysis shown in class in the solution environment. 	
	
### Subsets
The objective of this exercise is to use the subsets created in the data mart in the analysis tool.

(Teacher's note: Add some theory on the use of subset on value versus the use of subset in the subset selection tile). 

**Applying subsets on Value**:
	
1. Copy the analysis made in [Analysis Part Two - Formula editor and data manipulation](http://training.genus.no/discovery/analysis_part2.html) 

2. Keep the tile showing tip amount per payment type, and remove all other tiles.

3. Duplicate the tile, so that you have two identical tiles. image:subsetduplicate

4. Pick a tile and in DATA, go to **Value (# Yellow Trip)** and add a subset. Choose the subset "Total amount > $200". 

5. Save and preview your analysis. You should now see the difference between the original tile and the tile using the subset.

6. Go back to the same tile where you added the subset. On **Value (# Yellow Trip)** , open the subset selector and add the subset "Total tip > $50". You now have two subsets on the same tile.

7. Save and preview. 

**Applying subsets using the Subset control type:**

1. Add a new tile, and choose the **Subsets** control type. image:subsetselectionicon.

2. In DATA, expand **Available** to see the available subsets. Choose the "Weekend" subset.

3. Save and preview the result. In your preview analysis, any user should now be able to add and remove the "Weekday" subset. Verify that the data in your tiles changes when you add and remove the subset.

### Calculated fields

The objective of this exercise is to apply the calculated fields created in the data mart in an analysis. In addition, the section will show how calculations can be done directly in the analysis by combining subsets and calculated fields.

**Add calculated fields**

1. Create a new tile, with control type **Table**.

2. Under DATA, choose "Community District PU" as your data source.

3. Remove all columns except the "Name" column, and add a header to your table.

4. Add a column for each of the calculated fields that were created in the data mart. For all columns, keep the default aggregation.

5. In FORMAT, go to each column (except "Name") and change the value format from zero to two decimals.

6. Save and preview. In your preview analysis, select a weekday in one of the "tip per payment type" tiles. The selection should affect the data in the calculated fields.

**Calculate values using the analysis tool**

1. In the table tile, choose the column showing the calculated field for average trip speed per "Yellow Trip". Under **Aggregation**, choose **Average**. 

2. Save and preview. The altered column should now be identical to the column showing the calculated field for average trip speed per community district.

3. Next, go to the same column, and add the subset for tip > $50. 

4. Save and preview. The altered column should now be identical to the column showing the calculated field for average trip speed per community district with tip > $50.