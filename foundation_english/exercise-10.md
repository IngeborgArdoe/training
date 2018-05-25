## Exercise 10 - Business Intelligence
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction of the topic. The session will concern Genus App's report functionality.* 

In Genus Apps, we have a product called "Genus Discovery". This is a report and analysis tool. The report part is mainly used for setting up predefined reports that benefits the end user.

The tool can also be made available from the client, so that dedicated groups of end users can set up or modify reports/analysis themselves.

You will now go through a couple of exercises concerning the creation of reports. **A brief summary of Genus Discovery's report functionality is described here: *

*A new report is created from Genus Studio -> Discovery -> Reports -> New. The tool's structure is logically set up as shown below:*
![oppg10fig1.JPG](media/oppg10fig1.JPG)
 
*To make an Object Class available as a dimension in a report, you will have to specifically set it as property of the Object Class (right-click on the Object Class -> Open -> Data Aggregation). If you want to count on a Measure (ref No Of Activities in exercise 9), an Object Class Property with the same name - having "Enable as Measure" checked - must exist (look at the Data Aggregation properties of Activity.No of Activity - the "Enable as Measure" option should be checked).* 

In addition, you will have to specify how to group No of Activities per month, as this can be based either on «Created date» or «Completed date». You will have to set up these kinds of links ("Connections") in the report.

Connections that will become available in the report are defined under Object Classes in Studio:
![oppg10fig2.JPG](media/oppg10fig2.JPG)
 
*Note: You don't have to specify the link between Activity and Company, as Activity has a Company-field (the tool understands). However, if No of Activities is to be grouped by for example Country, you will have to create a Connection from Activity to Country through Company.

In the report, you can set up connections from No of Activities to the "Month" and "Company" dimensions by right-clicking No of Activities -> Connections:*
 ![oppg10fig3.JPG](media/oppg10fig3.JPG)

As you can see, we also added a "Local Filter" which selects only Activities with State="Completed" to the report.

Note also that when you are working in Genus Discovery, you are working in the client. Accordingly, if you for example add a new connection to an Object Class, you will have to deploy in order to make the Connection available for reports.

1. Create a new report "Activities per Company Speciality YTD". The report should count the number of completed activities per month per Company Speciality so far this year. It should also sum the number of activities both horizontally and vertically, and be presented to the end user either as a table or as a line chart.

   *Tip: You will have to set up a new Connection from Activity to Company Speciality (through Company). You also need to make Object Class Company Speciality available as a dimension in reports (i.e. check the "Allow this Object Class to be used as a dimension when aggregating data" option under the object class' Data Aggregation properties).*

   In order to sum data, right-click on "No of Activities" in the report -> Series Calculation and choose to sum over both Month and Company Speciality. Check "Calculate intersections" in both sum functions to get the "sum of sums" (i.e. sum of activities for all Company Specialities for all months YTD) in the bottom right corner:
  ![oppg10fig4.JPG](media/oppg10fig4.JPG)

  
   You can control which buttons to show in the report by checking/unchecking them in the "Buttons" menu (upper right). Allow the user to shift period back and forth. In addition, check Explore, Normal view (table), Line (line chart) and Filter Pane. By adding both Normal View and Line, the user can choose to see the trend as a line per Company Speciality or as a table per month per Company Speciality.

   *Comment: We haven't said anything about the setup of "No of Activities" as an Object Class Property yet. If you open Object Class Property "No of Activities" from Studio, you will see that the field is of type "function". In other words, the field is not refering to a specific column in the database (Provider Name), but is instead calculated. The value is set according to the RDBMS expression ("\*") defined in the Data Calculation tab and the aggregation method ("count") selected under Data Aggregation. When "No of Activities" is used as a measure in a report, a SQL statement "select count(\*) from.." grouped on the report's dimensions is executed.* 

2. Create a new report "Sales per Company last 3 months". The report should have measure "Order Value NOK" and dimensions "Month" (select last month and two months back) and "Company". Only Requests of type "Order" and state "Closed" should be shown, and the connection against month should based on Received Date.

   *Tip: You need to make Request.Order Value NOK available as a measure first. In addition, you will have to make a Connection from Request to Month. There is a shortcut for doing the latter in Genus: Right-click on Received Date -> Create Calendar Connection. You also need to make sure that object class Request is available as a dimension (Data Aggregation).*

3. Create a report "Company Benchmark" which shows measures "Annual Sales" and "Employees" from Company, and utilizes Company as vertical dimension to show a Plot diagram.

   *Comment: Take a look at the provided solution if needed. This report can be used to distinguish between companies with potential and companies to keep away from. As the diagram shows all Annual Sales plotted against Number of Employees for all companies, a point "above the curve" is a company doing well (i.e. generates a lot of revenue per employee).*

4. OPTIONAL EXERCISE: Create a report "Sales and Activities per Employee YTD" which has No of Activities, Sales (from Request.Order Value NOK) and Avg Sales per Request (formula based on Order Value NOK / NO of Requests).

   Add also a Measure (formula) "Sales Increase" that shows the increase or decrease of sales relative to last month.

   *Tip: You need to make a new Object Class Property on Request: No of Requests (equivalent to No of Activities). To be able to calculate Avg Sales per Request, you must use a Formula in the report tool. In a Formula, you can set up an expression based on the published Measures of the report (under "Values"). Accordingly, you will have to add No of Request to the report and make it Hidden. 

   To make a formula for Sales Increase, you will need a Measure that shows Sales last month: Copy "Sales" (right-click -> copy), rename it to "Sales (last month)", navigate to the "Period Shift" setting and add "-1" (minus one). Then, make a Formula "Sales - Sales (last month)".

   Make sure that the Sales measure only includes Requests in state "Closed" and of type "Order". You can do this "per measure" (right-click -> Local Filters) OR you can add Request State and Request Type to the "Filters" section of the report and define filters here. Measures that are connected to any (or all) of the latter filter objects will be filtered accordingly. If you don't want to define Connections every time you are using the sales measure, you can - in the Data Aggregation tab of Object Class Request - set up default connections. These are connections that will be set automatically in reports.*

5. **OPTIONAL EXERCISE: Add shortcuts to the reports in Navigation Pane.**

   *Comment: All reports (given that you have the rights to see them) are available from the Discovery menu in the client. In some cases, however, it can be useful to create shortcuts to reports in the Navigation Pane (e.g. reports are of high importance or are frequently used). Take a look at the provided solution if you want to see how reports have been published there.*

   
   </br>
<table>
   <tr><td><a href="exercise-09.md"><- Previous exercise</a></td><td align="right"><a href="exercise-11.md">Next exercise -></a></td></tr>
</table>