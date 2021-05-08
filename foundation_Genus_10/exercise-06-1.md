## Exercise 6 - Logic, Actions and Events
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to the topic.*


#### Actions

You are now ready to add «Actions», which are logical user initialized actions, to the solution. Client Actions are executed when they are initiated from somewhere - for example from a right click menu or when clicking a button.

An Action corresponds in many ways to a method or a function in the programming world. It may have an input. It is executed with a call from somewhere. It executes sequentially. It may create variables and lists. And, it can include if-statements and loops (for and while). Some common actions are built-in in Genus, such as "Save changes" and "Navigate Back". These are available for selection the same places your custom actions are.

Actions in Genus are modeled with the same mindset that you would use if you were programming a method:
-	An Action has a set of Data Sources. Instances of these can be given to the Action as input (as long as the Data Sources are added in the Public Interface section) or they can by read from the data base within the Action itself. The Data Sources are used to modify, delete or create data.
- 	An Action contains a sequence of Effects (e.g. «Read Objects», «Create Object» or «Modify Objects»), which can be placed within Decision Blocks (if-statements) or Enumerator Blocks (for-loops).
- An Action may also call another Action, and data/objects can be transferred back and forth.
-	An Action can operate in memory only, or it can persist changes to the database.
-	Client Actions can have user dialogs, e.g. show the user dialog boxes with options that be used to control the execution path through the sequence of effects.
In Genus Studio, you find Actions several places:
  * Within Modules you have Client Actions and Server Actions.
  * In the main menu of Genus Studio, you can find global Actions the «Logic»-section of the left menu.
  * Actions can also be found in Rules, Agents and Web Services in the main left menu of Genus Studio

  Even though the different places you find Actions are set up similarly, they are by nature different:
-	Client Actions are triggered by a user initialized action, e.g. a click on a button.
- Server Actions are run on the server, but can be triggered from e.g. a Client Action.
- Global Actions are also often triggered by a user initialized action, but an exception is generic actions that are called from other actions, rules, agents or web services.
-	Rules are triggered automatically by defined business events in the solution, e.g. "after Company.Responsible has been modified, run this rule". The setup of effects is equal to that of actions, but the trigger is automated.
-	Agents are triggered by times, e.g. "every morning, send an e-mail to users with activity reminders". They are schematic actions, running on pre-defined schedules.
-	Web Services can be set up and triggered by a web-service call from for example an external system. The setup of Web Services are logic-wise equal to that of actions, but Web Services have additionally defined Schemas which describes the structure of input and output XML (more about this later).


#### Events
An action can be triggered by an Event. An Event can be many things, among them; a user click, a value change, a selection, a page change.

In Pages, both Views and Forms, you will see a menu section named Event Handlers. Within the Event Handler, there are three categories of Events; Page Events, Data Events and Control Events. In addition to these, each page has an Action Bar where actions can be triggered.
The different Events can be summarized as follows:

- Page Events are standard events related to navigation. You can determine which action is taken for instance when a user leaves the page (e.g. On Leave Page "Confirm Save Changes" which gives a popup message where the user determines whether changes are saved or discarded). The set of available effects here are predefined.

- Data Events relate to value or selection changes for a defined data source or data field. Here, your custom actions are available for selection. These are added within the Event Handler section.

- Control Events are events connected to the controls which build the Form, View or Canvas. These are added within the Form, View or Canvas section. Most controls come with a default "On Activate" event section, where you can add custom Actions. This can be useful e.g. for buttons, or when an input field being activated should trigger actions. Some controls also have a "Context menu"-section, where you can add multiple Actions in the context menu, both custom and default actions.

- Action Bar Events are available at the Page level (the top level within the control view). Here both default and custom actions are available, as with certain control events.


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
