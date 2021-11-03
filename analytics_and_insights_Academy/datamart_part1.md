

# Data Mart Part One - Create a Data Mart

#### SESSION BY INSTRUCTOR

_The main idea of the data mart is to simplify access to enterprise data, for different purposes and users, by reducing data complexity and volume. The instructor will start of by giving you an introduction to the topic. After the lesson the participants will recreate the data mart made in class._

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

## Exercise
In this exercise, you are going to recreate the "Task" data mart, and add Concern.

To create a data mart
1. Open the Analytics and Insights application
2.  Create a new data mart by clicking **New** in the action bar
3. Save the data mart.

#### Useful links:
Data mart concepts - [here](https://docs.genus.no/users/analyze-report-and-discover/data-marts/data-mart-concepts.html)  
Data source, properties, connections in [Data view](https://docs.genus.no/users/analyze-report-and-discover/data-marts/data-view.html)

### Data Sources

Data sources that should be included in the data mart:

* Tasks
* Concern
* Company
* Concern Category
* Task Category
* Concern State
* Task State
* Started Month
* Started Day

Data Sources that are added more than once, represent different connections, in this case _Category_.  

For each data source, you should evaluate the data sources' max occurences, if it should be private
 <!-- and if it should **Allow Aggreagate Requests Only**. -->

There are multiple methods of adding data sources to the data mart. Use the method you prefer and add data sources to the data mart. The methods are summarised below.

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

If a property is not among the published fields, it will not be available in any analysis using the data mart. It is a good rule of thumb to only publish fields required to fulfil the purpose of the data mart to keep the complexity down.  A suggestion is:


![DM_connections_final.png](media/FM2.jpg)

### Data Filter

Each data source is by default set to read "All objects", but for object classes with millions of rows the data filter should be restricted. Data Filter can be restricted in Data Sources or Data View.  

In this data model, most of the object classes are small and don't **need** to be limited. Even so, it is **always best practice to add a data filter**. Data volumes can change over time, and for instance calendar datatypes can often make the creation of analysis more cluttered if they aren't limited.

If all objects are read for large data sources, the data mart will take a long time to load or the server can potentially crash due to the server running out of memory.  

### Connections

In the app model a connection between two object classes means that one object class has a a reference to the other object class, or one object class has a property that can contain values from the other object class.

If you have chosen to add data sources through connections, the connections are already in place, but if the data sources where added from the list there are no connections between the object classes.  

To connect data sources, or change existing connection, click on data view -> right click on data source -> connection. Connections are also available in data view -> click on data source -> properties panel -> connections.  

Add connections by choosing which field in the data source is connected to another data source in the data mart.

Complete list of connections from Task is displayed below:

![DM_connections_final.png](media/connections.jpg)

### Data Mart Load Plan

A data mart needs to be loaded before it is ready to provide data for analyses. Load Plans can be accessed from the "Analytics and Insights" app. In the "Data Marts"-navigation, you can click "Data Mart Monitor" in the action bar to check status of loading. Create a data mart load plan that loads the data mart every 1 hour.

- Highlight your new data mart and toggle "Load Plan" in the action bar.
- Set Availability to 0600-23:00
- Demand that the data mart is never older than 60 minutes.

 ![DM_loadplan_autoload.jpg](media/loadplan.jpg)

## Extra

- Try to create a circular reference (for instance by adding a connection between Company and Concern)
