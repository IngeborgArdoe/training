## Exercise 8-2 - Request

###8.2.1. Create Object Class «Request»

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



###8.2.2. Make a view for "Requests" in the Tab control in the Company-form

Create a View for Requests and add it in the Company Form. It should not be possible to delete Requests. However, the view in the Company form should filter out Requests with State="Canceled".

*Comment: Feel free to add the "New" command to the Action Bar. Find a meaningful symbol for Request.*

###8.2.3. Create a form for Requests

Model a Request-form with a view that displays all Request info. Add an activation from the Requests view.

*Guidance: If needed, take a look at the earlier View/Form exercise. Make sure Activating a row opens the relevant Request, and add support for adding new Requests.*

###8.2.4. Add a Request View to the Apps Sitemap

Add a shortcut (name "Requests") to the Navigation Pane that points to the Request view, and shows open Requests.

###8.2.5. OPTIONAL: Make a rule "Set Closed Date and Canceled Date when State changed"

This rule should change Closed Date if State is set to "Closed" (and NULL otherwise) and Canceled Date if State is set to "Canceled" (and NULL otherwise).

###8.2.6. OPTIONAL: Make actions "Close Request", "Reopen Request" and "Cancel Request"

Create actions and publish them the appropriate places. Set enabling and visibility based on current state where relevant. E.g. so that "Close Request" is enabled when State="Open", "Re-open Request" is enabled when State="Canceled"/"Closed", and "Cancel Request" is enabled when State="Open".

###8.2.7. OPTIONAL: Make Request "read-only" if State <> "Open"

Force all fields in the Request-form to be "Read Only"/Not enabled if State is not equal to "Open".

*Tip: You can determine when a Control is "Read Only" and not by defining conditions in the menu on the right-hand side of the editor. Luckily, you don't have to define one condition per field, you can also do it per Group. Everything placed within the Group will be "Read Only" if the condition is true.*




<table>
   <tr><td><a href="exercise-10-1.md"><- Previous</a></td><td align="right"><a href="exercise-11-1.md">Next -></a></td></tr>
</table>
