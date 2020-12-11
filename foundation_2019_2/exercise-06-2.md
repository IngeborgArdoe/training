## Exercise 6 - Logic og tasks
### 3. OPTIONAL: Paste new Mail from File - store e-mail under contact
Tasks which do not contain any Local Datasources may be copied. We will take advantage of this to ease the job of adding emails to contacts.

This task will be similar to the task "Paste new Mail from File (Company)" and we will therefore use this task as a template.

#### Copying a task and adding Contact Data Source
1. Copy the task "Paste new Mail from File (Company)" using right clicking the task or using "ctrl+c, ctrl+v" and name the copy "Paste new Mail from File (Contact).
2. Add security to the task: "Users" should be able to Find and List and Read and Execute.
3. Add a new data source Contact and name it "Contact (input)" with appropriate cardinality and privacy. You can also check for "Cannot be blank" as the e-mails need a Contact to be added to.

#### Actions
1. In the Create Object(s)-effect:
   1. Remove "Company" by right-clicking the value and choosing "Clear value".
   2. Add Contact (input).Company as new Value for the Company-field on Mail.
   3. Add Contact (input) as Value for the Contact-field on Mail.

When this is done you should be able to delet the old "Company" data source from the new task.
   
#### Adding a command and an event
Add the action to the mail grid in the Contact Form. The command will need to run the global task with Contact as input for contact and "Get objects from the clipboard" for the Mail Message. The event should be set up on the grid for the Context Menu Item "Paste special".

<table>
   <tr><td><a href="exercise-06-1.md"><- Previous</a></td><td align="right"><a href="exercise-07.md">Next -></a></td></tr>
</table>
