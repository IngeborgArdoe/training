## Exercise 6 - Logic og tasks
**SESSION BY INSTRUCTOR:** *The instructor will start of by giving you a brief introduction of the topic.*

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

3. Gå til File -> Properties (øverst til venstre i tasken) og legg til Security Group «Users» i arkfane Security. Huk av for «Find and List» og «Read and Execute». Merk: Tasken må først være lagret før du får tilgang til Security-arkfanen.
3. Go to File -> Properties (in upper-left corner of the task) and in the Security-tab add security group "Users". Check "Find and List" and "Read and Execute". Note: The task has to be saved before you are allowed to open the Security-tab.

*Tasken er ferdig, men er ikke tilgjengelig for sluttbrukere ennå – den må kobles inn i et User Interface som en event.*

4. Gå til table «Contacts». Under «Events» legger du til en event for å kjøre tasken
   1. Effect Type = «Run a Task (Global Scope)»
   2. Effect = “Change Responsible for Contact”
   3. Enabling: Huk av for “On selected objects” (tasken skal være enabled ved valg av flere rader)
   4. Filter Data: sett «Two way binding to objects in the data source: Contact» med Objects: Selected.

      *Merk: Setting av data filter på denne måten er en hurtig måte å si at «tasken sin datasouce Contacts input skal populeres med de kontaktpersonene jeg har valgt i tabellen min». Valgte kontaktpersoner vil nå i klienten, ved å trykke på Action «Change Responsible for Contact» i Actions pane, kopieres inn i tasken «Change Responsible for Contact» og tasken vil eksekvere effektene sine og avslutte.*
5. Legg til Change Responsible for Contact i Ribbon
   1. Navngi eventen i tabellen «Change Responsible»
   2. Gi den symbol #692 med overlay #13
   3. Åpne Customize Ribbon. Under Main Tabs legg til en ny Tab Section. Kall denne Responsible
   4. Marker Responsible-Tab Section-en og dobbeltklikk på Change Responsible-eventen (ligger under «Table Commands».

6. VALGFRITT (men anbefalt!): Gå til Form «Company» og legg til en command for å kjøre tasken. Legg commanden på Contacts-grid-en med riktig enabling. Husk symbol. Legg på event for å kjøre tasken «Change Responsible for Contacts» i grid-en. Gjør kommandoen tilgjengelig også fra Ribbon (Context Tab Group Contact i en ny Section «Responsible Contact».

*Merk: Under Filter Data for commanden setter du hva som skal filtreres inn til Tasken sin datasource «Contacts input». Denne settes Two-Way mot Data Source “Contact” sin Selected Objects.*
  
*At man setter noe “Two-Way” her betyr at endringene tas med tilbake, og hvis endringer i tasken ikke er persistert (committet/lagret) vil man få opp “Lagre” knappen enabled i Contact skjermbildet etter trykk på knappen.*

 
Vi skal nå legge til muligheten for å opprette Mail på kontaktpersoner. Til dette formålet har vi fra før en task «Paste new Mail from file» som tar som input «Mail Message (input)» og «Company». Tasken skal utvides til å også ta «Contact» som mulig input, samt logikk for å lagre en Mail under Contact.

### Paste new Mail from File - lagre e-post under kontakt
«Paste new Mail from File» skal utvides til å kunne lagre epost under kontaktperson
1. Åpne task «Paste new Mail from file». Legg til Contact som Data Source og navngi «Contact (input)»
   *Merk: I og med at det kun pastes ny Mail på én Contact av gangen skal Occurrences på denne Data Sourcen settes til “Allow one object”.*
2. Utvid logikk under Actions
   1. Utvid Condition i den første “Decision” blocken til å også slå til hvis kun Contact (input) har verdi.
   *Veiledning: Man kan lage Conditions med AND og OR. For å få satt opp «Mail Message input skal ha verdi OG (Company input eller Contact input skal ha verdi)» blir utrykket slik (Tips: «Add Group» knappen):*
   ![oppg6fig3.JPG](media/oppg6fig3.JPG)
   2. Utvid logikken i Create Objects effekten til å sette feltet «Company» fra Company (input) hvis den har verdi, eller fra Contact (input).Company hvis Contact (input) har verdi. Sett også feltet Contact fra Contact (input).
   ![oppg6fig4.JPG](media/oppg6fig4.JPG)
3. Legg til command i Mail-tab i Contact Form som trigger på Menu «Paste» og som kjører task «Paste new Mail from File». Legg til event i grid. Legg til event i Ribbon (ny seksjon under Mail Management: Cliboard. Husk passende Name, Tip og Symbol (søk opp paste).

*Veiledning:  Denne settes opp med Effect Type = Run a Task (global scope) og Menu = Paste Special. Under Filter Data setter du tasken sin Mail Message (input) lik «Get objects from the clipboard» og Contact (input) lik Contact.*
4. Legg samtidig på command i Mail-Tab som kaller eksisterende task “Copy Mail to Clipboard as Mail Message». Tilgjengeliggjør via event på grid og i Ribbon.

*Veiledning: Velg her Menu «Copy» og sett Data Filter til tasken sin Mail (input) lik selected objects fra Contact formen sin data source Mail. Ribbon: Søk opp «copy» for å finne passende symbol.*
