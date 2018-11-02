## Exercise 14 - Miscellaneous

This optional exercise contains various extensions to improve you CRM solution. As always, we recommend you to at least read through it.

####1. OPTIONAL: Create views for "My Activities" and "My Recently Completed"

Define 2 new views in the Activities-table for "My Activities" and "My Recently Completed" which list non-completed activities that the user is responsible for and activities that was completed the last 3 months, respectively. Add shortcuts in the Navigation Pane (under "Company") and rename menu "Company" to "CRM".

*Tip: A quick way to make a new "almost identical" view is to right-click on an existing view and select "Copy".*

####2. OPTIONAL: Create a view for "My Customers"

Add a new view in table "Companies" called "My customers". This view should show customers/companies that the user is responsible for or companies where he/she is responsible for the Contact. Add a shortcut in the Navigation Pane.

####3. OPTIONAL: Create a new security group "Key Account Managers". 

Add Super Users as a member to a new security group that you call "Key Account Managers". Make fields "Is Customer", "Annual Sales" and "Annual Revenue" on Company editable only by Key Account Managers, but visible for the rest (Users).

*Tip: In order to set security per Object Class Property on group level, check "Allow granting of permissions for property" in the Object Class Property's Security tab. Afterwards, set permissions under Security (left menu in Studio) -> Permissions.*

####4. OPTIONAL: Add Explore functionality 
Add the possibility to Explore other related objects from Company, Request and User (Object Class -> Explore -> Browse Paths).

* Company -> Activities, Contacts, Mail og Documents
* Request -> Companies, Contacts, Documents og Mail
* User -> Activities (responsible), Companies (responsible), Contacts (responsible), Documents (created/modified by), Mail (created by), Requests (responsible)

*Tip: This makes it possible to explore related data (menu "Explore") when a user for instance selects a list of Companies. You will have to set it up in the "Explore"-tab under "Browse Paths" among the properties of an Object Class. If a user explores Companies, Contacts should for example be listed - but first Genus needs to know which Contacts-list to use. If you open the properties of Company or Contacts in the provided solution (tab "Explore" under "Views"), you will see that a "default view" is selected. This is the view that is used when the user "Explore" (either from the Explore menu, or when the user double-clicks on a number in a report to see the underlying data). Take a look at the provided solution if needed.* 


<table>
   <tr><td><a href="exercise-14.md"><- Previous</a></td></tr>
</table>
