## Exercise 2 - Human Resources app
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to Web modeling.*

### Modules, pages and apps
In this exercise, you will make a simple web interface for Human Resources Management.

####2. Create a new Organization Module

1. Open Genus Studio. Navigate to Modules, and create new module
2. Name it "Orgnaization" and save it
3. Add the Person and Department data sources to the module by going to "Data Diagram", right-click and choose "Insert" - "Object Classes...". Select the object classes Person and Department, and choose OK. Right-click on the two boxes and select "Enable as Data Source".
	   
####3. Create a Person View

1. In the navigation pane on the left, go to pages and add a new view. Name it "Persons" and select Person as the Master Data Source
2. Note that a Master Data Set "Person" has been created. This Data Set is the set of data that is displayed in the view. We do not select any data filter inside the view, this is done later when we link the view in an app or an action.

3. Go to the View tab. Here you can drag fields from the Person data source to be displayed in the view. Add a few major columns such as User Name, First Name, Last Name, Department, Email, Type and State
![oppg02fig1.JPG](media/oppg02fig1.JPG)
4. Go to settings, and select the title "Persons" and an appropriate icon (e.g. Basic-User). Save all changes
   
####4. Create a new App

1. Return to the main window of Genus Studio, and navigate to Apps in the navigation pane.
2. Create a New app, and name it "Human Resources". Also choose "Human Resources" as the title. Pick an appropriate icon.
3. Navigate to Sitemap. The sitemap is devided into three levels; Area, Group and Link, where Group is optional.
4. Add an Area and use the Label "Human Resources".
5. Drag a link of the type "Page" and drop it on the Human Resources area. Select "Persons (Organization)" as your target. Under Data Filter, select "Read all" This is the view you just created. Flip "Enable Search" to "Yes".
6. In the bottom of the window, select Drawer Appearance "Expanded" and Landing Page Link "Human Resources/Persons". (This means that drawers will appear on the left, and you will land on the Persons view by default when opening the app). 
7. Save the app. Your app should now look like this:
![oppg02fig2.JPG](media/oppg02fig2.JPG)
8. Close the app. Now set security on the app, by right-clicking on the app and selecting properties. Go to the security tab, click tha "Add..." button, then "Advanced" and add the group "Standard". Click OK twice. Then select "Find and List" and "Read and Execute" on the list below.
     
####5. Check that your new App is available in origin

1. Go to the startpage or your application in the browser and refresh the page. The new app Human Resources should now be visible
![oppg02fig3.JPG](media/oppg02fig3.JPG)
2. Enter the Human Resources app. You should now see the sitemap on the left, and the companies view on the rest of the screen. The table is empty, because no data filter is set. You can perform a search (e.g. Name starting with "a") in order to display some data.
![oppg02fig4.JPG](media/oppg02fig4.JPG)

####7. Create a Company Form

1. Now we are going to create a form that we can open by clicking on a row in the Companies view. In the CRM Module, navigate to pages and add a Form page. Name it "Company" and select Company as the Master Data Source. 
2. Select Viewport Layout "None" and press OK (we will cover Viewports later).
3. Note that a Master Data Set "Company" has been created. This Data Set is the set of data that is displayed in the form. We do not select any data filter inside the form, this is done later when we link the form in an app or an action.
4. Navigate to the Form tab. Here you can design your form layout. Under "Insert Content", select Controls, and drag a Text control onto the form (inside the Viewport Area "Content"). Bind the Value to Company.Name by clicking on the vertical "...", select Data Binding, and choose the Name Field. Select Style = Heading 1. Your form should now look like the figure below. We will add more controls to the form later.
![oppg02fig8.JPG](media/oppg02fig8.JPG)

5. Go to the settings tab. Add the title "Company" and an appropriate icon (e.g. Basic-Company). Save all changes.
 
####8. Create a new Client Action to navigate from the view to the form
*In order to navigate to the form from the Companies View, we need to create a Client action that takes in one company and navigates to the Company form with that Company as input*

1. Return to the CRM Module. In the navigation pane, navigate to Client Actions. Client Actions are actions that can be executed directly in the browser, without a server roundtrip, and can only work on data that is already in the memory. Add a new Client Action and name it "Navigate to Company Form".
2. Go to the Data Sets tab. Add a Public Interface Data Set and name it "Task: Company". Choose the Company Data Source, Occurences "One" and flow "In". The Data Set is the set of data that the Client Action is aware of. We do not select any data filter inside the Client Action, this is done later when we link the Client Action in a page or inside another action.
3. Navigate to the Action Flow tab. Drag a "Navigate to Page" into the empty Action Flow in the middle of the window. Under Content --> Page, select the Company Form. Under Data filter, select "Task: Company". Your action flow should now look like the figure below. Save and close the Client Action.
![oppg02fig9.JPG](media/oppg02fig9.JPG)

4. Open the Companies view. Open the Control View, by toggling the button up to the left (green button on the figure below), or "Ctrl+Shift+L". Here you can navigate the different levels of your page. You can use Esc to navigate to the level above, just like in a desktop form. Go to the "Table" level.
5. In the Table level, Change the On Activate Interaction to "Navigate to Company Form" (you might need to close and open the view if the action is not visible). Under Data Exchange, select Company in the Data Column of the "Task: Company" row.  
![oppg02fig10.JPG](media/oppg02fig10.JPG)
When you activate a row in the View, it will now send the Data Set from the context to the Client Action. The Client Action will navigate to the Company form, transfering the Data Set further. See the results in the browser.
![oppg02fig11.JPG](media/oppg02fig11.JPG)

####Bonus: 
Create a Contacts View and add it as a page to the Tab Control in the Company Form

  
####1. Create a new Component for Company Summary
*Components are pages that can be parts of other pages. By strategically creating components, we can reuse part of the user interface in another context. Firstly, we will make a component with a summary of key fields from the company, and include this component in the Company Form*

1. Open the CRM Module. Navigate to Components, and create a new component of the type "form". Name it "Company Summary" and select Company as the Master Data Source.
2. Pick the "Left/right split" Viewpoint Layout. Go to settings and change the title to "Summary".
3. Go to the form tab and add relavant data fields by dragging fields from the data source into the left or the right Viewport Area (you can also use double-click). By default, the Input Field control will be selected for text fields, and Dropdown for complex fields (such as Responsible), etc. If other controls are preferred, you can hover over the field to see which controls are available for the data type (for instance, Customer No should be a display field, since it is read-only). You can also select controls from the Controls tab of the Insert Content pane. A good way to organize the fields can be to put basic info fields on the left and address fields on the right. Add text controls with style "Heading 2" to make the page more readable. See figure below. Save the component.
![oppg02fig12.JPG](media/oppg02fig12.JPG)
4. Open the Company form. Add a Tab Control under the text. Under pages, click on the "(no items)" to open the Pages dialog. Add an item and name it "Summary". Choose Target Tyoe "Component" and Target "Company Summary". Under Data filter, choose Transfer all --> Company. Save and check the results in the browser.
![oppg02fig13.JPG](media/oppg02fig13.JPG)

####2. Create a Viewport that is mobile friendly
*Phones are characterized by their narrow screen. A page that looks good on a PC screen, doesn't nessisarily look good on a phones. We use different Viewports to fix this, without having to make a completely new page.*

1. Open the Company Summary Component. Go to the viewport tab, and add a new Viewport (not a new Viewport Area). Under breakpoint, select "Medium (< 640px)". Keep the suggested name "Phone", and click ok.
2. In the phone Viewport, click on the "+"-button in the bottom of the screen to add a new row. Then click on the vertical "..." in the right column and delete that column. Select the top row by clicking on the left side near the "1 fr". Change the Hight Unit to "Fit to Content". Finally, drag the "right" Viewport Area to the new bottom row. The viewport port should now look like the figure below.
![oppg02fig14.JPG](media/oppg02fig14.JPG)

3. Go to the Form tab, to preview how the component will look on narrow screens. You can change the viewport are from the dropdown list on the above the page designer. Save all changes.
4. Open the browser, and adjust the window width to observe the responsive behaviour when the width is less than 640px. The result should look like this:
![oppg02fig15.JPG](media/oppg02fig15.JPG)


<table>
   <tr><td><a href="exercise-01.md"><- Previous</a></td><td align="right"><a href="exercise-03.md">Next -></a></td></tr>
</table>
