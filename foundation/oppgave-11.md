# Oppgave 11 - Genus Apps

*SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon med intro til modellering av Genus Apps-forms.*

## Enkelt web-grensesnitt
I denne oppgaven skal du lage et enkelt web-grensesnitt for å vise aktuelle aktiviteter for selskaper innlogget bruker er ansvarlig for – med mulighet for å sette status til Completed.
1. Klargjør for Genus Apps:
    * I Studio: Gi Super Users privilege: Sign in as an app user
    * Deploy to all (du må deploye to all for at det du gjør skal vises i nettleser. Det tar omtrent ti sekunder fra du deployer til endringene blir gjenspeilet på web).
    * Verifiser at du når følgende side:
      * For dere på edu1: http://edu1.genus.net/edu1Y/edu1Y, hvor Y erstattes med bokstav fra brukernavn (feks http://edu1.genus.net/edu1a/edu1a for usr1a).
      *	For dere på edu2: http://edu2.genus.net/edu2Y/edu2Y, hvor Y erstattes med bokstav fra brukernavn (feks http://edu2.genus.net/edu2a/edu2a for usr2a).
    
      Per nå vil det kun stå "CRM Edu1" med mulighet for å logge ut og lukke - det er ikke så rart siden vi ikke har laget noen app ennå.
2.	Opprett en ny Form ment til App og sett basic layout på denne:
    * Opprett en ny Form: "My tasks | APP"
      * Først gå til View.
      * Name: "My Activities - Main".
      * Huk av for Platforms: Tablet, Web on Phone, Web on Tablet, Web on Desktop.
      *  Padding: 24
3.	Legg til en overskrift
    * Dra inn en Text-controller fra App Controls:
      ![oppg11fig1.JPG](media/oppg11fig1.JPG)
      * Content: My Activities
      * Foreground Color: Navy
      * Font Size 24
4. Legg til en repeating section som repeterer over aktiviteter (Not started or In Progress) som tilhører Companies som innlogget bruker er ansvarlig for. Vis selskapsnavn, Activity’s subject og status vises ut til bruker.
   * Legg til Activity-datakilde
  ![oppg11fig2.JPG](media/oppg11fig2.JPG)
   * Lag en Repeating Section som repeterer over Activity
      * Dra inn en GroupBox i Viewet. Denne GroupBox-en må dras inn fra App Controls
      * Sett Vertical Alignment: Top
      * Bind GroupBoxen til Activity-datakilden.
      * Huk av for “Repeat Content under properties på GroupBox-en.
      * Sett på sortering på GroupBox-en med sorteringsnøkkel Due Time (Descending).
    * Legg inn tekstfelter for selskapsnavn, aktivitetens Subject, frist og aktivitetens State: 
      * Dra eller dobbeltklikk inn fire tekstfelt i GroupBox-en.
      * Bind den første til Datasource: Activity Field: Company.Name og gjør tilsvarende for Activity.Subject, Due(Fx) og Activity.State.Display Name
        
        Merk: Selv om Activity er en unbounded datasource og feltet bare skal vise ett enkelt tekstfelt trenger vi ikke spesifisere Active Object i DataSource. Dette er fordi vi allerede er i kontekst av et aktivt Activity-objekt når vi er i repeating section over Activity.
5. Opprett en App som bindes til Formen du akkurat lagde
    * Gå til Apps under User Interface i Genus Studio.
    * Opprett en ny som du kaller My ACctivities. Form My Activities
    * Huk av for default view for Web og Tablet
    * Sett AppBar Foreground til Navy
    * Etter du har lagret, sett security på Appen. (Properties=> Super 
  Users skal kunne Find and List og Read and Execute).
6. Deploy to all og sjekk i browseren at du får forventede resultater (noe a la dette)
![oppg11fig3.JPG](media/oppg11fig3.JPG)
 
7. Legg til knapp i repeating section for å endre state på aktiviteten til Complete 
    * Legg til en ny task med input Activity (Name: T.Activity, Max Occurences: One). Husk å sett private=false.
    * Under General sett “Enable on Application Server”=true
    * Under Actions: Legg til et Scope med en Modify Object som setter State til Completed.
    * Lagre og sett security på tasken:
  ![oppg11fig4.JPG](media/oppg11fig4.JPG)
    * Dra inn en Button fra App Controls inn i repeating section over Acitivities. 
      * Sett background color white, foreground color navy og border color navy, show boarder=true.
      * Name: Complete Activity
    * Sett command og event på knappen for å kjøre tasken. Husk Two-Way Binding til Activity.Single Selected.
    * Deploy og sjekk at knappen fungerer. 
    * Flytt litt rundt på og juster til du er fornøyd med utlistingen
  ![oppg11fig5.JPG](media/oppg11fig5.JPG)
  
## Open Data, Local Objects and Map
In this exercise, we will fetch open data from multiple public API’s, store it in local objects and visualize the aggregate data in a map. Note that we do not store any of the data in the database, everything is stored in memory as the client uses the app.
  1.  Create a new App-form and set the following layout:
      - Mark the view and name it “Main - map”
      - Check all Platforms for the views
      - Save the form and name it “OSLO”, close the form.
  2.  Select Apps in the navigation pane in the “User Interface” section
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
            - Add Layer, Type = Map and Server Type = OSM
            - Add Layer
               - Type = Point
               - DS = Bike Stations
               - Location fields
                  - Northing = longitude
                  - Easting = latitude
                  - Coordinate system = WGS84
               - Select an appropriate symbol and set the size to 32px and a color of your choice.
            * Add Layer
               - Type = Point 
               - DS = Bus Stops
               - Location fields
                  - Northing = longitude
                  - Easting = latitude
                  - Coordinate system = UTM32N
               - Select an appropriate symbol and set the size to 32px and a color of your choice.
  6.	Create the following local tasks: Get stops, Get bikes. Give the tasks appropriate security (Properties > security).
  7.	The first source of data is Ruter (which plans, coordinates, orders and markets public transport in Oslo and Akershus). Link to API documentation: https://ruter.no/labs/.
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
10.	Add popup context to the point layers to show the information (for instance id and name) on click. Customize it (try to be creative, maybe we don’t need label?)
   ![oppg11fig11.JPG](media/oppg11fig11.JPG)
   
   Now we see bus stops (for line 30) and all bike stations. The next step is to show number of bikes available and when the next departure of the bus is.
   
11.	We need a new Local Object to store the data temporarily as it is collected in 2 rounds, first stations and then availability. Create the local object inside the local task: name: “availability”, unbounded and fields id, bikes and locks all String. See screenshots.
   ![oppg11fig12.JPG](media/oppg11fig12.JPG)
   ![oppg11fig13.JPG](media/oppg11fig13.JPG)
 
12.	Add a REST service to call https://oslobysykkel.no/api/v1/stations/availability with credentials provided above. Map it to the availability DS. Then the data must be copied from availability DS to the bikes DS via a modify object-effect. See screenshot. Note: The filter is important here to ensure correct modifications!
   ![oppg11fig14.JPG](media/oppg11fig14.JPG)
   ![oppg11fig15.JPG](media/oppg11fig15.JPG)
13.	Add the local task as On Load Form event as the others. Add bikes and locks to popup content. Deploy to all and verify that you can see name and availability of bikes on the map.
   ![oppg11fig16.JPG](media/oppg11fig16.JPG)
   
14. Optional points for talented business engineers:
      * Get departure data for the bus and display it in the form (hint: use http://reisapi.ruter.no/StopVisit/GetDepartures/3010146). The solution modell contains a partial implementation of this, look at it if you are stuck.
      * Get weather forcasts from YR and dispay bus stops if rain and bike stations otherwise (https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fwww.yr.no%2Fsted%2Fnorge%2FOslo%2Foslo%2Foslo%2Fvarsel.rss).
      
      
<table>
   <tr><td><a href="oppgave-10.md"><- Previous exercise</a></td><td align="right"><a href="oppgave-12.md">Next exercise -></a></td></tr>
</table>
