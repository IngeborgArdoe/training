# Oppgave 11 - Genus Apps

*SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon med intro til modellering av Genus Apps-forms.*

## Enkelt web-grensesnitt
I denne oppgaven skal du lage et enkelt web-grensesnitt for å vise aktuelle aktiviteter for selskaper innlogget bruker er ansvarlig for – med mulighet for å sette status til Completed.
1. Klargjør for Genus Apps:
  1. I Studio: Gi Super Users privilege: Sign in as an app user
  2. Deploy to all (du må deploye to all for at det du gjør skal vises i nettleser. Det tar omtrent ti sekunder fra du deployer til endringene blir gjenspeilet på web).
  3. Verifiser at du når følgende side: 
    * For dere på edu1: http://edu1.genus.net/edu1Y/edu1Y, hvor Y erstattes med bokstav fra brukernavn (feks http://edu1.genus.net/edu1a/edu1a for usr1a).
    *	For dere på edu2: http://edu2.genus.net/edu2Y/edu2Y, hvor Y erstattes med bokstav fra brukernavn (feks http://edu2.genus.net/edu2a/edu2a for usr2a).
    
    Per nå vil det kun stå "CRM Edu1" med mulighet for å logge ut og lukke - det er ikke så rart siden vi ikke har laget noen app ennå.
2.	Opprett en ny Form ment til App og sett basic layout på denne:
  1. Opprett en ny Form: "My tasks | APP"
      * Først gå til View. 
      * Name: "My Activities - Main".
      * Huk av for Platforms: Tablet, Web on Phone, Web on Tablet, Web on Desktop.
      *  Padding: 24
3.	Legg til en overskrift
  2. Dra inn en Text-controller fra App Controls:
      ![oppg11fig1.JPG](media/oppg11fig1.JPG)
      * Content: My Activities
      * Foreground Color: Navy
      * Font Size 24
4. Legg til en repeating section som repeterer over aktiviteter (Not started or In Progress) som tilhører Companies som innlogget bruker er ansvarlig for. Vis selskapsnavn, Activity’s subject og status vises ut til bruker.
  1. Legg til Activity-datakilde
  ![oppg11fig2.JPG](media/oppg11fig2.JPG)
  2. Lag en Repeating Section som repeterer over Activity
    * Dra inn en GroupBox i Viewet. Denne GroupBox-en må dras inn fra App Controls
    * Sett Vertical Alignment: Top
    * Bind GroupBoxen til Activity-datakilden.
    * Huk av for “Repeat Content under properties på GroupBox-en.
    * Sett på sortering på GroupBox-en med sorteringsnøkkel Due Time (Descending).
  3. Legg inn tekstfelter for selskapsnavn, aktivitetens Subject, frist og aktivitetens State: 
    * Dra eller dobbeltklikk inn fire tekstfelt i GroupBox-en.
    * Bind den første til Datasource: Activity Field: Company.Name og gjør tilsvarende for Activity.Subject, Due(Fx) og Activity.State.Display Name
    *Merk: Selv om Activity er en unbounded datasource og feltet bare skal vise ett enkelt tekstfelt trenger vi ikke spesifisere Active Object i DataSource. Dette er fordi vi allerede er i kontekst av et aktivt Activity-objekt når vi er i repeating section over Activity.
5. Opprett en App som bindes til Formen du akkurat lagde
  1. Gå til Apps under User Interface i Genus Studio.
  2. Opprett en ny som du kaller My ACctivities. Form My Activities
  3. Huk av for default view for Web og Tablet
  4. Sett AppBar Foreground til Navy
  5. Etter du har lagret, sett security på Appen. (Properties=> Super 
  Users skal kunne Find and List og Read and Execute).
6. Deploy to all og sjekk i browseren at du får forventede resultater (noe a la dette)
![oppg11fig3.JPG](media/oppg11fig3.JPG)
 
7. Legg til knapp i repeating section for å endre state på aktiviteten til Complete 
  1. Legg til en ny task med input Activity (Name: T.Activity, Max Occurences: One). Husk å sett private=false.
  2. Under General sett “Enable on Application Server”=true
  3. Under Actions: Legg til et Scope med en Modify Object som setter State til Completed.
  4. Lagre og sett security på tasken:
  ![oppg11fig4.JPG](media/oppg11fig4.JPG)
  5. Dra inn en Button fra App Controls inn i repeating section over Acitivities. 
    * Sett background color white, foreground color navy og border color navy, show boarder=true.
    * Name: Complete Activity
  6. Sett command og event på knappen for å kjøre tasken. Husk Two-Way Binding til Activity.Single Selected.
  7. Deploy og sjekk at knappen fungerer. 
  8. Flytt litt rundt på og juster til du er fornøyd med utlistingen
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

