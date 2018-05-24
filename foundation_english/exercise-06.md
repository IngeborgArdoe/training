## Exercise 6 - Logic og tasks
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction of the topic.*

###Modeling logic - Principal overview

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


###Change Responsible for Contact
You will now make a simple Task that can take one or more Contacts as input, and change their Resposible.
1. Data Sources: Add Object Class «Contact».
   *Guidance: Right-click in the upper-left pane -> Add -> Object. Select «Contact». In the bottom pane (General) uncheck Private. Change also the Name to "Contacts input" to highlight for the "rest of the solution" what the input is, and which cardinality it has. Although this is not required, it is good practice, as it makes it easier when you for example want to connect a table to the task.*
2. Actions: The first thing that we want to do is to make it possible for the user to provide an input. The user should be able to select one person (User) - from a dropdown - which is to become the new resposible of all input contacts (Data Source "Contacts input").
   1. First, you will need a "variable" in which you can store the Responsible person (User) that is chosen by the user.
	  1. Go back to Data Sources and add a Local Object (Add -> Local Object). Name it "User Input".
	  2. In the pane on the right-hand side, add a Field. Set Display Name = "New Resposible" and Data Type = "User". Uncheck "Allow blank values" (the field is required).
   2. Navigate to Actions:
	  1. Add the Effect "Open a Form".
	  2. Double-click on the effect and set Type = "Local Object Window" and Data Source = "User Input". Check "Create" (we are creating a local object in memory). Click on button "Modify..." and write the text that will be showed to the end user when the window is opened. See below: 
      ![oppg6fig1.JPG](media/oppg6fig1.JPG)
 
   Next is the effect which changes Contact.Responsible for all objects in the data source "Contact input" and saves it to the database.
   3. Add a Block "Scope".
	  *Note: By default, the Commit-option is checked. This means that all changes (Create or Modify) done by effects within the Scope will be saved.*
   4. Place Effect "Modify Objects" within in the Scope and parameterize it to change the "Responsible" field of Data Source "Contact input".
  *Guidance: Set it up as illustrated below. This will generate a SQL query that changes the Responsible of all Contacts in "Contacts input".*
     ![oppg6fig2.JPG](media/oppg6fig2.JPG)
  
One important thing that we haven't considered yet is security. Access is given to security groups per task. All users of Genus CRM are members of security group "Users" og should have access to this task.

3. Go to File -> Properties (upper-left corner of the task). Under Security, add security group "Users". Check "Find and List" and "Read and Execute". Note: The task has to be saved before you are allowed to open the Security-tab.

*The task is finished, but not made available for the end user yet. To do so, you will have to publish it through an Event.*

4. Navigate to table «Contacts». Add an Event that executes your task.
   1. Effect Type = «Run a Task (Global Scope)».
   2. Effect = "Change Responsible for Contact".
   3. Enabling: Select "On selected objects" (the task should be enabled when one or more rows are marked).
   4. Filter Data: Set "Two way binding to objects in the data source: Contact" with Objects: Selected.

	  *Note: Defining a data filter like this is a quick way of saying "I want my task's data source «Contacts input» to be populated with all contact persons marked in the table by the user". When clicking the Action «Change Responsible for Contact» in the Action pane, the chosen contact persons are copied into the task «Change Responsible for Contact» and the task's effects are executed.* 
5. Add «Change Responsible for Contact» to the Ribbon.
   1. Name the event "Change Responsible".
   2. Choose symbol #692 with overlay #13
   3. Open Customize Ribbon. Under Main Tabs, add a new Tab Section. Call it "Responsible"
   4. Mark tab section "Responsible" and double-click on the "Change Responsible"-event (located under Table Commands).

6. OPTIONAL (but recommended!): Navigate to Form «Company», and add a command that runs your task. Place the command on the «Contacts»-grid and make sure the enabling is correct. Remember also to create an Event that triggers the command from the grid. The command should also be made available from the Ribbon (Context Tab Group Contact, in a new Tab Section called "Responsible Contact").

*Note: Define the Data Filter of the command, i.e. what to filter into the task's data source «Contacts input». It should be a Two-Way binding to Selected Objects in the Data Source «Contact».* 
*"Two-Way", in this context, means that if changes are not persisted (committed/saved) in the task, they are brought back to the Comapany-form and the "Save"-botton is made available.*
 
### Paste new Mail from File - store e-mail under contact
You will now make it possible to create Mail on contact persons. For this purpose, a task "Paste new Mail from file" - taking «Mail Message (input)» and «Company» as input - has already been created. You will have to expand this with logic to store Mail not only on Companies, but Contacts as well. For this, you must make it possible to input «Contact».

1. Open the task «Paste new Mail from file». Add «Contact» as a Data Source and name it "Contact (input)".
   *Note: Given that Mail will be pasted on one single Contact at a time, the Occurences parameter of this Data Source should be set to "Allow one object".*
2. Expand the logic under Actions
   1. Expand the Condition of the first Decision-block to make it valid also when «Contact (input)» has value (and «Company (input)» has not).
   *Guidance: You can make Conditions with AND and OR. The condition «Mail Message (input)» has value AND (Company input has value OR Contact input has value) is expressed as illustrated below (Tip: Add Group-button):*
   ![oppg6fig3.JPG](media/oppg6fig3.JPG)
   2. Modify the Create Objects effect so that the field Company is set to «Company (input)» if this has value or «Contact (input)».Company if «Contact (input)» has value. Also set field Contact equal to «Contact (input)».
   ![oppg6fig4.JPG](media/oppg6fig4.JPG)
3. Add a command to the Mail-tab in the Contact.form which runs the task «Paste new Mail from File». The command should be triggered by Menu item «Paste». Create the event and place it on the grid. Add the command to the Ribbon (New Tab Section under Mail Management: Clipboard. Remember to provide a suitable Name, Symbol and Tip).

*Guidance: The command is set up with Effect Type = Run a Task (global scope), and the Event with Menu = Past Special. The data filter of the command must be set to «Mail Message (input)» = "Get objects from the clipboard" and «Contact (input)» = Contact.*
4. While you're at it, place a command on the Mail-tab that calls the existing task "Copy Mail to Clipboard as Mail Message". Make it available through an event on the grid and in the Ribbon.

*Guidance: Set the event's Menu Item = Copy. The command's Data Filter must be set to «Mail Message (input)» = selected objects in data source Mail. Ribbon: Search for "copy" to find a suitable symbol.*
