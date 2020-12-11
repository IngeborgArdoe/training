## Exercise 5.1: Actions in Genus Apps

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
   
   *Comment: If this had been a test or production environment, you could have chosen "Deploy to all" with a defined time. Changes would then become available for all users of the solution.*

<table>
   <tr><td><a href="exercise-04.md"><- Previous</a></td><td align="right"><a href="exercise-05-2.md">Next -></a></td></tr>
</table>
