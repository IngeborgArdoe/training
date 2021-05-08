## Exercise 4 - Views and Sitemap


You will now make a site page that lists all contact persons associated with the logged in user. The Contacts will have to be made available as a shortcut in the app sitemap with a filter applied.

###1. Create Filter «My Contacts»

1. In the Company Module, navigate to Data Filters at the bottom of the left hand side. Create a new filter named "My Contacts" with data source set to Contact.
2. Set the datafilter to filter in objects where Responsible = the logged in user.

###2. Add Contacts View to App

3. Exit the Company Module and navigate to Apps in the top left hand side in Genus Studio. Open the CRM-app, and navigate to the sitemap.
4. Add a Page to the sitemap and set the target to the view "Contacts". Set label to "My Contacts" and Icon to "Basic-contacts". Enable Search.
5. Click the Data Filters and choose Apply Data Filters -> My Contacts.
6. Save and refresh web app.



### 3. (Optional) Group Rows by Contact State

1. Return to the Contacts View in the Company Module. Mark the Table level in the Control View. In the Table Settings edit on the right hand side, set Grouping on one or more data fields (e.g. State)
2. Save and Reload the browser. 


<table>
   <tr><td><a href="exercise-04.md"><- Previous</a></td><td align="right"><a href="exercise-05-1.md">Next -></a></td></tr>
</table>
