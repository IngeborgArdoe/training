## Exercise 5.1: Actions and Events





### 3.2.3 Create Action for New Contact
In order to create a new Contact, we need to create a Client Action which creates a new Object and allows for user input. This action will be available within this module.

1. Navigate to Client Actions and add new, name it "Add new contact".
2. Go to Action Flow. Navigate to "Effects" on the left hand side. Add a Scope Block by double clicking or dragging it into the working area.
Now we want to Create a new Contact which will be edited in the "Contact Details" Form we created initially. The Form is a type of Page, and we add a "Navigate to Page"-effect into the scope. Select Contact Details as the Page.
3. In the Data Filter-section, click the menu and select "Create Object". Some values here are preset, and some must be given as input. Some can be left blank for the user to fill in and some, like State, should have default values (State = active) which can be edited by the user later. Note that Company is mandatory and blank. As we plan on trigging this Action from the Company form, we will know which Company we want to fill inn here and should send it in as input to the action.

  ![Exc2fig7.JPG](media/Exc2fig7.JPG)


4. Navigate to Data Sets and add a Data Source for Company in the Public Interface section. Keep Flow set to In, since we want to receive this information *from* the Company Form. The Company Data Source does not have to be Required. We may want to trigger this action other places within the Company Module where the Company is not pre-defined from context. In these cases, Company value can be set within the "Company Details" Form, along with values such as first name and last name.

5. Return to Action Flow. Re-open the "Create Object" data filter. In the menu for the Company field, choose Select Field and choose the Company data source you just added.

6. Save and close.

  Create Object           |  Data Source selection
  :-------------------------:|:-------------------------:
  ![Exc2fig8.JPG](media/Exc2fig8.JPG)  | ![Exc2fig9.JPG](media/Exc2fig9.JPG)


<!-- <p float="left">
  <img src="media/Exc2fig8.JPG" width="300" />
  <img src="media/Exc2fig9.JPG" width="200" />
</p> -->

### 3.2.4 Utilize Action to Create New Contact

6. Re-open the Contacts View. Navigate to View, open the Control View (Ctrl+Shift+L) and mark the top level - Contacts.
7. In the Page-section on the right hand side. Click "Action Bar". Here, you can see built-in actions, as well as the Client Actions defined in the Module. Select "Add New Contact", set the label to "New" and an appropriate Icon (e.g. Basic-Contacts" or "Basic-AddButton". In the Data Exchange, we can see the Company data source defined in the Action. In order to send data into the Client Action, we need to define a corresponding data source in the View.
8. Close the Action Bar Editor and navigate to Data Sources. Add a Public Interface Data Source for Company. As in the View, the Data Source should be single occurrence and not Required.
9. Return to the Action Bar editor. Mark the "New"-action and click the Data Filter. Set the newly defined Company Data Source as input. While we're here, add another action to the action bar. From the built-in actions, select "Save changes". Rename to "Save" and set the icon "Save-fluent". Save and exit.

  ![Exc2fig10.JPG](media/Exc2fig10.JPG)

10. Refresh the app in your browser. Navigate to a Company, click the Contacts-tab and Add New. As you can see, the Company field is already filled in. Add First and Last name, and optionally email or mobile.

11. When you return to the Company page, we see the new Contact in the Contact Tab. However, nothing happens when we click the row. We need to add functionality for showing Contact information when a row is activated/clicked.


### 3.2.5 Open Contact Information
12. Return to the Client Actions-section and create a new one named "Navigate to Contact". In Action Flow, add the "Navigate to Page"-effect. Now we need a data source to filter into the Page.

13. Navigate to Data Sets and add Contact as a Public Interface Data Source. Set Occurrense to One and Required as Yes. If we do not have a Contact to show, we do not want to navigate to the Contact page.

14. Add the Contact Data Source to the Data filter for the "Navigate to Page"-effect by transferring all.

15. Return to the Contacts view. Mark the Table-level in the Control view (optionally: mark a column and press esc).

16. On the right hand side Navigate to the "On Activate"-dropdown. Select the Client Action you just created "Navigate to Contact"

17. Set the data exchange to Contact (0:n) from the view. The view will read the correct Contact/Row from context.

18. Save and refresh your browser.
19. Navigate to your newly created Contact via Company.



<table>
   <tr><td><a href="exercise-03-1.md"><- Previous</a></td><td align="right"><a href="exercise-04.md">Next -></a></td></tr>
</table>



####1. Add Contact events to the Company-form:

You will now add functionality to open, create and delete Contacts from the Company form.
1. Add a command to open an existing Contact. Place the Command on the Contacts-tab by selecting the tab (you can mark the Contact grid and press Esc), and - under Properties - clicking Commands. In the dialog box, click Add.. Open a Form
   1. Name: Open
   2. Tip: Contact (this tip is only visble for modelers)
   3. Effect: Contact (the form to open)
   4. Data Binding: Default (One Way. If Two-way is chosen, the form will open modally and changes will be brought back to the Company-form where they will have to be saved with the Save-button)
   5. Filter Data: Select "one way binding to objects in the data source". Click on Modify. In the dialog box, you will have to choose the data source to filter against (Contact) and "Single Selected". This allows the one active (selected) row in the Contact-grid to be filtered into the Contact-form. Check also the "Enable Browse Object"-box (makes it possible to use the up / down arrows to browse through a list of contact persons).
2. Create an Event for executing the above command. We want the Contact-form to open when a row in the Contact grid is clicked, so place the Event on the grid itself (select the Contact-grid -> click the Events-property):
   1. Type: On Context Meny Item Click
   2. Menu Item: Open in a New Window (the event, which by default triggers «Open in a New Window» in Genus, will happen when a row is double-clicked.
   3. Command: Open (The Command you just made)
   4. Click OK
3. Add a Command to create a new Contact. Place it on the Contacts-tab.
   1. Name: New
   2. Tip: Contact
   3. Type: Open a Form
   4. Effect: Contact
   5. View: Default (Contact)
   6. Data Binding: Default (One Way)
   7. Create Data: Click … and push Add. Under Default Values you will have to set Contact.Company = Company (in other words, the new Contact's Company will be set to the Company that you have open when the "New"-button is clicked).
   8. Assign a symbol: This will turn out to be useful later. You will find a suitable symbol if you search for "1081". Notice that you can choose both a main symbol and an "overlay". Try putting on an overlay. Before you push OK, right-click on the overlay and hit "Clear".
4. Add an Event to the Contacts-grid for creating a new contact.
   1. Type: On Context Menu Item Click
   2. Menu Item: New
   3. Command: New (The Command you just made).
5. Add a Command to the Contacts-tab that deletes selected Contacts.
  *Guidance: Look at the «Delete»-command which is placed on the ActivitiesTab-tab. In our case, the Delete-command should have Data Binding against Data Source «Contact». Tip: Use symbol #1195, and choose Enabling = Conditional with condition "Contact.Selected Objects has value" (illustration below).*
![oppg3fig7.JPG](media/oppg3fig7.JPG)

6. Add an Event to the Contacts-grid for deleting contacts.
   1. Type: On Context Menu Item Click
   2. Menu Item: Delete
   3. Command: Delete (The Command that you just made).
7. Restart Genus Desktop in order to try the new functionality for adding, editing and/or deleting a Contacts from a Company. Since we haven't define a Ribbon yet, you will have to click the close button ('X') and "Yes" to save. Check also that the default values on creation are as expected.

   *Comment: In order to publish the changes to other users you would have had to deploy the blue or green namespace. This can be done under the "Deployment"-menu item in Genus Studio. Either the blue or the green namespace can be set as the active namepace - the namespace end users are using. When the active namespace is deployed the new appmodel becomes available for the end users.*

<table>
   <tr><td><a href="exercise-04.md"><- Previous</a></td><td align="right"><a href="exercise-05-2.md">Next -></a></td></tr>
</table>
