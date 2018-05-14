#Analysis and Datamart introduction

In this course the participants will use **Datamart** and **Analysis** tools in **Genus Apps**, on a predefined data model, to get firsthand experience of how to discover new information and knowledge from existing data. 

Analysis and Datamart go hand in hand. Datamart is the structure and content of data, while analysis is the visual representation of the data. This course starts with basic implementation of analysis, continues to Datamart, then touches on more advanced analysis, before finally looking at finishing touches to both analysis and datamart.  

##Data model 
The data model used for this course represents New York City Yellow Cab taxi trips. The timespan is set to the first four weeks of 2017. The model includes the classes in the following list:

..* Yellow Trip
..* Borough
..* Payment Type
..* Rate Code
..* Service Zone
..* Store and forward
..* Taxi Zone
..* Vendor
..* Weekday


The main object class is Yellow Trip, where each instance represents a single trip. Each trip has information on pickup and drop off location, time and zone, and includes details on different payment amounts, payment type, duration of the trip and number of passengers. 

The pick up and drop off taxi zones consists of 265 different areas, such as "Jamaica Bay" and "Chinatown". Each taxi zone is connected to a larger Borough, which is split into seven areas. Two examples of boroughs are "Bronx" and "Brooklyn". Lastly, each borough is connected to a Service zone. There are five Service zones and an example is "Airports". 

