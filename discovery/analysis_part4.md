# Analysis Part Four - Advanced analysis 

#### Session by instructor
_In this section the participants will learn how to use more advanced analysis techniques by visualizing data using the **Sankey** and **Map** tools._

#### Agenda 

- Sankey
- Map
	- GeoJSON
	- Heat spots
	- Vector layer

## Exercise

Try to recreate the analysis shown in class in the solution environment. 	
	
### Sankey

Sankey is a type of flow diagram where the width of the streams is proportional to the quantity of the flow. 

Objective: Create a diagram that shows the flow of taxi trips from one part of New York City to another part of the city.

**Adding boroughs**

1. Create a new analysis

2. Add a new tile, and choose the visualization **Sankey** 

	![sankeyicon.png](media/sankeyicon.png) 


3. In Data set **Category 1** and **Category 2** to the data sources "Borough PU" and "Borough DO", respectively.

4. Choose “Yellow trip” as value, and make sure the aggregation is set to **Count**.

5. Save and preview.

**Adding community districts**

1. Add two new categories – "Community District PU" and "Community District DO".

2. Rearrange the order of the categories so that the flow starts with "Borough PU" and ends with "Borough DO".

	![sankeycategoryorder.png](media/sankeycategoryorder.png) 


3. Add two new values. Since we want to show the same data flowing through all the categories, both of the new values should be assigned to the same data source and aggregation as the first one.

4. Save and preview.

### Map

The objective of this exercise is to visualize the taxi trip data by using maps.

Theory about GeoJSON.

**Adding the map base**

1. Make a new analysis, and add a tile with the visualization **Map**. 

	![mapicon.png](media/mapicon.png)


2. Add a new map layer, and set Type=Map and Server type=OSM. This will be your “base layer”.

**Adding the GeoJSON for boroughs**

3. Add a new map layer. **Type=GeoJSON**, **Coordinate system=WGS84**

4. As **GeoJSON URL**, choose one of the following URLs

For solutions with user 1  
[https://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json](http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json)  
For solutions with user 2  
[https://edudiscovery2.genus.net/discover/Resources/GeojsonBorough.json](http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json)  

5. As **GeoJSON id-field** you should add the name of the field in your GeoJSON that uniquely identifies each region. This field also have to be mapped to a value in the data source you want to add the geoJSON to. In this case the field is “BoroCode”.

6. **Data binding**: Add "Borough PU" or "DO" as data source, and choose the field that corresponds with your **GeoJSON-field**. This field is called “BoroCode”.

7. Save and preview. You should now be able the see the boroughs in your map.

**Adding the GeoJSON for community districts**

1. Add another GeoJSON map layer. 

2. As **GeoJSON URL**, choose one of the following URLs:

For solutions with user 1  
[https://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json](http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json)  
For solutions with user 2  
[https://edudiscovery2.genus.net/discover/Resources/GeojsonCommunityDistrict.json](http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json)  

3. Add community district as your data source. Make sure your choice of pickup versus dropoff corresponds with what you chose for borough.

4. Set **Show layer selector** to enabled

5. Save and preview. Use the layer selector to switch between the two GeoJSON layers.

**Color distribution based on value - Conditional colors**

1. In DATA, select the borough layer, and add a **Value**. Use the same data source as you used in your data binding. Set BoroCode as your field.

	![mapboroughbinding.png](media/mapboroughbinding.png)


2. Go to FORMAT, and select your borough layer.

3. Open **GeoJson Fill Color**.

4. We now want to add a color to each region. To do this, click on **conditional colors**. Here, add a color to each BoroCode 

	![mapconditionalcolors.png](media/mapconditionalcolors.png)


5. Save and preview. Each borough in your map should now have a color.

**Color distribution based on value - gradient based on number of trips**

1. In DATA, select the community district layer, and add a **Value**. Choose "Yellow Trip" as your data source, and make sure **Aggregation** is set to **Count**.

2. Go to FORMAT, and select your community district layer. Open **GeoJson Fill Color**.

3. We now want to add a color gradient to each region. To do this, click on each end of the color scale, and choose a color.

4. Save and preview. The districts in your map should now have a gradient color distribution based on number of trips.

**Color distribution based on value - gradient based on average speed**

5. Go to **Value** in FORMAT and choose the field "trip speed". Set **Aggregation** to **Average**.

6. Save and preview. The color gradient now shows average trip speed per community.

**Selections**

1. Add two new table tiles to your analysis, and set data source to the two data sources used in your geoJSON layers (borough and community district). Add some useful columns.

2. Save and preview. By selecting a borough or community district in your table, the map should now be responsive, and reflect your selection.


You can read more about maps in the [Genus Documentation](https://docs.genus.no/users/analyze-report-and-discover/analysis/visualizations.html)
