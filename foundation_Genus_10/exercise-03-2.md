## Exercise 3.2 - Forms

####2. Create a list of Contacts within form «Company».

You will now add a list to the Company-form that shows all associated Contacts. You will also make actions to create new Contacts and open existing ones.


1. Navigate to Pages in the Company module. Add a New Page -> View.
2. Name the View "Contacts" and choose Master Data Source = Contact.
3. Navigate to View and drag relevant data fields into the View.

4. Navigate to the "Company"-form -> Form.
In the lower section, mark the Tab Control with Logs and Mails.
Click on Pages in the right hand Tab Control edit.
Add a Page and set target to your Contacts View, and set an appropriate name and title.
5. Click the data filter and the menu for the Contact data source. Choose "Read Related".
6. Select to filter objects on the Company source data set. Make the filter to read Contacts related to the Company by defining the connection between then in the "outbound field in target" section. This defines the relationship required between the Company from the Form and the Contact list. Because one Company may have several Contacts, it is a One to Many Relationship (One Company and many Contacts).

7. Save and refresh the app.

8. Now that we can view the table with relevant contacts, we want to be able to view more details about a single contact or even create a new one.



9. On Activate on View
10. Client Action and Context Menu for New (use Page)

1. In Studio, navigate to User Interface -> Forms. Open «Company».
2. Add a new tab to the Tab Sheet at the bottom of the form.
   *Guidance: See screenshot below*
![oppg3fig4.JPG](media/oppg3fig4.JPG)

   *Note: In the Company-form, you will see that the names of the tabs and headers are «Company Label», «Log Label», etc. Don't worry about this yet - it simply means that the label of the control is bound to the field of an object and hence shows a dynamic name (both name and the number of objects in the list is shown).*
3. Name the new tab «Contacts» (both Name and Label). Right-click the tab and select "Sort tabsheets". Move it one step up.
4. Under «Data Sources», add Contacts ("Private" and "Unbounded", as by default). In the properties menu, navigate to Data Filter. Add filter Contact.Company = Company (i.e. read only Contacts belonging to the Company in the form).
   *Guidance: See screenshot below:*
![oppg3fig5.JPG](media/oppg3fig5.JPG)
   The Contacts are filtered and read when the Company-form opens.
5. Navigate back to the tab "Contacts" and add a Grid from the menu on the right. Set the Data Binding to Data Source «Contact». Select which columns to include under Columns. Define the sorting (First Name, Last Name) under Sorting, and set Selection Mode to "Multiple" (allows the user to mark several contacts in the list).
   *Guidance: See screenshot below*
![oppg3fig6.JPG](media/oppg3fig6.JPG)
   You have now successfully added a list of Contacts to Company. Later we will add functionality to open the Contact-form that you made earlier (by double-clicking a row in the grid) and a button that allows the user to create a new Contact.   

<table>
   <tr><td><a href="exercise-03-1.md"><- Previous</a></td><td align="right"><a href="exercise-04.md">Next -></a></td></tr>
</table>
