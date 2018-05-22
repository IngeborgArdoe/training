
**_Øvingsopplegg er under arbeid_**

# Data Mart Part One - Create a Data Mart

### SESSION BY INSTRUCTOR: 

_The main idea of the data mart is to simplify access to enterprise data, for different purposes and users, by reducing data complexity and volume. More on data marts [here](https://docs.genus.no/users/analyze-report-and-discover/data-marts/getting-started.html). After the lesson the participants will recreate the data mart made in class._

#### Agenda:

- Data Mart 
    - Data Sources
        - Add and remove
    - Data View 
        - Data filter
        - Published fields
        - Connections 
- Circular references and directions of data flow
- data mart Load Plan
    - General
    - Reload
    - Autoload 
    - Status
- Load State for data mart

## Create Yellow Trips Data Mart

To create a data mart open Genus Desktop and open the portal **Discovery**. Create a new data mart by clicking **New** in the toolbar, or by right-clicking in the list of data marts and clicking **New**. Save the data mart. 

### Data Sources and Published Fields

In the newly created data mart add the object classes in **Data Sources** or **Data View**. To add object classes in **Data Sources** right click -> Add -> Object... To add an object class in **Data View** right click -> New -> Data Source -> Object... 

To make data available for the analysis **Property Fields** must also be specified. They can be added in Data View. Right click on each data source -> Published fields -> Add/Remove.  

### Data Filter

Each data source is default set to read "All objects", but for object classes with millions of rows the data filter should be restricted. It is done in **Data Filter** in Data Sources or Data View.  

In this data model most of the object classes are small and don't need to be limited, except Taxi Trips, which has many million rows. In Taxi Trips there is one field -  used to read wanted taxi trips. We have made  this In Taxi Trips there has been  created a flag to indicate the taxi t

### Connections

When adding datasources the object classes appear in _data view_, but without any connections. 

