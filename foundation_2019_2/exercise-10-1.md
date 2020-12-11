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

<table>
   <tr><td><a href="exercise-09.md"><- Previous</a></td><td align="right"><a href="exercise-10-2.md">Next -></a></td></tr>
</table>
