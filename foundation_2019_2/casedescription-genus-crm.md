# Case description: Genus CRM

###The provided solution Genus CRM contains the following business objects:
- 	Company & Log (logging of important company events)
-	Contacts & Log
-	Activities
-	Mail
-	Document
-	Request (requests from customers)
-	Users (users that have access to the solution)
-	Codes (various code domains)

Companies have a flag which indicates whether they are customers or not. This is to keep track of active customers, in addition to earlier customers and/or prospects.
Each company has one or more Contacts, which are the persons to contact, conduct sales meeting with, receive requests from and so on.
Activities are used to plan meetings. When executed, their status is set to "completed". It is possible to drag-and-drop activities between Outlook and Genus CRM. Activities also have a responsible user and can be linked to a contact.

The Mail object allows the user to drag important e-mail conversations and confirmations from Outlook into Genus CRM and to the respective company. One can also send e-mail from the system. These will be stored both in Outlook and on the company in Genus CRM.
Similarly, important Documents can be dragged into Genus CRM and stored on the company. One can also generate some documents from Genus, e.g. order confirmations (from a Request that has been confirmed as an order).
All users of the solution are stored as Users, and can be responsible for activities, companies and so on.

In addition, there are Code-objects in the solution (e.g. Activity Code), which will allow end/super users to modify code domains themselves.

### Case
You, as a user of the solution, works in a company that sells bike parts to various bike stores around the country/world. The bike stores are defined as Companies and the contact persons at these stores are defined as Contacts.

Your daily work consists of getting new customers and to follow up existing ones. In order to do this, you need a sales support system to
-	Keep track of customers and contact persons.
-	Log what is going on / has been going on with each customer.
-	Register sales activities, and get an overview of your own and others activities towards the customers.
-	Log important documents and e-mail.
-	Register requests from customers about bike parts, statuses of requests, and detailing of requests.
-	Show statistics on sales and activities.
-	Search data effectively.
-	Generate order confirmations and send these to customers.

The solution you have been given - and will now work on - already contains some of the main objects of the system, but other than that little functionality. In this course you will be asked to create objects Contacts, Requests and Documents, and eventually most of the functionality needed for the different parts of the system.

<table>
   <tr><td><a href="installation-of-sql-server-mgmt-studio.md"><- Previous</a></td><td align="right"><a href="exercise-01.md">Next -></a></td></tr>
</table>
