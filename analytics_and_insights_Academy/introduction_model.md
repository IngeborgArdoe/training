#Analysis and Data Mart introduction

In this course the participants will use **Data Mart** and **Analysis** tools in **Genus Apps**, on a predefined data model, to get first-hand experience on how to discover new information and knowledge from existing data. 

Analysis and data mart go hand in hand. Data mart is the structure and content of data, while analysis is the visual representation of the data. This course starts with basic implementation of analysis, continues to data mart, then touches on more advanced analysis, before finally looking at finishing touches to both analysis and data mart.  

##Data model 
The data model used for this course represents New York City Yellow Cab taxi trips. The timespan is set to the first four weeks of 2017. The model includes the classes in the following list:

* Yellow Trip
* Borough
* Community District
* Payment Type
* Taxi Zone
* Weekday
* Day


The main object class is Yellow Trip, where each instance/row represents a single trip. Each trip has information on pick-up and drop off location, time and zone, and includes details on different payment amounts, payment type, duration of the trip and number of passengers. 

The pick-up and drop off taxi zones consists of 265 different areas, such as "Jamaica Bay" and "Chinatown". Each taxi zone is connected to a larger community district, and to an even larger borough, such as "Bronx" or "Brooklyn".


