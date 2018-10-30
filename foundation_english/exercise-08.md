## Exercise 8 - Documents, Mail
Your next task will be to add the possibility of dragging documents into a tab in the Company-form.

For this, you will have to model an object «Document» (like «Mail») that allows the user to save the file in the database. You will also have to build the functionality for handling "drag-and-drop" to and from Genus CRM.

1. Model Object Class «Document».

   *Guidance: To save some time, use the SQL query below to create a Document-table in the database. Make sure that the Data Interpretations of File Name, File Data, File Extension and File Size are set correctly when you model the object class. Use the built-in data types with identical names.*
   
   SQL: 
  
   ```
   CREATE TABLE Document (
    DocumentID uniqueidentifier PRIMARY KEY,
    FileName varchar(240), 
    FileData varbinary(max), 
    FileSize int, 
    FileExtension varchar(30), 
    CreatedDate datetime, 
    CreatedByUserID uniqueidentifier, 
    ModifiedDate datetime, 
    ModifiedByUserID uniqueidentifier, 
    CompanyID uniqueidentifier,
    ContactID uniqueidentifier
   )
   ```
   
2. Add Document.File Data as a search field on Company.

   *Guidance: This allows the user to search for text found in documents associated with the Company. Open Object Class «Company», and add Document.File Data as Search Property under «Search».*

   NB: In order to get "full text" search operators, you need to open Object Class Property «Document.File Data» and check «Full Text and Like operators» under «Data Filtering».

3. RUN A "DEPLOY TO ALL". The reason is that you will soon set up a "file preview" which utilizes calls against the server. Naturally, the server needs to know about the new object class for this to work.
4. Make a new Task "Paste new Document from File". This should take Company and File(s) as input, and create Document(s).
   *Guidance: You will need 3 data sources; Company (name="Company (input)", cardinality="one", private=no), General File (name="General files (input), cardinality="unbound", private=no) and Document (name="Documents (to be created)", cardinality=unbound, private=yes). The task is logically very simple. All you need is a Scope and a Create Objects effect. If you need inspiration, you can look at the equivalent task «Paste new Mail from file». Remember to define the security of the task after creation.*

   *Tip: The file-input comes with cardinality "unbounded". For each file, a document has to be made. Here you can either make use of an Enumerator which loops through the General File data source OR (even simpler) you can define a Create Object on data source Document which is bound to the General File data source at the top level. The latter option will create a document per instance in the "General Files (input)" data source!*
  ![oppg8fig1.JPG](media/oppg8fig1.JPG)
5. Create a new tab in the Company-form that you can use to list documents. Add a Grid, and define which columns to show and what sorting to use. Place a Command pointing to the task that you just made on the Documents-tab, along with an Event to trigger it on the grid itself. Add also commands and events for Delete and Invoke a File (open document by double-clicking).
   Insert a "file viewer" on the right side of the grid for showing files (take a look at tab "Mail" for inspiration).
   *Tip: For the event to trigger when files are pasted into the grid, choose Menu Item = Past Special. Note that you can - under the command's data filter parameter - filter out General File types Mail Message and Calendar Item from the input to the task, as you don't want to store these file types as Documents (but rather as Mail or Activity):*
  ![oppg8fig2.JPG](media/oppg8fig2.JPG)
6. OPTIONAL EXERCISE: Create a new task "Copy Document to Clipboard as File" equivalent to "Copy Mail to Clipboard as Mail Message". Publish it.
   *Guidance: The task should take Documents as input and should create General Files. Make it available through an Event with Menu item = Copy.*
7. OPTIONAL EXERCISE: Add Delete and Paste/Copy to the Ribbon.
   Guidance: Create two new Tab Sections under Context Tab Group "Document" and Tab "Document Management": Tab Section "Manage" for Delete and Tab Section "Clipboard" for Paste/Copy to Clipboard. Recall symbols and enabling conditions.*
   
The next thing for you to make is the functionality for sending e-mail to contact persons and store them as «Mail». This exercise is again optional, but we recommend you to at least browse through it and look at the solution.
   
8. OPTIONAL EXERCISE: Create a new task "Send Mail to Contact". The task should be made available through buttons both in the Contact-form and the Company-form (where you have a grid of contact persons).
   1. Create a new task which opens a mail-window and stores the e-mail as a Mail-object in the database after "Send" has been clicked.
  
   *Guidance: The task needs «Contact» as data source (cardinality=unbound). In addition, you will need a File data source (cardinality=one) of type "Mail Message". This is the Outlook-file which will be created in memory and sent out. After being sent, the e-mail has to be stored as a Mail-object - one instance per contact. Accordingly, you will have to include the data source Mail (cardinality=unbound) as well.*
   *The effects needed are Create a Mail Message (that creates a Mail Message file with the e-mail addresses of the contacts and saves the message to the data source «Mail Message»), Open a Form (that opens a Mail Message window from the file data field of «Mail Message») and Create Objects (that saves Mail objects).*
   
   *Take a look at the provided solution for further guidance. Remember to set the security of the task!*

<table>
   <tr><td><a href="exercise-07.md"><- Previous</a></td><td align="right"><a href="exercise-09.md">Next -></a></td></tr>
</table>
