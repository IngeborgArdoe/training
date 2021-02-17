## Exercise 13.2 - Web
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to Web modeling.*

### Simple web application
In this exercise, you will make a simple web interface for customer relation management.

####1. Preparations

1. Open the origin namespace in your web browser. Here you can see changes immedietly after they are saved. The origin URL is *https://edu-usr{X}-origin.edu.genus.net/*
2. As of now, you should only see built in apps, such as, Analytics and Insights, Genus Desktop and Genus Studio, as well as a header with options to log out, change language, etc.
	
####2. Create a new CRM Module

1. Open Genus Studio. Navigate to Modules, and create new module
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
     
####5. Check that your new App is available in origin

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
2. Go to the Data Sets tab. Add a Public Interface Data Set and name it "Action: Company". Choose the Company Data Source, Occurences "One" and flow "In". The Data Set is the set of data that the Client Action is aware of. We do not select any data filter inside the Client Action, this is done later when we link the Client Action in a page or inside another action.
3. Navigate to the Action Flow tab. Drag a "Navigate to Page" into the empty Action Flow in the middle of the window. Under Content --> Page, select the Company Form. Under Data filter, select "Action: Company". Your action flow should now look like the figure below. Save and close the Client Action.
![oppg13fig9.JPG](media/oppg13fig9.JPG)

4. Open the Companies view. Open the Control View, by toggling the button up to the left (green button on the figure below), or "Ctrl+Shift+L". Here you can navigate the different levels of your page. You can use Esc to navigate to the level above, just like in a desktop form. Go to the "Table" level.
5. In the Table level, Change the On Activate Interaction to "Navigate to Company Form" (you might need to close and open the view if the action is not visible). Under Data Exchange, select Company in the Data Column of the "Action: Company" row.  
![oppg13fig10.JPG](media/oppg13fig10.JPG)
When you activate a row in the View, it will now send the Data Set from the context to the Client Action. The Client Action will navigate to the Company form, transfering the Data Set further. See the results in the browser.
![oppg13fig11.JPG](media/oppg13fig11.JPG)

####Bonus: 
Create a Contacts View and add it as a page to the Tab Control in the Company Form

  
### Components, Viewports, Tabs and Kanban
In this exercise we will explore some more web consepts, and demonstrate how choices during modeling affect our ability to reuse parts of the model

####1. Create a new Component for Company Summary
*Components are pages that can be parts of other pages. By strategically creating components, we can reuse part of the user interface in another context. Firstly, we will make a component with a summary of key fields from the company, and include this component in the Company Form*

1. Open the CRM Module. Navigate to Components, and create a new component of the type "form". Name it "Company Summary" and select Company as the Master Data Source.
2. Pick the "Left/right split" Viewpoint Layout. Go to settings and change the title to "Summary".
3. Go to the form tab and add relavant data fields by dragging fields from the data source into the left or the right Viewport Area (you can also use double-click). By default, the Input Field control will be selected for text fields, and Dropdown for complex fields (such as Responsible), etc. If other controls are preferred, you can hover over the field to see which controls are available for the data type (for instance, Customer No should be a display field, since it is read-only). You can also select controls from the Controls tab of the Insert Content pane. A good way to organize the fields can be to put basic info fields on the left and address fields on the right. Add text controls with style "Heading 2" to make the page more readable. See figure below. Save the component.
![oppg13fig12.JPG](media/oppg13fig12.JPG)
4. Open the Company form. Add a Tab Control under the text. Under pages, click on the "(no items)" to open the Pages dialog. Add an item and name it "Summary". Choose Target Tyoe "Component" and Target "Company Summary". Under Data filter, choose Transfer all --> Company. Save and check the results in the browser.
![oppg13fig13.JPG](media/oppg13fig13.JPG)

####2. Create a Viewport that is mobile friendly
*Phones are characterized by their narrow screen. A page that looks good on a PC screen, doesn't nessisarily look good on a phones. We use different Viewports to fix this, without having to make a completely new page.*

1. Open the Company Summary Component. Go to the viewport tab, and add a new Viewport (not a new Viewport Area). Under breakpoint, select "Medium (< 640px)". Keep the suggested name "Phone", and click ok.
2. In the phone Viewport, click on the "+"-button in the bottom of the screen to add a new row. Then click on the vertical "..." in the right column and delete that column. Select the top row by clicking on the left side near the "1 fr". Change the Hight Unit to "Fit to Content". Finally, drag the "right" Viewport Area to the new bottom row. The viewport port should now look like the figure below.
![oppg13fig14.JPG](media/oppg13fig14.JPG)

3. Go to the Form tab, to preview how the component will look on narrow screens. You can change the viewport are from the dropdown list on the above the page designer. Save all changes.
4. Open the browser, and adjust the window width to observe the responsive behaviour when the width is less than 640px. The result should look like this:
![oppg13fig15.JPG](media/oppg13fig15.JPG)


####3. Create an Activity Module
*The aim of this exercise is to demonstrate how you can use different Modules to separate and organize part of the total data model. Later we will also show how an app can link to pages from multiple Modules, and components from a different Module can be used in a Form page*

1. Create a new Module and save it as "Activities". 
2. Add "Activity" and "Activity State" from the Data Sources tab (Currently, you can't add code domains from the Data Diagram).

####4. Display Activities in a Kanban control
*The Kanban control is a very visual way of displaying processes where objects move through different states. We will use this to display activities. We create this as a component, so that we can later reuse it in a different context.*

1. In the Activities module, create a new component of the type "Canvas", and name it "Activities - Kanban". Select the "None" viewport layout. Go to Settings and change the Title to just "Activities"
2. Add a public interface data set: Name: "Activities", Data Source: "Activity", Occurrence: "Many"
3. Add a filtered data set: Name: "Activity States", Data Source: "Activity State", Occurrence: "Many", Data Filter: "Read all"
4. Navigate to the Canvas Tab, find Controls under Insert Content. Add a Kanban Control (directly inside the "content" Viewport Area).
5. On the Kanban Control, select the following properties:
   * List Data Binding: "Activity States"
   * Card Data Binding: "Activities"
   * Card to List Data Binding: "Activities.State"
   * Sort Order: "Sorting"
6. On the Card Template (click on the "(empty)" on "LIST0"), you can design the layout of a kanban Card. Add a Text Control inside the Card Template. Bind the value to Activities.Subject, and choose the Style "Heading 3". Add one more Text to the template and bind it to Activities.Description. Keep the style "Body 2". Save and close the component.

####5. Incorporate the Activities Kanban in the Company form

1. Open the Company form in the CRM Module. On the tab control, clik on "Related places". (Here, you can add tabs from other modules, that only load data after you navigate to them).
2. Add a new item with the following properties:
   * Name: "Activities"
   * Target Type: "Component"
   * Target: "Activities - Kanban"
   * Data Filter: "Read related"
      * Filter target data set: "Activities"
      * On objects in source data set: "Company"
      * Where the source is related to the target in a: "One to Many Relationship"
      * By outbound field in target: "Activities.Company"
3. Save and see the results in the browser. Remember to open a Company that has activities related to it.
4. Your results should look like the figure below. Try moving cards between lists to change the state of the activity.
![oppg13fig16.JPG](media/oppg13fig16.JPG)

### Themes

*You can use themes to customize the visual expression of the application, to, for instance, match that of the application owners organizaion*

1. In the very bottom of the navigation pane in Genus Studio, navigate to Themes. Create a new Theme and name it "Main Theme"
2. Select your favorite color as primary in both light mode and dark mode (e.g. #bf3711).
3. Navigate to the CRM app, and change the theme to be "Main Theme". Save and check the results on the web.

<table>
   <tr><td><a href="exercise-12.md"><- Previous</a></td><td align="right"><a href="exercise-14.md">Next -></a></td></tr>
</table>
