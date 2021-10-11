## Logic and Actions


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


## Client Action

A Client Action is a sequence of side effects initiated by an event in the user interface, such as a click on a button. Various side effects are provided to support common tasks such as CRUD operations for objects, navigation between pages and dashboards, displaying messages and notifications, uploading and downloading files, and executing other Client- and [Server Actions](#server-action).

Block constructs such as decisions, for each loops, and catch exception provides functionality for conditional execution, enumeration of objects, and handling exceptions.

Within a Client Action you can determine which data the Client Action should operate on by specifying:
* A **Public Interface**: A Public Interface consists of [Data Sets](#data-set) received from "the outside" of the Client Action. These Data Sets are always filled when a Client Action is invoked.
* **Private Data Sets**: Private Data Sets, on the other hand, are internal to the Client Action and not visible outside the Client Action.

As with Page data sets, Data Sets here can be one of two types:
* **Filtered Data**: These are subsets of data from the Page's [Module](#module) Data Sources and are filled when a Page opens.
* **Refined Set**: These are criteria based subsets of data from Public Interface Data Sets or Writeable Sets. Refined Sets are read only and contains all objects which satisfies the given criteria at any time.

## Server Action
As the name implies, these actions are executed on the server side. The set of side effects supported by Server Actions is a bit more powerful than the set supported by [Client Actions](#client-action), and some of the effects are not possible to execute on the client side.

A Server Action can be defined within a Module (Local Server Action), or as an action which can be used from anywhere in your solution (Global Server Action). Local Server Actions can access data within your module. Global Server Actions cannot, but they provide a public interface for exchanging data.

Server Actions can be executed from a [Client Action](#client-action) using the "Run a Local Server Action" and "Run a Global Server Action". This makes it possible to share business logic in a hybrid desktop/web experience.
