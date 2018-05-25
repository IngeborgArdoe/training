## Exercise 4 - Tables
You will now make a Table that lists all contact persons associated with the logged in user. The Table will have to be made available as a shortcut in the navigation pane. 
1. Create a new Table and name it «Contacts»
   *Guidance: From Studio -> User Interface -> Tables -> New (Basic Table).*
   1. Data Sources: Add "Contact". Uncheck "Private".
   2. Layout: Here you define which rows and columns you want to make available. Drag the Data Source (from the right menu) into Rows. Then, drag fields First Name, Last Name, Mobile, Mail, Responsible, State, Position, Created and Modify into Columns.
   3. Views: A View is a customization of the Layout, including filtering of data, search settings, etc. When you publish a table, either in a form or in the navigation pane, you will utilize a View.
	  1. General: Change the name of the View to "My Contacts". Under Columns, uncheck Visible on the Created and Modified fields.
	  *Comment: The two fields will be hidden by default, but can optionally be made visible by the user.*
	  2. Data Filters: Set Default Filter on «Contact» to be "Contact.Resposible = Active User Account". Also add sorting to the View (First Name, Last Name, ascending).
	  *Comment: Default filters can be changed by the user in the client. In other words, a user can perform a search in the table and get Contacts that he/she is not responsible for. If you make the same filter mandatory (i.e. set Mandatory filter instead of Default filter), the table will always be limited to Contacts that the user is responsible for.*
	  3. Search: Check Enable Search and add Contact as a Data Source.
	  *Comment: This makes it possible to search for Contacts in the «My Contacts»-list.*
	  4. Filter Pane: Check Show Filter Pane and add Contact to Date Sources.
	  *Comment: This allows the user to see the Default filter at the bottom of the client when the «My Contacts»-list is opened.*
   4. Events:
	  1. Add an event for opening the Contact-form by double-clicking a row ("Open in a New Window").
		 *Guidance: Command and Event are put together in Tables. Set Effect Type = "Open a Form", Effect = "Contact" and Menu = "Open in New Window". Additionally, the Data Filter must be set in accordance with the screenshot below:*
        ![oppg4fig1.JPG](media/oppg4fig1.JPG)
	  2. Add an event for creating a new Contact.
	  *Guidance: Name = "New Contact", Symbol = #1081, Enabled = "Yes", Visbility = "Yes", Menu = «New». Set Create Data in accordance with the screenshot below:*
      ![oppg4fig2.JPG](media/oppg4fig2.JPG)
2. Save and close the table. Navigate to Studio -> Navigation Pane. Right-click on "Companies", and add a Shortcut pointing to the Table that you made (Table: Contacts, View: My Contacts). Click Next. Change the name to "My Contacts", so that the name of the shortcut shown in the navigation pane matches the view. If you like, you can also add an icon to the shortcut. Click Finish.
3. Deploy to yourself and verify that you can see all your contacts (Note: you may have to put yourself as responsible for some of them first). Check also that you can open and create Contacts.
4. As a last addition, we wish to highlight inactive contact persons by coloring the rows gray. Navigate to Layout and mark the Row («Contact»). In the menu on the left, open Automatic Formatting and add a new rule named "Inactive". Finally, select some kind of gray as Foreground and use "Contact.State = Inactive" as Condition.
5. Deploy again og verify your latest modification by setting a contact person to "inactive" in the client.


<table>
   <tr><td><a href="exercise-03.md"><- Previous exercise</a></td><td align="right"><a href="exercise-04.md">Next exercise -></a></td></tr>
</table>