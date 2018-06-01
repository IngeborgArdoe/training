
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

5. Save and preview.

**Adding community districts:**

1. Add two new categories – "Community District PU" and "Community District DO".

2. Rearrange the order of the categories so that the flow starts with "Borough PU" and ends with "Borough DO". image: sankeycategoryorder

3. Add two new values. Since we want to show the same data flowing through all the categories, both of the new values should be assigned to the same data source and aggregation as the first one.

4. Save and preview.

### Map

The objective of this exercise is to visualize the taxi trip data by using maps.

Theory about GeoJSON.

**Adding the map base**

1. Make a new analysis, and add a tile with the control type **Map**. image: mapcontroltype.

2. Add a new map layer, and set Type=Map and Server type=OSM. This will be your “base layer”.

**Adding the GeoJSON for boroughs**

3. Add a new map layer. **Type=GeoJSON**, **Coordinate system=WGS84**

4. As **GeoJSON URL**, choose one of the following URLs:

For solutions with user 1  
[http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json](http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json)
For solutions with user 2  
[http://edudiscovery2.genus.net/discover/Resources/GeojsonBorough.json](http://edudiscovery.genus.net/discover/Resources/GeojsonBorough.json)

5. As **GeoJSON id-field** you should add the name of the field in your GeoJSON that uniquely identifies each region. This field also have to be mapped to a value in the data source you want to add the geoJSON to. In this case the field is “BoroCode”.

6. **Data binding**: Add "Borough PU" or "DO" as data source, and choose the field that corresponds with your **GeoJSON-field**. This field is called “BoroCode”.

7. Add a **Value**, and use the same data source as you used in your data binding. Set BoroCode as your field. image: mapboroughbinding

8. Save and preview. You should now be able the see the boroughs in your map.

**Adding the GeoJSON for community districts**

1. Add another GeoJSON map layer. 

2. As **GeoJSON URL**, choose one of the following URLs:

For solutions with user 1  
[http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json](http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json)
For solutions with user 2  
[http://edudiscovery2.genus.net/discover/Resources/GeojsonCommunityDistrict.json](http://edudiscovery.genus.net/discover/Resources/GeojsonCommunityDistrict.json)

3. Add community district as your data source. Make sure your choice of pickup versus dropoff corresponds with what you chose for borough.

**Color distribution based on value**

[Link to more information about maps](https://docs.genus.no/users/analyze-report-and-discover/analysis/visualizations.html)

