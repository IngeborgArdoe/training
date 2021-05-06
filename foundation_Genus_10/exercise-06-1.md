## Exercise 6 - Logic og Actions
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to the topic.*

### Modeling logic - Principal overview

You are now ready to add «Actions», which are logical user initialized actions, to the solution. Actions are executed when they are initiated from somewhere - for example from a right click menu or when clicking a button.

An Action corresponds in many ways to a method or a function in the programming world. It may have an input. It is executed with a call from somewhere. It executes sequentually. It may create variables and lists. And, it can include if-statements and loops (for and while). 

Actions in Genus Apps are modeled with the same mindset that you would use if you were programming a method:
-	An Action has a set of Data Sources. Instances of these can be given to the Action as input (as long as the Data Sources are not private) or they can by read from the data base. The Data Sources are used to modify, delete or create data. 
- 	An Action contains a sequence of Effects (e.g. «Read Objects», «Create Object» or «Modify Objects»), which can be places within Decision Blocks (if-statements) or Enumerator Blocks (for-loops).
- 	An Action may also call another Action, and data/objects can be transferred back and forth.
-	An Action can operate in memory only. You will have to place everything within Scope Blocks that have the Commit-option checked (default), if you want to make changes to the database. If you, on the hand, uncheck the Commit-option or exclude the Scope Blocks completely, nothing gets persisted to the database.
-	An Action can have user dialogs, e.g. show the user dialog boxes with options that be used to control the execution path through the sequence of effects.
In Genus Studio, you will see Actions in the «Logic»-section of the left menu. Here are also Rules, Agents and Web Services. Even though the 4 of them are set up similarly, they are by nature different:
-	Actions are triggered by a user initialized action, e.g. a click on a button. The exception is generic actions that are called from other actions, rules, agents or web services. 
-	Rules are triggered by business events in the solution, e.g. "after Company.Responsible has been modified, run this rule". The setup of effects is equal to that of actions.
-	Agents are triggered by times, e.g. "every morning, send an e-mail to users with activity reminders". They are schematic actions.
-	Web Services can be set up and triggered by a web-service call from for example an external system. The setup of Web Services are logic-wise equal to that of actions, but Web Services have additionally defined Schemas which describes the structure of input and output XML (more about this later).


### 1. Change Responsible for Contact
You will now make a simple Action, "Change Responsible for Contact" that can take one or more Contacts as input, and change their Resposible.
#### Data Sources
a. Contact - an unbounded datasource for which we will choose new responsible for.
   i. Let the cardinality be Unbounded, and set the privacy to not Private (Private unchecked).
   *Guidance: Right-click in the upper-left pane -> Add -> Object. Select «Contact». In the bottom pane (General) uncheck Private.
   
b. Data Source:  User - a "One"-data source which will represent the new Responsible.*
      i. Add the Data Source User with cardinality One and Private checked.
      
#### Actions - Choose new responsible

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
One important thing that we haven't considered yet is security. Access is given to security groups per action. All users of Genus CRM are members of security group "Users" og should have access to this action.
1. Go to File -> Properties (upper-left corner of the action). Under Security, add security group "Users". Check "Find and List" and "Read and Execute". Note: The action has to be saved before you are allowed to open the Security-tab.

*The action is finished, but not made available for the end user yet. To do so, you will have to publish it through an Event.*
2. Navigate to table «Contacts». Add an Event that executes your action.
   1. Effect Type = «Run a Action (Global Scope)».
   2. Effect = "Change Responsible for Contact".
   3. Enabling: Select "On selected objects" (the action should be enabled when one or more rows are marked).
   4. Filter Data: Set "Two way binding to objects in the data source: Contact" with Objects: Selected.
   *Note: Defining a data filter like this is a quick way of saying "I want my action's data source «Contacts input» to be populated with all contact persons marked in the table by the user". When clicking the Action «Change Responsible for Contact» in the Action pane, the chosen contact persons are copied into the action «Change Responsible for Contact» and the action's effects are executed.* 

<table>
   <tr><td><a href="exercise-05-2.md"><- Previous</a></td><td align="right"><a href="exercise-06-2.md">Next -></a></td></tr>
</table>
