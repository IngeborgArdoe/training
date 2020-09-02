## Exercise 3.2 - Forms

####2. Create a list of Contacts within form «Company».

You will now add a list to the Company-form that shows all associated Contacts (using a grid). You will also make actions to create new Contacts and open existing ones.
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
