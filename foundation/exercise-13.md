## Exercise 13 - Web
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to Web modeling.*

### Simple web application
In this exercise, you will make a simple web interface for customer relation management.

####1. Preparations

1. Open the origin namespace in your web browser. Here you can see changes immedietly after they are saved. The origin URL is *<your assigned solution>-origin.genus.net*
2. As of now, you should only built in apps, such as, Analytics and Insights, Genus Desktop and Genus Studio, as well as a header with options to log out, change language, etc.
	
####2. Create a new CRM Module

1. Navigate to Modules, and create new module
2. Name it "CRM" and save it
3. Add the Company and Contact data sources to the module by going to "Data Diagram", right-click and choose "Insert" - "Object Classes...". Select the object classes Company and Contact, and choose OK. Right-click on the two boxes and select "Enable as Data Source".
	   
####3. Create a Company View

1. In the navigation pane on the left, go to pages and add a new view. Name it "Companies" and select Company as the Master Data Source
2. Note that a Master Data Set "Company" has been created. This Data Set is the set of data that is displayed in the view. We do not select any data filter inside the view, this is done later when we link the view in an app or an action.

3. Go to the View tab. Here you can drag fields from the Company data source to be displayed in the view. Add a few major columns such as Customer No, Org No, Name, Responsible and Status
![oppg13fig1.JPG](media/oppg13fig1.JPG)
4. Go to settings, and select the title "Companies" and an appropriate icon (e.g. Basic-Company). Save all changes
   
####4. Create a new App

1. Return to the main window of Genus Studio, and navigate to Apps in the navigation pane.
2. Create a New app, and name it "CRM". Also choose CRM as the title. Pick an appropriate icon.
3. Navigate to "Sitemap". The sitemap is devided into three levels; Area, Group and Link, where Group is optional.
4. Add an Area and use the Label "CRM".
5. Drag a link of the type "Page" and drop it on the CRM area. Select "Companies (CRM)" as your target. This is the view you just created. Flip "Enable Search" to "Yes".
6. In the bottom of the window, select Drawer Appearance "Expanded" and Landing Page Link "CRM/Companies". (This means that drawers will appear on the left, and you will land on the Companies view by default when opening the app.) 
7. Save the app. Your app should now look like this:
![oppg13fig2.JPG](media/oppg13fig2.JPG)
8. Set security on the app, by right-clicking on the app (the same way as for actions).
     
####5. Check that your new App is availible in origin

1. Go to the startpage or your application in the browser and refresh the page. The new app CRM should now be visible
![oppg13fig3.JPG](media/oppg13fig3.JPG)
2. Enter the CRM app. You should now see the sitemap on the left, and the companies view on the rest of the screen. The table is empty, because no data filter is set. You can perform a search (e.g. Name starting with "a") in order to display some data.
![oppg13fig4.JPG](media/oppg13fig4.JPG)

####6. Data Filters and pages

1. We often want to look at a subset of data, without having to perform a search. To do this we need to create a data filter. Open the CRM Module, and navigate to "Data Filters" in the navigation pane on the left.
2. Create a new data filter, and name it "My Companies". Select the data source "Company".
3. Add the conditions "Company.Responsible = Active User Account (User)" and "Company.State = Active". Sort By name and press OK. Save changes on the module.
![oppg13fig5.JPG](media/oppg13fig5.JPG)

4. Now we are going to reorganize our CRM App, and utilize the ne filter. Open the CRM App. In the site map, change the label of the Companies link to "Search", by clicking on the vertical "...", selecting Text and entering the label. 
5. Drag a link of the type "Pages" and drop it on the CRM Area. Change the label to "Companies". Drag the Search link onto the Companies Pages link (see figure further down).
6. Drop a new Page-link onto the Companies Pages link. Name the new page link "My Companies". Select the Companies View as your target, and also select the "My Companies" data filter. Select default = Yes. 
7. Select CRM/Companies as your Landing Page Link. Your sitemap should now look like this:
![oppg13fig6.JPG](media/oppg13fig6.JPG)
8. Check out the new sitemap in your browser as well, by refreshing. Your can navigate between My Companies and Search from the dropdown next to the title.
![oppg13fig7.JPG](media/oppg13fig7.JPG)

####7. Create a Company Form

1. Now we are going to create a form that we can open by clicking on a row in the Companies view. In the CRM Module, navigate to pages and add a Form page. Name it "Company" and select Company as the Master Data Source. 
2. Select Viewport Layout "None" and press OK (we will cover Viewports later).
3. Note that a Master Data Set "Company" has been created. This Data Set is the set of data that is displayed in the form. We do not select any data filter inside the form, this is done later when we link the form in an app or an action.
4. Navigate to the Form tab. Here you can design your form layout. Under "Insert Content", select Controls, and drag a Text control onto the form (inside the Viewport Area "Content"). Bind the Value to Company.Name by clicking on the vertical "...", select Data Binding, and choose the Name Field. Select Style = Heading 1. Your form should now look like the figure below. We will add more controls to the form later.
![oppg13fig8.JPG](media/oppg13fig8.JPG)

5. Go to the settings tab. Add the title "Company" and an appropriate icon (e.g. Basic-Company). Save all changes.
 
####8. Create a new Client Action to navigate from the view to the form
*In order to navigate to the form from the Companies View, we need to create a Client action that takes in one company and navigates to the Company form with that Company as input*

1. Return to the CRM Module. In the navigation pane, navigate to Client Actions. Client Actions are actions that can be executed directly in the browser, without a server roundtrip, and can only work on data that is already in the memory. Add a new Client Action and name it "Navigate to Company Form".
2. Go to the Data Sets tab. Add a Public Interface Data Set and name it "Task: Company". Choose the Company Data Source, Occurences "One" and flow "In". The Data Set is the set of data that the Client Action is aware of. We do not select any data filter inside the Client Action, this is done later when we link the Client Action in a page or inside another action.
3. Navigate to the Action Flow tab. Drag a "Navigate to Page" into the empty Action Flow in the middle of the window. Under Content --> Page, select the Company Form. Under Data filter, select "Task: Company". Your action flow should now look like the figure below. Save and close the Client Action.
![oppg13fig9.JPG](media/oppg13fig9.JPG)

4. Open the Companies view. Open the Control View, by toggling the button up to the left (green button on the figure below), or "Ctrl+Shift+L". Here you can navigate the different levels of your page. You can use Esc to navigate to the level above, just like in a desktop form. Go to the "Table" level.
5. In the Table level, Change the On Activate Interaction to "Navigate to Company Form" (you might need to close and open the view if the action is not visible). Under Data Exchange, select Company in the Data Column of the "Task: Company" row.  
![oppg13fig10.JPG](media/oppg13fig10.JPG)
When you activate a row in the View, it will now send the Data Set from the context to the Client Action. The Client Action will navigate to the Company form, transfering the Data Set further. See the results in the browser.
![oppg13fig11.JPG](media/oppg13fig11.JPG)
  
### Components, Viewports, Tabs and Kanban
In this exercise we will explore some useful web concepts, and use them to make our form more interactive and productive. 

####1. Create a new Component for Company Summary

####2. Add Tab Control to the Company form

####3. Add Create an Activity Module

####4. Display Activities in a Kanban control

####5. Incorporate the Activities Kanban in the Company form
      
### Themes
      
<table>
   <tr><td><a href="exercise-12.md"><- Previous</a></td><td align="right"><a href="exercise-14.md">Next -></a></td></tr>
</table>
