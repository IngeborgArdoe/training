## Exercise 5.2: Actions in Genus Apps
   
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
   *Guidance: Similar to above - but for Mail, not Activitiy : )  
3. Make Activity.Contact available in the user interface.
   1. Open form Activity, and include property "Contact" - from the Activity data source - to it as a field (ComboBox) below Company.
   2. The drop-down should be limited to show only Active Contacts belonging to the Company of the selected Activity. Hence, you will have to define the field's Data Restriction.
      *Guidance: See screenshot below:*
   ![oppg3fig8.JPG](media/oppg3fig8.JPG)
4. Add activity-functionality to the Contact-form. First, you will have to make a list of all Activities associated with a contact person. Secondly, you will have to make it possible to register Activities on a contact.
   1. Create a list (grid) of activities in the «Activities»-tab (Contact-form).
      *Guidance: You will have to add object Activities to the form's list of data sources. Define its data filter (read Activities where Activity.Contact = Contact and Activity.State <> Canceled), and add a Grid to the Activities-tab. The grid needs to bound to Data Source «Activity». Remember also to select Columns and determine Sorting (e.g. descending Due Date). Try Grouping (on State) as well if you want to.*
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
   <tr><td><a href="exercise-05-1.md"><- Previous</a></td><td align="right"><a href="exercise-06.md">Next -></a></td></tr>
</table>
