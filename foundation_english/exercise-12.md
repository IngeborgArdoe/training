## Exercise 12 - Mail Merge
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction of the topic. He/she will explain the concept of Mail Merge and show the schema editor in Genus Apps.*

These exercises are optional and should be done only if time allows. That being said - we recommend you to at least read through the exercises.

**OPTIONAL EXERCISE:** Make a new task "Order Confirmation", which takes a Request as input and from it generates an order confirmation (Word document). Information that will be merged into the document is Order No, Subject, Description, Expected Delivery Date, Order Value NOK, Company Name, Org No, Contact Name (name of person ordering) and ResponsibleName (name of user).

1. Create a Schema "Order Confirmation" with "OrderConfirmation" as root node (Complex Type) and all the fields above as Elements (all can be of data type String).

   *Guidance: This exercise requires that you have been through a Schema setup review. A Schema is basically a description of the XML layout. You will later generate XML with your schema through the "Create Objects" effect (data source = schema). This XML can then be used as input to the "Merge Data to a Document" effect along with a Word file. The Word file will contain "tags" (merge fields) with names identical to those of the XML elements, allowing data to be merged into the document. Take a look at the provided solution for inspiration.*
   
2. Create a Word document for Order Confirmation with merge fields equivalent to the element names of the schema just made.
   *Guidance: Insert a "merge field" in Word by marking the spot where you want the data to be placed and navigate to menu Insert -> Quick Parts -> Field. Next, choose "Merge Field" from the list on the left-hand side and type in the "Field Name" (same as the element name in the schema!).*

   You are required to start the document with a merge field "TableStart:OrderConfirmation", where "OrderConfirmation" is the root node (Complex Type) of the schema (or the node that holds the fields that you want to merge). Equivalently, you will have to end the document with a field "TableEnd:OrderConfirmation". In between the latter two merge fields, you can add merge fields such as "OrderNo", "Subject" and so on. Note; to speed up the process you can copy merge fields, right-click and "Edit Field...".

   Ask the instructor to send you the Word document if you don't want to spend time on the order confirmation template.
   
3. Create a task "Order Confirmation". Publish it through a button in the Request-form.

   *Guidance: The task needs data sources "OrderConfirmation" (xml schema), Request (input), Document (to be created) and General File (temp, will be used as temporary output in the merge effect before Document is created). Necessary effects to include are a "Create Objects" (creating OrderConfirmation / mapping values), a "Merge Data to a Document" (where the Word document is the "Embedded file", the OrderConfirmation schema is the "XML Document" and the General File is the "Output Document"), another "Create Objects" (creating the Document object with data from the General File object), and fianlly an "Invoke a File" (opens Document.File Data in Word).*

4. **EXTRA:** Make a task "Send Order Confirmation" which, after allowing the user to select among existing Order Confirmations (Documents on the Request), opens Outlook with the document attached. The task should also store the Mail object. Make the task available in the Ribbon of the Request-form.
  
   *Guidance: Add data sources Request (input), Mail (to be created), Document (confirmation document to attach)and Mail Message (temporary file which opens in Outlook, and is used to generate the Mail object after send).

   The task should have the following effects:
   * "Read Object": Data source = Document, with user interaction (let the user choose among documents associated with the request).
   * "Create a Mail Message": Define "To", "Subject", "Attachments" (Document.File Data) and suggest a default e-mail text. Make sure the effect is set to "Write message to a data source" (Mail Message (temp)) so that the e-mail is not sent immediately. Note: The reason for keeping the Mail Message file in a data source is to avoid losing changes made by the user in Outlook before he/she press "Send". You could have used the "Open a Form" effect directly, but it's more visual to create an e-mail in the "Create a Mail Message" effect.
   * "Open a Form": Choose Mail Message Window and Modify. Check "Wait until the form is closed". The effect will now open the suggested e-mail and pause the execution until the user has pressed "Send" in outlook. 
   * "Create Objects": Data source = Mail. Map fields from Mail Message (temp). Put the effect in a Commit Scope to save the Mail object.


<table>
   <tr><td><a href="exercise-11.md"><- Previous</a></td><td align="right"><a href="exercise-13.md">Next -></a></td></tr>
</table>