
**_Øvingsopplegg er under arbeid_**

# Data Mart Part One - Create a Data Mart

### SESSION BY INSTRUCTOR: 

_The main idea of the data mart is to simplify access to enterprise data, for different purposes and users, by reducing data complexity and volume. More on data mart concepts [here](https://docs.genus.no/users/analyze-report-and-discover/data-marts/data-mart-concepts.html). After the lesson the participants will recreate the data mart made in class._

#### Agenda:

- Data Mart 
    - Data Sources
        - Add and remove
    - Data View 
        - Data filter
        - Published fields
        - Connections 
- Circular references and directions of data flow
- Data Mart Load Plan
    - General
    - Reload
    - Autoload 
    - Status
- Load State for data mart

## Create Yellow Trips Data Mart

To create a data mart open Genus Desktop and open the portal **Discovery**. Create a new data mart by clicking **New** in the toolbar, or by right-clicking in the list of data marts and clicking **New**. Save the data mart. 

#### Useful links:

Add data source, properties, connections - [Data view](https://docs.genus.no/users/analyze-report-and-discover/data-marts/data-view.html)

### Data Sources 

There are multiple methods of adding data sources to the data mart. Use the method you prefer and add data sources to the data mart. The methods are summarised below. 

Data sources that should be included in the data mart: 

* Yellow Trip
* Borough Pick Up
* Borough Drop off
* Payment Type
* Rate Code
* Service Zone Pick Up
* Service Zone Drop Off
* Store and forward
* Taxi Zone Pick Up 
* Taxi Zone Drop Off
* Vendor
* Weekday
* Day
* Week 

Data Sources that are added more than once represent different connections, in this case Borough, Service Zone and Taxi Zone. For example, the two data sources for Taxi Zone represents **pick up zone** and **drop off zone** in Yellow Trip.  

#### Choose Data Sources from list

In the newly created data mart add object classes in **Data Sources** or **Data View**. To add object classes in **Data Sources** right click -> Add -> Object... To add an object class in **Data View** right click -> New -> Data Source -> Object... 

#### Choose Data Sources by connections  

Another way of adding data sources is to start with a data source and add new ones based on the connection to the first data source:

- Right click on a data source in data view.
- Click New -> Outbound Data Sources or Inbound Data Sources 
- Select data sources 
- Add 

**Outbound data sources** adds data sources referenced in the chosen data source, while **Inbound Data Sources** adds data sources with references to the chosen data source. By using this method connections between the data sources are automatically created. 

### Published Fields

To make data available for analysis **Property Fields** must also be specified. They can be added in Data View. Right click on each data source -> Published fields -> Add/Remove. 

If a property is not among the published fields, it will not be available in any analysis using the data mart. It is a good rule of thumb to only publish fields required to fulfil the purpose of the data mart to keep the complexity down.  

### Data Filter

Each data source is default set to read "All objects", but for object classes with millions of rows the data filter should be restricted. Data Filter can be restricted in Data Sources or Data View.  

In this data model, most of the object classes are small and don't need to be limited, except for Taxi Trips which has millions of rows. The data filter should therefore include Yellow Trip if the boolean **Include in data mart** is equal to true. 

If all objects are read for large data sources, the data mart will take a long time to load and the server can potentially crash due to no available memory. 

### Connections

In the app model a connection between two object classes means that one object class has a a reference to the other object class, or one object class has a property that can contain values from the other object class. 

If you have chosen to add data sources from the list there are no connections between the object classes.  

To connect data sources click on data view -> right click on data source -> connection. 
