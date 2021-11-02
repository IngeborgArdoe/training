

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
* Completed Month
* Started Month

Data Sources that are added more than once, represent different connections, in this case _Month_ and _Category_. For example, the two data sources for Month represents different timestamps.  

For each data source, you should evaluate the data sources' max occurences, if it should be private and if it should **Allow Aggreagate Requests Only**.

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

If a property is not among the published fields, it will not be available in any analysis using the data mart. It is a good rule of thumb to only publish fields required to fulfil the purpose of the data mart to keep the complexity down.  

### Data Filter

Each data source is by default set to read "All objects", but for object classes with millions of rows the data filter should be restricted. Data Filter can be restricted in Data Sources or Data View.  

In this data model, most of the object classes are small and don't need to be limited, except for Taxi Trips which has millions of rows. The data filter for Yellow Trip should be included if the boolean **Include in data mart** is equal to true.

If all objects are read for large data sources, the data mart will take a long time to load or the server can potentially crash due to the server running out of memory.  

### Connections

In the app model a connection between two object classes means that one object class has a a reference to the other object class, or one object class has a property that can contain values from the other object class.

If you have chosen to add data sources through connections, the connections are already in place, but if the data sources where added from the list there are no connections between the object classes.  

To connect data sources, or change existing connection, click on data view -> right click on data source -> connection. Connections are also available in data view -> click on data source -> properties panel -> connections.  

Add connections by choosing which field in the data source is connected to another data source in the data mart.

Complete list of connections from Yellow Trip is displayed below:

![DM_connections_final.png](media/DM_connections_final.png)

### Data Mart Load Plan

A data mart needs to be loaded before it is ready to provide data for analyses. Create a data mart load plan that loads the data mart twice per day starting at 11.00 AM and only auto loads between 07.00-20.00.

- In Genus Desktop click on Discovery -> expand Data Marts shortcut -> click on **Load Plans** -> "New"
- General is a summary of **Reload** and **Auto Load** plans.
- In reload set up the data mart to load every day at 11.00, then click Advanced... and set up reload every 12 hours for 24 hours. ![DM_loadplan.jpg](media/DM_loadplan.jpg)
- In auto load set up to not auto load in interval 00.00-07.00 and 20.00-00.00 ![DM_loadplan_autoload.jpg](media/DM_loadplan_autoload.jpg)

## Extra

- Try to create a circular reference
