## Exercise 5.2: More Actions and User Interfaces in Genus

###5.2.1 Create lists of Activities on Contacts (with functionality)

1. Add a new field to Object Class «Activity» named "Contact".
   *Guidance: Add the field to the database by running SQL statement:

   ```
   ALTER TABLE Activity
   Add ContactID uniqueidentifier
   ```

   *This adds a column ContactID to the Activity-table in the database, with data type identical to the primary key of Contact).*

   Then, right-click on Activity in Studio and choose «Add Object Class Properties». Remember to set the Data Interpretation under «Property Definition» to «Contact»  
3. Make Activity.Contact available in the user interface.
   1. Open form Activity, and include property "Contact" - from the Activity data source - to it as a field (Dropdown) below Company.
<!--2. The drop-down should be limited to show only Active Contacts belonging to the Company of the selected Activity. Hence, you will have to define a new data filter in the module named "Active Contacts-->
   3. Return to the Activity Form and highlight the Contact Control.

4. Add activity-functionality to the Contact-form. First, you will have to make a list of all Activities associated with a contact person. Secondly, you will have to make it possible to register Activities on a contact.
   1. Create a list (view) of activities in a new View named "Activities". Add relevant columns to the Table-section. **Set "On Activate" to "Navigate to Activity Form" and set up Data Exchange.
      **Guidance: You will have to add a view "Activities" to the the modules pages. Remember also to select Columns and determine Sorting (e.g. descending Due Date). Try Grouping (on State) as well if you want to. Consider changing the width definition for columns.**
   2. Navigate to the Contact form and hightlight the Tab Control. Click Pages and add an Item with target set to the "Activities" View, rename "Contact Activities". Set data filter to Read Related, by connecting to Contacts as a One to Many Relationship through Activity.Contact

5. We now need to be able to Create and Delete Activities. There's already a "Add New Activity"-action. Edit this as follows:
    1. Add Public interface Data Source Contact, set up the same way as Company is.
    2. Navigate to the Action Flow, highlight the Navigate to Page:Activity, and click the "Create Object" Data Filter. In the Contact Field in the Object editor, click and select "Select Field" and set the Data Source you just defined.
    3. Now, when we send in Contact as input here, we may not send in data for the Company Data Source in the Action, but we still want to auto-fill fields we can know from context. In that case we want the Company-field in the Activity to inherit the Contact's Company. Click the Company field -> Enter an Expression and enter "if company <> null then company
    else contact.company". This will use the Contact's Company as default when the Company data source is not set.

6. Return to the Activities View.

7. Add a Public Interface Data Source Contact with One occurrence.

8. Navigate to View and highlight the top level in the Control View or Esc all the way out. Click the Action Bar and add:
    1. "Save Changes" with Icon 'Fluent-Save'
    2. "Add New Activity" with Data Exchange set up for the Contact Data Source. Set Label as "new" and Icon as 'Fluent-account-activity'
8. Highlight the Table level in the Control View. Click the Context Menu-setup on the right hand side and add:    
  3. "Delete Activity" with data exchange as single selected Activity, Label "Delete" and Icon "Fluent-Delete"

4. Refresh and check your work. Check that you are able to create Activities on a contact person. Note that the Contact and Company fields are set when you open the "New Activity" window from this context.


<!--
###3. Add a Contact Log to Contact

This exercise is not strictly necessary for the remaining set of tasks. However, it contains an interesting new concept - «Part of composition».

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

   By setting Contact Log to be part of Contact's composition, Contact Log will inherit security and audit trail settings from the Contact Object Class. Set it up like the screenshot below:
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
-->

<table>
   <tr><td><a href="exercise-05-1.md"><- Previous</a></td><td align="right"><a href="exercise-06-1.md">Next -></a></td></tr>
</table>
