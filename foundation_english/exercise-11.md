## Exercise 11 - Genus Apps

**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to Genus App-form modeling.*

### Simple web interface
In this exercise, you will make a simple web interface that shows current activities associated with companies for which the logged in user is responsible. It should also be possible to change the status to Completed.
1. Preparation for Genus Apps:
   1. Deploy to all (you need to deploy to all for things to show in the web browser. It takes about 10 seconds from deployment until changes are reflected on the web).
   2. Verify that you reach the following site:
      * For learners on edu1: http://edu1.genus.net/edu1Y/edu1Y, where Y corresponds to the letter from the username (e.g. http://edu1.genus.net/edu1a/edu1a for usr1a).
      *	For learners on edu2: http://edu2.genus.net/edu2Y/edu2Y, where Y corresponds to the letter from the username (e.g. http://edu2.genus.net/edu2a/edu2a for usr2a).
    
	  As of now, you should only see "CRM Edu1" and an option to log out and close - which is natural as you haven't made an app yet.
2. Create a new App Form and give it a basic layout:
   1. Add a new Form: "My tasks | APP" (Forms -> right-click App -> New)
	  * Navigate to View
      * Name: "My Activities - Main".
      * Check Platform options: Tablet, Web on Phone, Web on Tablet, Web on Desktop.
      * Padding: 24
3. Add a headline
   1. Drag in a Text-control from App Controls:
         ![oppg11fig1.JPG](media/oppg11fig1.JPG)
      * Content: My Activities
      * Foreground Color: Navy
      * Font Size 24
4. Add a repeating section that iterates over Activities ("Not Started" or "In Progress") belonging to Companies which the logged in user is responsible for. Display company name, activity subject and activity status. 
   1. Add data source Activity
  ![oppg11fig2.JPG](media/oppg11fig2.JPG)
   2. Create a Repeating Section that iterates over Activity
      * Drag a GroupBox into the View. 
      * Set Vertical Alignment: Top
      * Bind the GroupBox to the Activity data source.
      * Check "Repeat Content".
      * Sort the GroupBox on Due Time (Descending).
   3. Add text fields for company name, activity subject, deadline and activity state:
      * Drag or double-click 4 Text-controls into the GroupBox.
      * Bind the first to Datasource:Activity Field:Company.Name, and do the equivalent for Activity.Subject, Due(Fx) and Activity.State.Display Name.
        
	    *Note: Although Activity is an unbounded data source and the field is only supposed to show one single text string, you don't have to specify Active Object in DataSource. This is because you are already in the context of an active Activity-object when you are within a repeating Activity section.*
5. Build an App that is bound to the Form you just made.
   * Navigate to Apps under User Interface in Genus Studio.
   * Create a new one which you call "My Activities". Form "My Activities".
   * Check default view for Web and Tablet.
   * Set AppBar Foreground to Navy
   * After saving, define the security of the App. (Properties -> Super Users should be able to "Find and List" and "Read and Execute").
   
6. Deploy to all and verify that you get expected results in the browser. You should see something like this:
![oppg11fig3.JPG](media/oppg11fig3.JPG)
 
7. In the repeating section, add a button for changing the state of the activity to Complete.
   * Add a new task with input Activity (Name: T.Activity, Max Occurences: One). Remember to set Private=false.
   * Under General: set “Enable on Application Server”=true
   * Under Actions: Add a Scope with a Modify Object that changes State to Completed.
   * Save and add security:
  ![oppg11fig4.JPG](media/oppg11fig4.JPG)
   * Drag a Button from App Controls into the repeating section (Activities).
     * Set background color = white, foreground color = navy and border color = navy, show border=true.
     * Name: Complete Activity
   * To run the task, create a command+event and place them both on the button. Remember Two-Way Binding to Activity.Single Selected.
   * Deploy and verify that the button works as expected.
   * Move things around and adjust until you are happy with the display.
  ![oppg11fig5.JPG](media/oppg11fig5.JPG)
  
## Open Data, Local Objects and Map
In this exercise, we will fetch open data from multiple public API’s, store it in local objects and visualize the aggregate data in a map. Note that we do not store any of the data in the database, everything is stored in memory as the client uses the app.
1. Create a new App-form and set the following layout:
   * Mark the view and name it “Main - map”
   * Check all Platforms for the views
   * Save the form and name it “OSLO”, close the form.
2. Select Apps in the navigation pane in the “User Interface” section
   * Right click and new App
   * Name it “OSLO”
   * Select form OSLO
   * Check all default views and set Main - map as default, the app will be available from all devices.
   * Give the app appropriate security
3. Deploy to all and check the website to verify that the app is published and available.
4.	Create the following local data sources (note: occurrences=unbounded and datatypes):
   ![oppg11fig6.JPG](media/oppg11fig6.JPG)
   ![oppg11fig7.JPG](media/oppg11fig7.JPG)
5.	Visualization in Map-control
   * Add Map as Control
     * Edit layers on the Map-control
       - Add Layer
         - Type = Map
         - Server Type = OSM
       - Add Layer
         - Type = Point
         - DS = Bike Stations
         - Location fields
           - Northing = latitude
           - Easting = longitude
           - Coordinate system = WGS84
         - Select an appropriate symbol and set the size to 32px and a color of your choice.
       - Add Layer
         - Type = Point
         - DS = Bus Stops
         - Location fields
           - Northing = longitude (!)
           - Easting = latitude   (!)
           - Coordinate system = UTM32N
         - Select an appropriate symbol and set the size to 32px and a color of your choice.
6. Create the following local tasks: Get stops, Get bikes. Give the tasks appropriate security (Properties > security).
7. The first source of data is Ruter (which plans, coordinates, orders and markets public transport in Oslo and Akershus). Link to API documentation: https://ruter.no/labs/.
   * Open the Get stops-task
   * In the Actions-pane add Consume a REST Service-effect
   * URL: http://reisapi.ruter.no/Line/GetStopsByLineId/30
   * Click the Test-button and click Send. The response of the API call is shown in Response Body. Click Handle Current Response. Open the entry in Response Handlers. Genus has created a mapping from the test-run (this is VERY time consuming for the developer of the app, appreciate Genus :smile:).
   * Configure the response handler as the screenshot illustrates:
      ![oppg11fig8.JPG](media/oppg11fig8.JPG)  
   * When the task “Get stops” is executed, the API is called and the return data is mapped to the specified data source, creating X number of Bus stops with its associated data.
   * To see the result of the call, create a command executing the Get stops task and add it as a On Load Form event. Data will be populated when the form is accessed. Deploy to all and see that the map contains Bus stops.
      ![oppg11fig9.JPG](media/oppg11fig9.JPG)
   
8. The second source of data is Oslo Bysykkel. Link to API documentation: https://developer.oslobysykkel.no/api
9. Open the Get bikes-task.
   * In the Actions-pane add Consume a REST Service-effect
   * URL: https://oslobysykkel.no/api/v1/stations/
   * Header (both in test and request): Client-Identifier:9d0c945ef25d6f01ccc382df111437cc
     ![oppg11fig10.JPG](media/oppg11fig10.JPG)
   * Click the Test-button and click Send. The response of the API call is shown in Response Body. Click Handle Current Response. Open the entry in Response Handlers.
   * Repeat step 7g, but for the Get bike task, to verify that consuming data from the API works in the website.
10. Add popup context to the point layers to show the information (for instance id and name) on click. Customize it (try to be creative, maybe we don’t need label?)
    ![oppg11fig11.JPG](media/oppg11fig11.JPG)
   
    Now we see bus stops (for line 30) and all bike stations. The next step is to show number of bikes available and when the next departure of the bus is.
   
11. We need a new Local Object to store the data temporarily as it is collected in 2 rounds, first stations and then availability. Create the local object inside the local task: name: “availability”, unbounded and fields id, bikes and locks all String. See screenshots.
    ![oppg11fig12.JPG](media/oppg11fig12.JPG)
    ![oppg11fig13.JPG](media/oppg11fig13.JPG)
 
12. Add a REST service to call https://oslobysykkel.no/api/v1/stations/availability with credentials provided above. Map it to the availability DS. Then the data must be copied from availability DS to the bikes DS via a modify object-effect. See screenshot. Note: The filter is important here to ensure correct modifications!
   ![oppg11fig14.JPG](media/oppg11fig14.JPG)
   ![oppg11fig15.JPG](media/oppg11fig15.JPG)
13. Add the local task as On Load Form event as the others. Add bikes and locks to popup content. Deploy to all and verify that you can see name and availability of bikes on the map.
    ![oppg11fig16.JPG](media/oppg11fig16.JPG)
   
14. Optional points for talented business engineers:
    * Get departure data for the bus and display it in the form (hint: use http://reisapi.ruter.no/StopVisit/GetDepartures/3010146). The solution modell contains a partial implementation of this, look at it if you are stuck.
    * Get weather forcasts from YR and dispay bus stops if rain and bike stations otherwise (https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fwww.yr.no%2Fsted%2Fnorge%2FOslo%2Foslo%2Foslo%2Fvarsel.rss).
      
      
</br>
<table>
   <tr><td><a href="oppgave-10.md"><- Previous exercise</a></td><td align="right"><a href="oppgave-12.md">Next exercise -></a></td></tr>
</table>
