## Exercise 3 - Productivity app
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to Web modeling.*

 
### Kanban, Pages and Data Filters
In this exercise we will explore some more web consepts, and demonstrate how choices during modeling affect our ability to reuse parts of the model


####1. Create an Activity Module
*The aim of this exercise is to demonstrate how you can use different Modules to separate and organize part of the total data model. Later we will also show how an app can link to pages from multiple Modules, and pages from a different Module can be used in a Form page*

1. Create a new Module and save it as "Activities". 
2. Add "Activity" and "Activity State" from the Data Sources tab (Currently, you can't add code domains from the Data Diagram).

####2. Display Activities in a Kanban control
*The Kanban control is a very visual way of displaying processes where objects move through different states. We will use this to display activities. We will show how the same page can reused later in a different context.*

1. In the Activities module, create a new page of the type "Canvas", and name it "Activities - Kanban". Select the "None" viewport layout. Go to Settings and change the Title to just "Activities", and select an appropriate icon (e.g. Basic-Task)
2. Add a public interface data set: Name: "Activities", Data Source: "Activity", Occurrence: "Many"
3. Add a filtered data set: Name: "Activity States", Data Source: "Activity State", Occurrence: "Many", Data Filter: "Read all"
4. Navigate to the Canvas Tab, find Controls under Insert Content. Add a Kanban Control (directly inside the "content" Viewport Area).
5. On the Kanban Control, select the following properties:
   * List Data Binding: "Activity States"
   * Card Data Binding: "Activities"
   * Card to List Data Binding: "Activities.State"
   * Sort Order: "Sorting"
6. On the Card Template (click on the "(empty)" on "LIST0"), you can design the layout of a kanban Card. Add a Text Control inside the Card Template. Bind the value to Activities.DisplayName, and choose the Style "Heading 3". Add one more Text to the template and bind it to Activities.Description. Keep the style "Body 2". Save and close the page.

####3. Create the Productivity App

1. Return to the main window of Genus Studio, and navigate to Apps in the navigation pane.
2. Create a New app, and name it "Productivity". Also choose "Productivity" as the title. Pick an appropriate icon (e.g. Basic-Task).
3. Navigate to Sitemap. Add an Area and use the Label "Productivity".
4. Drag a link of the type "Page" and drop it on the Productivity area. Select "Activities - Kanban (Activities)" as your target. This is the view you just created. Under Data Filter, select "Read all".
5. In the bottom of the window, select Drawer Appearance "Expanded" and Landing Page Link "Productivity/Activities".
6. Close the app. Now set security on the app, by right-clicking on the app and selecting properties. Go to the security tab, click tha "Add..." button, then "Advanced" and add the group "Standard". Click OK twice. Then select "Find and List" and "Read and Execute" on the list below.
7. Test the new app. It should look like the figure below.
![oppg02fig4.JPG](media/oppg02fig4.JPG)

####3. Data Filters and pages

1. We often want to look at a subset of data, without having to perform a search. To do this we need to create a data filter. Open the CRM Module, and navigate to "Data Filters" in the navigation pane on the left.
2. Create a new data filter, and name it "My Companies". Select the data source "Company".
3. Add the conditions "Company.Responsible = Active User Account (User)" and "Company.State = Active". Sort By name and press OK. Save changes on the module.
![oppg02fig5.JPG](media/oppg02fig5.JPG)

4. Now we are going to reorganize our CRM App, and utilize the ne filter. Open the CRM App. In the site map, change the label of the Companies link to "Search", by clicking on the vertical "...", selecting Text and entering the label. 
5. Drag a link of the type "Pages" and drop it on the CRM Area. Change the label to "Companies". Drag the Search link onto the Companies Pages link (see figure further down).
6. Drop a new Page-link onto the Companies Pages link. Name the new page link "My Companies". Select the Companies View as your target, and also select the "My Companies" data filter. Select default = Yes. 
7. Select CRM/Companies as your Landing Page Link. Your sitemap should now look like this:
![oppg02fig6.JPG](media/oppg02fig6.JPG)
8. Check out the new sitemap in your browser as well, by refreshing. Your can navigate between My Companies and Search from the dropdown next to the title.
![oppg02fig7.JPG](media/oppg02fig7.JPG)

####4. Incorporate the Activities Kanban in the Company form

1. Open the Company form in the CRM Module. On the tab control, clik on "Related places". (Here, you can add tabs from other modules, that only load data after you navigate to them).
2. Add a new item with the following properties:
   * Name: "Activities"
   * Target Type: "Page"
   * Target: "Activities - Kanban"
   * Data Filter: "Read related"
3. Save and see the results in the browser. Remember to open a Company that has activities related to it.
4. Your results should look like the figure below. Try moving cards between lists to change the state of the activity.
![oppg02fig16.JPG](media/oppg02fig16.JPG)

### Themes

*You can use themes to customize the visual expression of the application, to, for instance, match that of the application owners organizaion*

1. In the very bottom of the navigation pane in Genus Studio, navigate to Themes. Create a new Theme and name it "Main Theme"
2. Select your favorite color as primary in both light mode and dark mode (e.g. #bf3711).
3. Navigate to the CRM app, and change the theme to be "Main Theme". Save and check the results on the web.

<table>
   <tr><td><a href="exercise-02.md"><- Previous</a></td><td align="right"><a href="exercise-04.md">Next -></a></td></tr>
</table>
