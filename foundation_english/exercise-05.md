## Exercise 5: Actions in Genus Apps

### Commands and Events

In Genus Apps, Commands are used to specify effects that will happen in a form. A Command can be started/triggered by an Event or from the Ribbon. It can be of various types, such as «Open a Form», «Apply Changes», «Delete Object» or «Run a Task». Several Commands can also be put (Combined) together, and a Command can call another Command.

You can trigger a Command with an Event by for example adding the Event «On Click» to a button and point it to the Command. When the button is clicked, the actions defined by the Command is executed.
When doing the exercises below, it may seem natural to place the Command on the same control as the Event that points to it. This will work brilliantly, but we often choose to place the Commands on a different level due to reasons we will have a closer look at in Exercise 5: Ribbon. The Ribbon is also the reason why we typically pick a symbol for each Command and change their names, e.g. from Name: Open Contact to "New Contact". 
  
####1. Add Contact actions to the Company-form:

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
   3. Command: Open Contact
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
7. To test what you have done so far: In Genus Studio, select File (at the top) -> Deploy to this computer. All changes are now deployed to your own computer for testing. Open the client (or restart it if you already have it open) and try to add, edit and/or delete a Contact from a Company. Since we haven't define a Ribbon yet, you will have to click the close button ('X') and "Yes" to save. Check also that the default values on creation are as expected.
   
   *Comment: If this had been a test or production environment, you could have chosen "Deploy to all" with a defined time. Changes would then become available for all users of the soultion.*
   
####2. Create lists of Activities and Mail on Contacts (with functionality)

1. Add a new field to Object Class «Activity» named "Contact".
   *Guidance: Add the field to the database by running SQL statement:
   
   ```
   ALTER TABLE Activity
   Add ContactID uniqueidentifier 
   ```
   
   This adds a column ContactID to the Activity-table in the database, with data type identical to the primary key of Contact).*
   Then, right-click on Activity in Studio and choose «Add Object Class Properties». Remember to set the Data Interpretation under «Property Definition» to «Contact»
2. Add a new field called "Contact" to Object Class «Mail».
   *Guidance: Same as exercise 3.4 above (substitute "Activity" with "Mail" in the SQL query)*  
3. Make Activity.Contact available in the user interface.
   1. Open form Activity, and include property "Contact" - from the Activity data source - to it as a field (ComboBox) below Company.
   2. The drop-down should be limited to show only Active Contacts belonging to the Company of the selected Activity. Hence, you will have to define the field's Data Restriction.
      *Guidance: See screenshot below:*
   ![oppg3fig8.JPG](media/oppg3fig8.JPG)
4. Add activity-functionality to the Contact-form. First, you will have to make a list of all Activities associated with a contact person. Secondly, you will have to make it possible to register Activities on a contact.
   1. Create a list (grid) of activities in the «Activities»-tab (Contact-form).
      *Guidance: You will have to add object Activities to the form's list of data sources. Define its data filter (read Activities where Activity.Contact = Contact and Activity.State <> Canceled), and add a Grid to the Activities-tab. The grid needs to bound to Data Source «Activity». Remember also to select Columns and determine Sorting (e.g. descending Due Date). Try Grouping (on State) as well if you want to.
   2. Add a Command to the Activity-tab for opening Activities:
      1. Command: Open a Form
      2. Name: Open, Tip: Activity
      3. Remember filtering!
      4. Add an Event = Context Menu Item Click: Open in New Window to the grid which executes the above Command.
   3. Additionally, create a Command + Event for «New» and «Delete». Place them on the Activities-grid. Remember to set Default values on «New» so that Activity is connected to both Contact and Company. Symbols #1198 and #1195 should suit «New» and «Delete», respectively. If you need inspiration, go back to exercise 3.3.
   4. Deploy the solution to yourself and check that you are able to create Activities on a contact person.
5. You will also have to list Mails associated with a Contact. The way of adding instances to the Mail-list in the Company-form is to paste new Mail from the Clipboard (i.e. drag-and-drop). You will make this functionality in a later task, so for now, you only need to focus on the list itself and how to open an e-mail from it.
   1. Create a list (grid) in the «Mail»-tab of form «Contact» that shows Mail where Mail.Contact = Contact.
   2. Add a Command of type "Invoke a File" to the Mail tab control. Next, add an Event to the grid that executes it (Type="On Contect Menu Item Click", Menu Item="Open in New Window").
      
      *Comment: This allows the Mail to open in Outlook when a row has been double-clicked. If the object class contains File Data, File Size, File Type and File Name, the "Invoke a File"-effect will open it in its "default" program. You can look at how this is done in the Mail-grid of the Company-form.*
   
####3. OPTIONAL: Add a Contact Log to Contact

This exercise is not strictly necessary for the remaining set of tasks. However, it contains an interesting new consept - «Part of composition» - ~~so we recommend you to at least read through it~~.

We want the user to be able to write and add lines to a Contact log (similar to «Company Log» which exist under Company).
1. Create a new Object Class called "Contact Log". When you run through the wizard to add the new Object Class, remember to define the Data Interpretation of Created By (User) and Contact (Contact). In the last step of the wizard, choose Part of Composition "Contact".
   *Guidance: You can use the following SQL query to create the database table:*
   
   ```
   CREATE TABLE ContactLog (
    ContactLogID uniqueidentifier PRIMARY KEY,
    "Subject" varchar(1000),
    CreatedDate datetime,
    CreatedByUserID uniqueidentifier,
    ContactID uniqueidentifier
    )
   ```
   
   By setting Contact Log to be part of Contact's composition, Contact Log data will always be read together with Contact, and inherit both security and audit trail from it. Set it up like the screenshot below:
![oppg3fig9.JPG](media/oppg3fig9.JPG)
2. Assign Default values to Created By and Created Date, and set Subject to "required".
3. Make a form «Contact Log».
   1. This should only have one single Data Source: Contact Log (remember to uncheck Private and set Max Occurence = Allow one object).
   2. View (properties): Change Style to "Dialog Box" and Buttons to "OK and Cancel". Set Alignment = "Fixed", Width = 800 and Height = 400. *Comment: The reason for chosing "Dialog Box" is that we don't need a save-button in this form. It will be opened modally from the list of Log objects on Contact, and by clicking OK, the form will be closed and changes saved in the Contact-form instead.*
   3. View: This should only display the «Subject»-field. Drag it into the view, and change the following properties of the field:
      1. Check Multiline and Word Wrap
      2. Set Vertical Alignment to «Stretch»
      3. Set Label Position to «Top».
4. Add Contact Log to the Contact-form. 
   1. Add a new GroupBox inside the RIGHT GROUP BOX that you made earlier (which perhaps is a Group now?). Give it label "Log:", and check property Transparent Title Area. Set Border Thickness to 0.
   2. Add a grid inside the GroupBox. Bind the grid to Data Source «Contact» and Field «Contact Log». Select Columns to show and define the Sorting (Created Date, descending). **NB: You may need to re-start Genus Studio to do this!**. *Comment: Since Contact Log is part of composition and we don't need to filter out anything, Contact Log don't have to be a Data Source on its own. The grid is now bound to the group of log objects that is "attached" to the Contact in the Data Source.* 
   3. Add a Command to the ContactLog-grid for opening a Contact Log (through form «Contact Log»). This should be enabled if Contact.Log.Single Selected has value. Also add an event to the grid which executes the command.
      *Guidance: As the «Contact Log»-form is a dialog box, it can't save changes on its own. Accordingly, choose Two-Way binding (as shown below) when setting up the Event.
   ![oppg3fig10.JPG](media/oppg3fig10.JPG)
      Data Binding: 
   ![oppg3fig11.JPG](media/oppg3fig11.JPG)
   4. Add also a Command and an Event for New and Delete, respectively. Place both the commands and the events on the Contact Log grid itself.
      1. New: *Guidance: The opening of Contact Log in "Create"-mode is also two-way bound. Consequently, a new object is created in the Contact Log-form, but is not saved before the object is brought back to the Contact-form and the Save-button is pressed. See screenshot below:*
      ![oppg3fig12.JPG](media/oppg3fig12.JPG)
      2. Delete: *Guidance: Se screenshot below: (Command)*
      ![oppg3fig13.JPG](media/oppg3fig13.JPG)
5. Deploy and test creation, modification and deletion of a Contact's log objects in the client.
   

<table>
   <tr><td><a href="exercise-03.md"><- Previous</a></td><td align="right"><a href="exercise-05.md">Next -></a></td></tr>
</table>
