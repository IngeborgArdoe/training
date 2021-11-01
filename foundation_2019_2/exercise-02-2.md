####5. Contact's Data Properties

Modify the following settings on the Data Properties of Contact (double-click on a Property):
1. Company, First Name and Last Name: Tab «Data Validation», uncheck «Allow blank value». In effect this makes the fields mandatory.
2. Created Date:
   1. Tab «Security», check «Read». The field becomes Read Only for the end user.
   2. Tab «Data Calculation»: Set Default = Time Stamp. The value of the field is set to the server's current time when the Contact object is created, and cannot be edited later.
3. Created By: Add the same Security as Created Date, but set default value to «Active User Account Stamp». The value of the field is set to the logged in user that creates the object, and cannot be editet later.
4. Modified Date:
   1. Tab «Data Calculation», set Formula = Time Stamp. Formulas are updated at all times. By using "Time stamp" instead of "Now" here, the time is set every time the object - in this case, the Contact - is saved.
5. Modified By: Same Security as Modified Date, but set Formula = Active User Account Stamp. The value of the field is set to the logged in user everytime a change on a Contact is saved.
6. State: Tab «Data Calculation»: Set Default = Active. The state of the Contact is set to Active when it is created. The state can be changed later. Note also that the field is of Data Type int. The state is stored in the database as an integer, but is mapped to the Code Domain in Genus called «Object State», which translates 1 to «Active» and 2 to «Inactive». You will be able to see this by right-clicking the object class «Object State» -> Open -> Data Entries.

The object «Contact» is now almost done. The last step is to assign a few properties to the object class «Contact» itself.

####6. Modify settings on Object Class Contact

Right-click on Object Class «Contact» -> Open.
1. Tab «Auditing»: Check "Enable auditing" and then "Mandatory" on "Modify". Press Apply. This allows the user to right-click on a Contact in the client to look at its change history (which user has done what).
2. Tab «Data Sorting»: Click Add.. and select First Name and Last Name. This will by default sort Contacts automatically by their first name and last name wherever Contacts are listed (e.g. tables, grids) without any sorting specified.
3. Tab «Data Filtering»: Under "Auto Complete", click Add.. and select First Name, Last Name and Mail. This allows the user to type in a part of a Contact's first name, last name or e-mail in any field of type Contact, and hit Tab to lookup contact persons that match the written text.
4. Tab «Data Integrity»: Click on Change under "Uniqueness Constraint", and then Add. In the window that opens you can set uniqueness requirements for the creation of contacts. Here you can for example say that "if e-mail has a value", check if another contact person with the same e-mail exists, and if so, qive a warning to the user.

   *Guidance: See screenshot below:*

   ![oppg2fig5.JPG](media/oppg2fig5.JPG)

   In this case it will generate an SQL query that checks (prior to saving) whether a Contact in the database has the same e-mail address as the one you want to store, or not. If the query returns true, the user will get a warning. Notice that we have allowed the user to store the Contact nevertheless, as the "Notify user and ask for confimation to proceed"-box has been checked. By selecting the option above, however, you will deny users to store Contacts with identical e-mail addresses. 


5. **Click OK.** The object «Contact» is now complete and ready to be included in the interface (and optionally get additional functionality).

Note that you can go back and modify the properties of an Object Class/Object Class Property at any time, with a few exceptions (e.g. Data Interpretation of an Object Class Property; if you want to change this, you will have to delete the property and add it again). You can obviously also add new Object Class Properties to an Object Class after creation (e.g. you want to add Photo to Contact). Then you will have to run the wizard «Add object class properties», which is available in Studio by right-clicking on an Object Class. Remember to expand the table in the database first.

####7. Add field Responsible (user) to Contact.
1. Create a new field called Responsible on Contact.

   *Guidance: A column must be added to the database first. Do this by running the SQL statement «alter table Contact add ResponsibleUserID uniqueidentifier». Navigate to object class «Contact» -> Right-click -> «Add Object Class Properties..». Click Next in the first dialog window. In the second, Genus reads all columns from the table that has not modelled yet. Click Next. Under «Property Definitions», double-click on the row and change the Data Interpretation to «User» (make sure you change the Display Name to «Responsible» afterwards). Click OK and Finish.*

2. Set Default value of Responsible to «User (User Account)» (Active User Account).

   *Guidance: Note that this is not the same as «Active User Account Stamp». «Active User Account Stamp», like «Time Stamp», means that the default value is set server-side, and can hence not be changed from the client. Choose instead F3 (see screenshot below) and pick «User (User Account)» which corresponds to the logged in user on the client.*

![oppg2fig6.JPG](media/oppg2fig6.JPG)

####8. Replace Draft Object with Object Class

The Draft-object that you made in Exercise 2.2 is no longer needed. Navigate to Object Class Diagram -> Right-click on Draft-object «Contact» -> «Replace Draft». In the dialog box, select object class «Contact». This will remove the Draft-object from the view and replaced it with modeled object class «Contact».


<table>
   <tr><td><a href="exercise-02-1.md"><- Previous</a></td><td align="right"><a href="exercises3-5.md">Next -></a></td></tr>
</table>
