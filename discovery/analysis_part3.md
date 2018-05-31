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

**Applying subsets on Value**:
	
1. Copy the analysis made in [Analysis Part Two - Formula editor and data manipulation](http://training.genus.no/discovery/analysis_part2.html) 

2. Keep the tile showing tip amount per payment type, and remove all other tiles.

3. Duplicate the tile, so that you have two identical tiles. image:subsetduplicate

4. Pick a tile and in DATA, go to Value (# Yellow Trip) and add a subset. Choose the subset "Total amount > $200". 

5. Save and preview your analysis. You should now see the difference between the original tile and the tile using the subset.

6. Go back to the same tile where you added the subset. On Value (# Yellow Trip) , open the subset selector and add the subset "Total tip > $50". You now have two subsets on the same tile.

7. Save and preview. 

**Applying subsets using the Subset control type:**

1. Add a new tile, and choose the "Subsets" control type.