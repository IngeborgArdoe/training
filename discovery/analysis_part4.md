
# Analysis Part Four - Advanced analysis 

### SESSION BY INSTRUCTOR: 
In this section the participants will learn how to use more advanced analysis techniques by visualizing data using the **Sankey** and **Map** tools.

#### Agenda 

- Sankey
- Map
	- GeoJSON
	- Heat spots (Coming soon!)
	- Vector layer (Coming soon!)

## Exercise

Try to recreate the analysis shown in class in the solution environment. 	
	
### Sankey

Sankey is a type of flow diagram where the width of the streams is proportional to the quantity of the flow. 

Objective: Create a diagram that shows the flow of taxi trips from one part of New York City to another part of the city.

**Adding boroughs:**

1. Create a new analysis

2. Add a new tile, and choose the control type **Sankey** image:sankeyicon

3. In DATA set **Category 1** and **Category 2** to the data sources "Borough PU" and "Borough DO", respectively.

4. Choose “Yellow trip” as value, and make sure the aggregation is set to **Count**.

**Adding community districts:**

1. Add two new categories – "Community District PU" and "Community District DO".

2. Rearrange the order of the categories so that the flow starts with "Borough PU" and ends with "Borough DO". image: sankeycategoryorder

3. Add two new values. Since we want to show the same data flowing through all the categories, both of the new values should be assigned to the same data source and aggregation as the first one.

### Map

The objective of this exercise is to ...

Theory about GeoJSON.

**Adding the map base**

1. Create a new tile, with control type **Map**.

[Link to more information about maps](https://docs.genus.no/users/analyze-report-and-discover/analysis/visualizations.html)

**Adding the GeoJSON for boroughs**

1. Add a new map layer.

[http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json](http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json)

**Adding the GeoJSON for community districts**

1. Add a new map layer. 

[http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json](http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json)

**Color distribution based on value**

