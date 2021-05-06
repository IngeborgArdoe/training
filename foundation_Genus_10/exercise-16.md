## Exercise 16 - Miscellaneous

This optional exercise contains various extensions to improve you CRM solution. As always, we recommend you to at least read through it.

####1. OPTIONAL: Create views for "My Activities" and "My Recently Completed"

Define 2 new views in the Activities-table for "My Activities" and "My Recently Completed" which list non-completed activities that the user is responsible for and activities that was completed the last 3 months, respectively. Add shortcuts in the Navigation Pane (under "Company") and rename menu "Company" to "CRM".

*Tip: A quick way to make a new "almost identical" view is to right-click on an existing view and select "Copy".*

####2. OPTIONAL: Create a view for "My Customers"

Add a new view in table "Companies" called "My customers". This view should show customers/companies that the user is responsible for or companies where he/she is responsible for the Contact. Add a shortcut in the Navigation Pane.

####3. OPTIONAL: Define Search Properties on Contact/Request

1. Make object class properties Company, First Name and Last Name available as search fields in the search panel found above the list of Contacts that you made.

   *Guidance:*

   *Open object class Contact, navigate to tab "Search", and Click "Modify". Add the properties that you want to be searchable (Company, First Name, Last Name). Deploy and verify that the three properties can be searched for in the Contacts table.*
   
2. Do the same for object class Request. Add search properties that you find meaningful. 

####4. OPTIONAL: Add Data Validation on Contact.Mail

Add a data valididation on property Mail (object Contact) that notifies the user if the field is blank (NULL). We don't want to force it to have value, but we want the make the user aware that this is a field that "should have a value".

*Guidance:*

Open the Mail property on object class Contact, navigate to Data Validation and click Add:
* _Add condition "Contact.Mail has no value"_
* _Check "Notify user and ask for confirmation to proceed (invalid value, but possible to proceed)_
* _Check "Notification Message" and type something like "Mail should be set for all users"._
* _Disable "Show in dialog box" and enable "Show in screen tip"._

Deploy and check how the Mail-field behaves in the Contact-form.

####5. OPTIONAL: Create a new security group "Key Account Managers". 

Add Super Users as a member to a new security group that you call "Key Account Managers". Make fields "Is Customer", "Annual Sales" and "Annual Revenue" on Company editable only by Key Account Managers, but visible for the rest (Users).

*Tip: In order to set security per Object Class Property on group level, check "Allow granting of permissions for property" in the Object Class Property's Security tab. Afterwards, set permissions under Security (left menu in Studio) -> Permissions.*

####6. OPTIONAL: Add Explore functionality 

Add the possibility to Explore other related objects from Company, Request and User (Object Class -> Explore -> Browse Paths).

* Company -> Activities, Contacts, Mail og Documents
* Request -> Companies, Contacts, Documents og Mail
* User -> Activities (responsible), Companies (responsible), Contacts (responsible), Documents (created/modified by), Mail (created by), Requests (responsible)

*Tip: This makes it possible to explore related data (menu "Explore") when a user for instance selects a list of Companies. You will have to set it up in the "Explore"-tab under "Browse Paths" among the properties of an Object Class. If a user explores Companies, Contacts should for example be listed - but first Genus needs to know which Contacts-list to use. If you open the properties of Company or Contacts in the provided solution (tab "Explore" under "Views"), you will see that a "default view" is selected. This is the view that is used when the user "Explore" (either from the Explore menu, or when the user double-clicks on a number in a report to see the underlying data). Take a look at the provided solution if needed.* 


<table>
   <tr><td><a href="exercise-15.md"><- Previous</a></td></tr>
</table>
