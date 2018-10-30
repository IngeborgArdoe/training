## Exercise 6 - Logic og tasks
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to the topic.*

### Modeling logic - Principal overview

You are now ready to add «Tasks», which are logical user initialized actions, to the solution. Tasks are executed when the user selects them from the Actions-pane or when he/she clicks on a button pointing to one of them in a Form.

A Task corresponds in many ways to a method or a function in the programming world. It may have an input. It is executed with a call from somewhere. It executes sequentually. It may create variables and lists. And, it can include if-statements and loops (for and while). 

Tasks in Genus Apps are modeled with the same mindset that you would use if you were programming a method:
-	A Task has a set of Data Sources. Instances of these can be given to the Task as input (as long as the Data Sources are not private) or they can by read from the data base. The Data Sources are used to modify, delete or create data. 
- 	A Task contains a sequence of Effects (e.g. «Read Objects», «Create Object» eller «Modify Objects»), which can be places within Decision Blocks (if-statements) or Enumerator Blocks (for-loops).
- 	A Task may also call another Task, and data/objects can be transferred back and forth.
-	A Task can operate in memory only. You will have to place everything within Scope Blocks that have the Commit-option checked (default), if you want to make changes to the database. If you, on the hand, uncheck the Commit-option or exclude the Scope Blocks completely, nothing gets persisted to the database.
-	A Task can have user dialogs, e.g. show the user dialog boxes with options that be used to control the execution path through the sequence of effects.
In Genus Studio, you will see Tasks in the «Logic»-section of the left menu. Here are also Rules, Agents and Web Services. Even though the 4 of them are set up similarly, they are by nature different:
-	Tasks are triggered by a user initialized action, e.g. a click on a button. The exception is generic tasks that are called from other tasks, rules, agents or web services. 
-	Rules are triggered by business events in the solution, e.g. "after Company.Responsible has been modified, run this rule". The setup of effects is equal to that of tasks.
-	Agents are triggered by times, e.g. "every morning, send an e-mail to users with activity reminders". They are schematic actions.
-	Web Services can be set up and triggered by a web-service call from for example an external system. The setup of Web Services are logic-wise equal to that of tasks, but Web Services have additionally defined Schemas which describes the structure of input and output XML (more about this later).


### 1. Change Responsible for Contact
You will now make a simple Task, "Change Responsible for Contact" that can take one or more Contacts as input, and change their Resposible.
#### Data Sources
a. Contact - an unbounded datasource for which we will choose new responsible for.
   i. Let the cardinality be Unbounded, and set the privacy to not Private (Private unchecked).
   *Guidance: Right-click in the upper-left pane -> Add -> Object. Select «Contact». In the bottom pane (General) uncheck Private.
b. Data Source:  User - a "One"-data source which will represent the new Responsible.
      i. Add the Data Source User with cardinality One and Private checked.
#### Actions
1. Choose new responsible
The first thing that we want to do is to make it possible for the user to choose a User which shall be the new Responsible for the contact. Here we use a useful input method which shows a table of Users to the user that the user can choose between.
1. Add a "Read Object(s)"-effect
2. Double-click the effect and choose "User" as the Data Source and "User.state=Active" as Data Filter.
3. Switch to the tab item "User Interaction"
   1. Check "Prompt the user to select objects".
   2. Type in a meaningful Dialog Title like "Choose responsible" and Dialog Prompt "Please ..."
   3. Choose fields that will be shown to the end user when he or she will choose the new Responsible
   4. Use a meaningful sorting (E. g. First name, Last name)
   ![oppg6fig1.JPG](media/oppg6fig1.JPG)

Next is the effect which changes Contact.Responsible for all objects in the data source "Contact input" and saves it to the database.

#### Set the chosen User as Responsible
1. Add a Block "Scope".
*Note: By default, the Commit-option is checked. This means that all changes (Create or Modify) done by effects within the Scope will be saved.*
2. Add a "Modify objects" effect which sets the Contact.Responsible field to the chosen User.
*Guidance: Set it up as illustrated below. This will generate a SQL query that changes the Responsible of all Contacts in "Contacts input".*
![oppg6fig2.JPG](media/oppg6fig2.JPG)

#### Security
One important thing that we haven't considered yet is security. Access is given to security groups per task. All users of Genus CRM are members of security group "Users" og should have access to this task.
1. Go to File -> Properties (upper-left corner of the task). Under Security, add security group "Users". Check "Find and List" and "Read and Execute". Note: The task has to be saved before you are allowed to open the Security-tab.

*The task is finished, but not made available for the end user yet. To do so, you will have to publish it through an Event.*
2. Navigate to table «Contacts». Add an Event that executes your task.
   1. Effect Type = «Run a Task (Global Scope)».
   2. Effect = "Change Responsible for Contact".
   3. Enabling: Select "On selected objects" (the task should be enabled when one or more rows are marked).
   4. Filter Data: Set "Two way binding to objects in the data source: Contact" with Objects: Selected.
   *Note: Defining a data filter like this is a quick way of saying "I want my task's data source «Contacts input» to be populated with all contact persons marked in the table by the user". When clicking the Action «Change Responsible for Contact» in the Action pane, the chosen contact persons are copied into the task «Change Responsible for Contact» and the task's effects are executed.* 
   
### 2. Ribbon
Add «Change Responsible for Contact» to the Ribbon.
1. Name the event "Change Responsible".
2. Choose symbol #692 with overlay #13
3. Open Customize Ribbon. Under Main Tabs, add a new Tab Section. Call it "Responsible"
4. Mark tab section "Responsible" and double-click on the "Change Responsible"-event (located under Table Commands).

#### OPTIONAL (but recommended!)
Add Change Responsible Contact to Ribbon
Navigate to Form «Company», and add a command that runs your task. Place the command on the «Contacts»-grid and make sure the enabling is correct. Remember also to create an Event that triggers the command from the grid. The command should also be made available from the Ribbon (Context Tab Group Contact, in a new Tab Section called "Responsible Contact").

*Note: Define the Data Filter of the command, i.e. what to filter into the task's data source «Contacts input». It should be a Two-Way binding to Selected Objects in the Data Source «Contact».* 
*"Two-Way", in this context, means that if changes are not persisted (committed/saved) in the task, they are brought back to the Comapany-form and the "Save"-botton is made available.*
 
### 3. Paste new Mail from File - store e-mail under contact
You will now make it possible to create Mail on contacts. This task will be similar to the task "Paste new Mail from File (Company)" and we will therefore use this task as a template.

#### Copying a task and adding Contact Data Source
1. Copy the task "Paste new Mail from File (Company)" using right clicking the task or using "ctrl+c, ctrl+v" and name the copy "Paste new Mail from File (Contact).
2. Add security to the task: "Users" should be able to Find and List and Read and Execute.
3. Add a new data source Contact and name it "Contact (input)" with appropriate cardinality and privacy. You can also check for "Cannot be blank" as the e-mails need a Contact to be added to.

#### Actions
1. In the Create Object(s)-effect:
   1. Remove "Company" by right-clicking the value and choosing "Clear value".
   2. Add Contact (input).Company as new Value for the Company-field on Mail.
   3. Add Contact (input) as Value for the Contact-field on Mail.

#### Copying an e-mail (optional)
1. Place a command on the Mail-tab that calls the existing task "Copy Mail to Clipboard as Mail Message". Make it available through an event on the grid and in the Ribbon.

*Guidance: Set the event's Menu Item = Copy. The command's Data Filter must be set to «Mail Message (input)» = selected objects in data source Mail.


<table>
   <tr><td><a href="exercise-05.md"><- Previous</a></td><td align="right"><a href="exercise-07.md">Next -></a></td></tr>
</table>
