## Exercise 3 - Forms

####1. Create a Form: «Contact»

You will now make a Form for registering and opening customer Contact information.
1. In Studio, navigate to User Interaction -> Modules. Access the Company module. In Pages, Right-click -> New ->  Form. Save it right away with Master Data Source "Contact" and name «Contact Details. Pick the Default "None" for Viewport Layout.
2. Data Sources (upper-left corner): This is where you add the object(s) that you want to show or utilize in the Form. You already defined «Contact» as the Master Data Source when creating the form. Note that:
   1. We want to be able to send Contact-data into the form and get data back. This means that the dataset needs to have "Included in Public Interface" activated.
   2. The form Data Source «Contact» is restricted to occurence = "One" by default when it is set as the Master Data Source, which means that only one Contact-object can exist in the Form. This has to be done in order to allow the properties of Contact to be shown in fields. "Unbound" is used for data sources that you want to list (e.g. in a Grid, Table, etc).

![oppg3fig1.JPG](media/oppg3fig1.JPG)

3. Viewport: Go to Viewport and rename the Area content to "Contact Details" (double click for edit mode).
4. Navigate to "Form". Toggle the "Show Control View Pane" in the ribbon. You can now see the empty Viewport Area you just renamed.

5. Navigate to "Controls" in the Insert Content section. Add a Container - either by double clicking or drag and dropping. The second section shows available controls for data fields. These can be added to the form and bound to data fields here, but a quicker route follows:
6. Navigate back to the Data tab in the Content-section. You can now add data fields to your form, with the data binding pre-defined. Hovering over a data field will show you the available control types for the given data field. Give some thought to the data type and amount of data being displayed when choosing the control type. For instance, radio buttons and dropdown menus are great for small selections of data, but may become overwhelming if applied to the data field for Company with several hundreds of instances. Here, a Lookup may increase user friendliness.
7. Save your work and close the window.

As an end result, we want to view Contact Details in combination with related activities and documents.
We will start by using our "Contact Details" form as a Page in a larger form.  

8. We want Create a new Form named "Contact", with the same Master Data Source - Contact. Pick the Default "None" for Viewport Layout.
Viewport: Go to Viewport and rename the Area content to "Contact".
9. Go to Form, and navigate to Controls. Add the container "Tab Control".
10. Go to the Tab Control Settings at the right hand side. Click on Pages under "Content". Add a Page, add the "Contact Details"-form you just created, and name the page "Contact Details". We need to define the data filter, so the "Contact Details"-form will read data for the same Contact as the "Contact"-form. Click on "No filters defined" and then click on the menu. Choose "Transfer All" and "Contact (0:1). Because both forms have Contact as their Master Data Source, they both contain maximum one instance of Contacts and the filter can simply transfer this instance.




4. Add Container «Tab Sheets». Click inside the first tab to mark the Group it contains. Change the name to "General".
  Add a new tab: Move one level out (hint: press the Esc-button), and double-click on "Group" in the Desktop Control menu. Name the new tab «Activities» (content will come later).
  Add also a tab named «Mail» to the Tab Sheet (content will come later).
5. In tab «General», you will add the fields for Contact.
   *Guidance: You will be asked to model a «Contact log» at the right hand side of this display in an upcoming task. Hence, we recommend the following layout for the «General»-tab:*
![oppg3fig2.JPG](media/oppg3fig2.JPG)

   Select OUTER GROUPBOX (or whatever you called it in your solution) and change «Container Type» to «Group» in the menu on the left. This will remove the frame of the box. Do the same for LEFT GROUPBOX and RIGHT GROUPBOX. Fields can be dragged from the right menu and dropped into the form after changing the following:

![oppg3fig3.JPG](media/oppg3fig3.JPG)

   After having made the change above, you can drag Data Properties from the Contact data source into the Groups located in the «General»-tab. A proposed layout control is selected by default (e.g. TextEdit is proposed for «First Name»). If you drag Company into the form, a ComboBoxEdit - which is a dropdown - is suggested. This may be unfortunate when there are a lot of objects to choose from. Instead you can press Shift while dragging the Company into the form, and you will get a SearchBoxEdit rather than a ComboBoxEdit - increasing the user friendliness.

<table>
   <tr><td><a href="exercise-02-2.md"><- Previous</a></td><td align="right"><a href="exercise-03-2.md">Next -></a></td></tr>
</table>
