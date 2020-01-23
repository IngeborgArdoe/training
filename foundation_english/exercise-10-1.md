## Exercise 10-1 - Request

In this exercise, you will make a new business object «Request» that allows the user to register inquiries from customers. «Request» will be used in later exercises to generate order confirmations and reports, so the most important thing is to model the object. As you have seen before, some exercises are mandatory and some are optional. Do the optional ones if you have time.

Before modeling «Request», you will be asked to create a couple of Code Domains and an Identifier Domain. This way, you will be able to set all Data Interpretations correctly when you model the object class. 

####1. Create a Code Domain named "Request State"

Add values "Open" (value=10), "Closed" (value=20) and "Canceled" (value=30).

*Guidance: In Genus Studio, right-click on Object Classes -> New -> Select Code Domain.*

####2. Create a Code Domain named "Request Type"

Add values "Order" (value=10) and "Service" (value=20).

*Comment: The requests can hence be classified as either orders ("Order") or inquiries for help / other ("Service").*


It would also be nice to have a sequential "order number" that is generated on the creation of a Request. For this, you can create an «Identifier Domain» (from Studio -> right-click on Object Classes -> New -> select Identifier Domain). Such an object class demands a table in the database containing the latest order number. The table has a name (e.g. "Order No Counter") and an integer field (e.g. "Order No"). When an Identifier Domain is used in the calculation of a field, Genus retrieves the latest number in the sequence and updates it incrementally with 1.

####3. Create an Identifier Domain named "Order No Counter"

The Identifier Domain should have an integer field "Order No".
   
*Guidance: Create the table in the database and insert the first "order number" instance. Do it with the following SQL query:*

```
CREATE TABLE OrderNoCounter (
 OrderNo int
)  
go

INSERT INTO OrderNoCounter
VALUES (10000)

```

In the wizard for creating a new Identifier Domain, choose "Sequential Counter" in step 2:
![oppg9fig1.JPG](media/oppg9fig1.JPG)
 
In step 3, select the column that will hold the counter:
![oppg9fig2.JPG](media/oppg9fig2.JPG)

Click Finish.
  
####4. Create Object Class «Request» 

In the New Object Domain wizard, remember to set correct Data Interpretations.

*Comment: The SQL script for creating table «Request» has already been run against your database. This is because we wanted to genereate some data in advance for making reports/analysis in later exercises.*
   
   1. Set default value for field «Order No». Select «Custom Id Generator» and «Order No Counter» from the list. Make Subject, State and Type mandatory. Also, agreed Delivery Date and Expected Delivery Date should have Data Interpretation "Date" (not "Date and Time"), as we don't want the user to care about the time of the delivery.
      
      After creating the object class, sett Default values for the «Created» fields and Formula values for the «Modified» fields. Default values for State and Type should also be defined. In addition, set the default value of Received Date to "Now", but let it be possible to change.
      
      *Comment: Default locks the values after creation (i.e. they remain unchanged after creation), while Formula allows the values to be automatically set whenever the Request object is modified.*
   
   2. Open Object Class «Request» (right-click -> Open) and define the following properties:
      - Search (set search properties, under «Search Properties» in tab «Search»).
      - Events -> Auditing (want to log all changes made on Request objects, check «Enable Auditing» in tab «Events»).
      - Display -> Naming (field «Subject» should at least be a part of the naming, in tab «Display»).
      -	Data Sorting (default sorting on «Company» ascending and «Received Date» descending, in tab «Data Sorting»).
  
You have now created the object itself. Next, you will make it possible to drag documents and e-mail into a Request.

####5. Add property "Request" on object classes Mail and Document

*Guidance: Use the following SQL query to create a new column in the Document table:*

```
ALTER TABLE Document
 ADD RequestID uniqueidentifier 
```

*Run the equivalent query against the Mail Table. Add the two fields to their corresponding Object Classes in Studio.*

####6. Create tasks «Paste new Mail from file (Request)» and «Paste new Document from file (Request)»

Both tasks should take Request as input.

*Guidance: Copy the corresponding Paste-tasks for Company, and substitute the data source Company with Request. Make sure that the reference to Request is correctly set on Mail/Document creation (Mail.Request = Request (input) and Document.Request = Request (input)).*

You are now ready to add Request to the interface, i.e. make a Request-form and list Requests under Company. In addition, you will be asked to make a list (table) of Requests that is accessible from the Navigation Pane.

<table>
   <tr><td><a href="exercise-09.md"><- Previous</a></td><td align="right"><a href="exercise-10-2.md">Next -></a></td></tr>
</table>
