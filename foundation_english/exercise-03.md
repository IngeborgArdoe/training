## Exercise 3 - Forms

####1. Create a Form: «Contact»

You will now make a Form for registering and opening customer Contact information.
1. In Studio, navigate to User Interface -> Forms. Right-click -> New -> Desktop Form. Save it right away with name «Contact».
2. Data Sources (upper-left corner): This is where you add the object(s) that you want to show or utilize in the Form. Add «Contact» as a Data Source (see screenshot below). Note that:
   1. Data Source «Contact» has to be "public". Hence, uncheck the property named Private. The reason is that you want to be able to filter a Contact-object into the form (i.e. input an object to the Form, so that the form knows which contact person to show).
   2. Data Source «Contact» must be set to «Max Occurences» = "One", which means that only one Contact-object can exist in the Form. This has to be done in order to allow the properties of Contact to be shown in fields. "Unbound" is used for data sources that you want to list (e.g. in a Grid, Table, etc).
   3. This form will be used as the "master" form for showing Contacts, i.e. you can use it as the default form for showing a Contact. Hence, check the «Is Master» property.
![oppg3fig1.JPG](media/oppg3fig1.JPG)

3. Views: Go to View (Default). Change the name to «Contact».
4. Add Container «Tab Sheets». Click inside the first tab to mark the Group it contains. Change the name to "General".
  Add a new tab: Move one level out (hint: press the Esc-button), and double-click on "Group" in the Desktop Control menu. Name the new tab «Activities» (content will come later). 
  Add also a tab named «Mail» to the Tab Sheet (content will come later).
5. In tab «General», you will add the fields for Contact.
   *Guidance: You will be asked to model a «Contact log» at the right hand side of this display in an upcoming task. Hence, we recommend the following layout for the «General»-tab:*
![oppg3fig2.JPG](media/oppg3fig2.JPG)
   
   Select OUTER GROUPBOX (or whatever you called it in your solution) and change «Container Type» to «Group» in the menu on the left. This will remove the frame of the box. Do the same for LEFT GROUPBOX and RIGHT GROUPBOX. Fields can be dragged from the right menu and dropped into the form after changing the following:
   
![oppg3fig3.JPG](media/oppg3fig3.JPG)
  
   After having made the change above, you can drag Data Properties from the Contact data source into the Groups located in the «General»-tab. A proposed layout control is selected by default (e.g. TextEdit is proposed for «First Name»). If you drag Company into the form, a ComboboxEdit - which is a dropdown - is suggested. This may be unfortunate when there are a lot of objects to choose from. Instead you can press Shift while dragging the Company into the form, and you will get a SearchBoxEdit rather than a ComboBoxEdit - increasing the user friendliness.
6. The initial version of the Contact-form is now complete. You can optionally navigate to the outermost layer of the View and set Width and Height to 800 and 500, respectively. To see what this looks like, change the Alignment to "Fixed". The latter alteration prevents the end user to change the size of the window, so set Alignment back to "Stretch" before you save. 

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
   You have now successfully added a list of Contacts to Company. Next you will have to add an event that opens the Contact-form that you made earlier (by double-clicking a row in the grid) and a button that allows the user to create a new Contact.   

<table>
   <tr><td><a href="exercise-02.md"><- Previous</a></td><td align="right"><a href="exercise-04.md">Next -></a></td></tr>
</table>
