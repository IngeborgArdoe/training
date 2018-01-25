##Oppgave 3

1. Lag en ny Form: «Contact»
   1. I Studio, gå til User Interface -> Forms. Høyreklikk -> New -> Desktop Form. Lagre denne med en gang med navn «Contact».
   2. Data Sources (øverst til venstre): Velg denne. Her legger man inn objektet (eller objektene) man skal vise eller benytte i Formen. Legg til «Contact» som en Data Source. *Veiledning: Se screenshot under. Merk at:*
      1. *Data Source «Contact» må endres til å ikke være Private (huke vekk). Grunnen er at man skal åpne skjermbildet (formen) Contact fra andre steder, og da skal Contact filtreres inn til Formen (input til Formen, slik at Formen vet hvilken kontaktperson den skal vise data for).*
      2.  *Data Source «Contact» må settes til «Max Occurences» = “One”. Dette for at det skal være mulig å vise properties for Contact i et felt – “Unbounded” brukes om data sources som skal listes ut i GRIDs*.
      3.  *Huk også av for «Is Master» og «Enable Read Audit Trail» - dette for at endringshistorikk skal være tilgjengelig når du åpner skjermbildet for en kontaktperson, samt at Formen er «master» Formen for visning av 1 Kontaktperson (Formen kan med andre ord brukes som Default form for Contact).*
    ![oppg3fig1.JPG](media/oppg3fig1.JPG)
   3. Views: Gå til View (Default). Endre Name til «Contact».
   4. Legg Container «Tab Sheets» ytterst. Trykk inne i den første arkfanen (du markerer med andre ord Group-en som ligger her). Endre Label til “General”. 
  Legg til en til fane: Gå et nivå ut (tips: trykk Esc-knappen), og dobbeltklikk på "Group" i komponentvelgeren. Gi den nye fanen navn «Activities» (her kommer innhold senere). Dette blir en ny arkfane på Tab Sheet’en. (Nærmere beskrivelse i oppgave 2.2 om dette ikke ga mening.)
  Legg også på en arkfane med navn «Mail» (innhold kommer senere).
   5. I Arkfane «General»: Her skal feltene for Contact legges til. 
  *Veiledning: I en oppgave senere skal man også liste ut «Contact log» nederst i dette skjermbildet, så vi anbefaler følgende oppdeling av «General»:*
  ![oppg3fig2.JPG](media/oppg3fig2.JPG)

      Velg så GroupBox1, og endre «Container Type» til «Group» - dette for å fjerne rammen rundt. Gjør tilsvarende for Groupbox3 og Groupbox4 (eller hva nå enn disse er navngitt default i din løsning).
  Felter kan legges til ved «drag and drop» fra høyresiden etter at man har endret som følger:
  ![oppg3fig3.JPG](media/oppg3fig3.JPG)
  
      Etter at endringen over er gjort, kan man dra inn Properties fra Contact inn i Groupene i «General»-arkfanen. Det vil da default foreslås riktig layoutcontrol (feks, TextEdit foreslås for «First Name»). Men hvis du drar inn Company vil ComboboxEdit foreslås – en dropdown – dette kan være uheldig om det er mange objekter i listen. Hvis du holder inne Shift når du drar over Company vil SeachBoxEdit foreslås isteden, som er mer gunstig for sluttbrukeren.
   6. Formen for Contact er nå ferdig i sin første versjon. Du kan eventuelt gå til ytterste nivå i View’et og endre Width og Height til 800 og 600. For å se hvordan dette ser ut, endre Alignment til «Fixed». Dette gjør at sluttbruker ikke kan endre størrelsen, så endre tilbake igjen til «Stretch» før du lagrer.
  Det er litt luft nederst i Form’en, hvilket er OK (her kommer innhold senere). 
  Vi skal nå legge til utlisting av Contacts inne på et Company (ved hjelp av en GRID), og legge handlinger for å lage ny Contact, samt åpne eksisterende Contact..

2. Legg til utlisting av Contacts i en egen arkfane i Form-en «Company»
   1. I Studio, gå til User Interface -> Forms. Åpne «Company».
   2. Legg til en ny arkfane på Tab Sheeten nederst i Formen. 
  *Veiledning: Se screenshot under*
  ![oppg3fig4.JPG](media/oppg3fig4.JPG)
 
   *Merk: I Formen ser du at navnet på arkfanene samt header er «Company label» etc. Ikke bry deg med det per nå – dette vil si at Labelen på controllen er bundet til feltet i et objekt som viser et dynamisk navn på Labelen (på arkfanene vises navn + antall i listen i parantes). Formen «Company» inneholder også forsinket opplesning av data som gjør at feks «Activity History» ikke leses opp før man trykker på arkfanen. Dette er den del av mer avansert modellering som du ikke trenger å tenke på nå.*
   3. Gi navn (Name + Label) på den nye arkfanen: «Contacts». Høyreklikk på arkfanen, og velg «Sort tabsheets». Flytt denne frem et hakk.
   4. Under «Data Sources»: Legg til Contacts ("Private" og “Unbounded” - dette er forhåndsvalgt). På properties på denne datasourcen, gå til Data Filter. Legg til filter på at Contact.Company = Company (mao., les opp Contact tilhørende Company’et i Formen).
  *Veiledning: Se screenshot under:*
  ![oppg3fig5.JPG](media/oppg3fig5.JPG)
  Data filteret kjøres når Formen «Company» åpnes, og kontaktpersoner leses opp.
   5. Gå tilbake til arkfanen «Contacts» og legg til en Grid. Set Data Binding til denne mot Data Source «Contact». Legg til hvilke kolonner som skal vises under «Columns». Legg deretter på sortering (First Name, Last Name) under «Sorting». Sett også «Selection Mode» til «Multiple» (det blir med andre ord lov å markere flere kontakter i listen).
  *Veiledning: Se screenshot under*
  ![oppg3fig6.JPG](media/oppg3fig6.JPG)
  Du har nå lagt til utlisting av Contacts på Company. Nå skal det legges til eventer for å åpne den nylig opprettede Formen «Contact» ved dobbeltklikke på en rad i GRID’en, samt en knapp med event for å lage en ny Contact.

#Handlinger i Genus App Platform: Commands og Events:

I Genus App Platform er Commands brukt til å spesifisere effekter som skal skje i en Form. En Command kan bli startet/trigget av en Event eller fra Ribbon. En Command kan være av mange ulike typer – blant annet «Open a Form», «Apply Changes», «Delete Object» eller «Run a Task». Flere Commands kan også settes sammen (Combined) og en Command kan kalle en annen Command. 

Eventer kan trigge Commands ved at en for eksempel legger en Event av typen «On Click» på en Button og peker den til en Command som er handlingen som skal skje når knappen blir trykket på.
For å gjøre oppgavene under kan det virke mer naturlig å legge Command på samme controller som eventen skal ligge på. Dette ville også fungert helt utmerket, men vi velger ofte å legge command på et annet nivå av grunner som vi skal se nærmere på i Oppgave 5: Ribbon. Ribbon er også grunnen til at vi velger et symbol til Commands og endrer navnet til eksempelvis «New Contact» heller enn å bruke Name:Open Contact.
  
3. Legg til handlinger i Form-en «Company»
   1. Velg Griden for Contacts. Under Properties, klikker du på «Commands». Legg til en ny Command av typen «Open a Form»:
      1. Name: Open
      2. Tip: Contact (Dette er et tips som kun vises til deg som modellerer.)
      3. Type: Open a Form
      4. Effect: Contact (Formen som skal åpnes)
      5. View: Default (hvis det finnes flere Views i formen kan man velge her)
      6. Data Binding: Default (One Way. Hvis Two-way velges, vil Formen åpnes modalt, og endringene vil tas med tilbake til Company Formen, hvor de må lagres med lagre-knappen)
      7. Filter Data: Velg «one way binding to objects in the data source». Trykk Modify. I dialogen velger du datasourcen det skal filtreres mot (Contact), samt «Single Selected Object». Dette gjør at aktiv (valgt) rad i Contacts Griden filtreres inn i formen «Contact». Huk også av for «Enable Browse Object» (hvilket gjør at du kan bruke pilene opp / ned for å bla deg gjennom en liste av kontaktpersoner).
   2. Legg til Event på grid-en:
      1. Type: On Context Meny Item Click
      2. Menu Item: Open in a New Window (når skal eventet inntreffe – ved dobbeltklikke (som default trigger verb «Open in a New Window» i Genus).
      3. Command: Open Contact
         Trykk OK
   3. Legg til Command for å opprette ny Contact. Denne skal ligge på arkfanen til Contacts. Dette kan eksempelvis gjøres ved å markere grid-en for Contacts og trykke Esc. Vi legger Commanden her fordi vi ønsker at denne Commanden skal være tilgjengelig både fra grid-en og senere også fra Ribbon.
      1. Name: New Contact
      2. Type: Open a Form
      3. Effect: Contact
      4. View: Default
      5. Data Binding: Default
      6. Create Data: Klikk … og velg “Add”. Under «Default Values» må du huske å sette Contact.Company = Company (mao, Contact’en som skal opprettes får satt Company fra Form’en du er i når knappen «New» trykkes)
      7. Velg et symbol: Dette vil også vise seg å være nyttig senere. Et godt symbol kan være det som dukker opp dersom du gjør søk på «1081». Merk at du kan velge både hovedsymbol og «Overlay». Forsøk å også sett på et overlay, men før du trykker OK, høyreklikk på overlayvalget du gjorde og trykk «Clear».
      8. Trykk OK og lagre Commanden.
   4. Legg til Event på grid-en for å opprette ny kontakt.
      1. Type: On Context Menu Item Click
      2. Menu Item: New
      3. Command: New Contact (Command-en du akkurat lagde)
   5. Vi ønsker også å kunne slette kontakter. Legg til Command for å slette kontakt på arkfanen.
     *Veiledning: Se på Commanden «Delete» som ligger under ActivitiesTab-arkfanen for veiledning: For vårt tilfelle skal Delete-commanden ha Data Binding mot Data Source «Contact». Tips: Bruk symbol #1195. Enabling: Conditional hvis Contact.Single Selected Object has value. (Bilde under)*
  ![oppg3fig7.JPG](media/oppg3fig7.JPG)

   6. Legg til Event på grid-en med Type: On Context Meny Item Click, Menu Item: Delete som peker til Command-en. 
   7. Vi ønsker nå å teste det vi har laget så langt: I Genus Studio velg File (øverst) - >Deploy to this computer. Endringene deployes nå til din egen PC for test. Gå til klienten, åpne et Company og forsøk å legge til en ny Contact, endre en Contact eller slette en Contact. Sjekk at Default verdier ved opprettelse av Contact er som forventet.
  Kommentar: Hvis dette hadde vært et test- eller produksjonsmiljø kunne du valgt «Deploy to all» med et valgt tidspunkt. På dette tidspunktet ville endringene du har gjort så lagt blitt tilgjengelig for alle brukere av løsningen.
  
      Vi har nå laget Contact og verifisert at det fungerer. Vi ønsker nå å kunne liste ut Activities og Mail på Contact. For at dette skal fungerer trenger disse to objektklassene en referanse til Contact.
4. Legg til et nytt felt på Object Class «Activity»: Contact
  *Veiledning: Vi legger nå feltet til i databasen først. Du kan kjøre SQL «alter table Activity add ContactID uniqueidentifier» (legger til et felt ContactID på Activity tabellen i databasen. Datatypen er lik primærnøkkelen til Contact).*
  
   Deretter høyreklikker vi på Activity og velger «Add Object Class Properties». I veiviserens steg «Property Definition» må du igjen passe på å sette Data Interpretation til «Contact»
5. Legg til et nytt felt på Object Class «Mail»: Contact
   *Veiledning: Som oppgave 3.3 over (bytt «Activity» med «Mail» i SQL’en)*
6. Vi må også gjøre feltet Activity.Contact tilgjengelig i brukergrensesnittet. 
   1. Åpne Form «Activity» og legg til «Contact» Fra Activity-datakilden som et felt (ComboBox) under Company i grensesnittet.
   2. Vi ønsker også drop-down’en skal begrenses til Contacts som tilhører aktivitetens Company, og kun Aktive kontakter. Sett «Data Restriction» på feltet.
      *Veiledning: Se screenshot under:*
      ![oppg3fig8.JPG](media/oppg3fig8.JPG)
7. Vi skal nå liste ut Activities på en Contact, samt lage mulighet for å registrere Activities på en kontaktperson.
   1. Lag en utlisting av Activities i arkfane «Activities» i Contact Formen.	
      *Veiledning: Du må ha Activities som en Data Source i Formen først. Sett på data filter på denne (les opp Activities hvor Activity.Contact = Contact og Activity.State ulik Canceled). Legg deretter en Grid i arkfanene som du binder mot Data Source «Activity». Sett opp Columns. Pass også på å få Sorting (feks etter Due Date descending). Du kan også feks sette på Grouping (på State).*
   2. Legg til Command på arkfane Activity for å åpne Activity:
      1. Command: Open a Form
      2. Name: Open, Tip: Activity
      3. Husk filtrering!
      4. Legg til event på Griden som gjør commanden på Context Menu Item Click: Open in New Window.
   3. Legg også til command + event for «New» og «Delete» på Griden for Activities. Legg på eventer på disse (tilsvarende som i oppgave 3.3.3, ..4 og ..5). Pass på å få satt Default verdier på «New» slik at Activity kobles både til Contact og til Company. For new kan symbol #1198 passe og for delete #1195. For oppsett for «New» går det an å hente inspirasjon fra oppgave 3.3.
   4. Deploy løsningen til deg selv og test at du får opprettet Activities på en kontaktperson.
8. Vi skal også liste ut Mail på en Contact. Muligheten for å legge til ny Mail i en liste er i Company Formen løst med en handling som paster inn ny Mail fra Clipboard (mao., drag & drop). Vi skal lage dette i en senere oppgave, for nå skal vi kun legge til utlisting og åpning av epost på kontaktperson
   1. Lag en utlisting av Mail i arkfane «Mail» i Contact Form’en )som lister ut Mail hvor Mail.Contact = Contact)
   2. Legg på event i Grid’en med Event Type «On Activate» og Effect Type «Invoke a File».
     *Kommentar: Denne gjør at Mailen, ved dobbelklikk på en rad, åpnes i outlook. Dette er bygget inn i plattformen  – hvis objektklassen inneholder File Data, File Size, File Type og File Name så åpnes objektet i «default» program ved «Invoke a File» effekten. Se eventuelt hvordan dette er løst i Grid’en «Mail» i Company Form’en*

9. VALGFRI OPPGAVE: «Logg» på kontaktperson
   Denne er ikke strengt nødvendig for resten av oppgavesettet. Men den inneholder et nytt konsept «Part of composition», så vi anbefaler at oppgaven ihvertfall leses gjennom.

   Vi ønsker å kunne skrive logginnslag på kontaktpersoner (tilsvarende «Company Log» som finnes under Company). 
   1. Opprett en ny Object Class «Contact Log». Når du går gjennom wizarden for å legge til ny Object Class, pass på å sette Data Interpretation på Created By (User) og Contact. I siste steg i wizarden velger du Part Of Composition “Contact”
      *Veiledning: Du kan benytte SQL: 
      Create table ContactLog (ContactLogID uniqueidentifier PRIMARY KEY, "Subject" varchar(1000), CreatedDate datetime, CreatedByUserID uniqueidentifier, ContactID uniqueidentifier)*
      Når du setter Part of Composition betyr dette at dataene i Contact Log (som henger under en Contact) alltid leses opp sammen med Contact og samtidig arver sikkerhet og “audit trail» fra Contact. Sett opp part of composition ihht screenshot under:
      ![oppg3fig9.JPG](media/oppg3fig9.JPG)
   2. Sett Default verdier på Created by og Created Date, samt sett Subject påkrevd.
   3. Lag en Form «Contact Log»
      1. Denne har kun 1 Data Source: Contact Log (husk: Huk vekk «Private» og sett Occurence = Allow one object)
      2. View (properties): Her endrer du Style til «Dialog Box» og Buttons til «OK and Cancel». Endre også Alignment til «Fixed» og Width = 800 og Height = 600 (feks). 
     *Kommentar: Grunnen er at denne Formen ikke skal ha noen lagre knapp. Den skal åpnes modalt fra utlistingen av Log på Contact, og ved trykk på «OK» vil denne Form’en lukkes og endrinene lagres i Contact Form’en.*
      3. View: Denne skal kun vise feltet «Subject». Dra inn dette. Endre følgende egenskaper ved Subject:
         1.	Huk av Multiline og Word Wrap
         2.	Sett Vertical Alignment til «Stretch»
         3. Sett Label Position til «Top».
   4. Åpne Form «Contact». 
      1. Legg til en ny Group Box nederst. Gi denne Label «Log:». Huk av for «Is Collapsible» og “Transparent Title Area”. Under “Border Thickness” setter du 0.
      2. Legg en Grid inni denne. Bind Griden mot Data Source = Contact, Field = Contact Log. Legg på Columns og sett Sorting (Created date, descending). **NB: Det kan være du må starte Genus Studio på nytt før du gjør denne!**
     *Kommentar: I og med at Contact Log er part of composition og vi ikke skal filtrere vekk noe trenger denne ikke være en egen Data Source. Griden er nå bundet mot gruppen av logginnslag som henger under kontaktpersonen og kan vise kolonner derfra.*
      3. Legg på Command i GeneralTab for å åpne en Contact Log i Formen «Contact Log». Denne skal kun være enablet hvis Contact Log.Single Selected har verdi. Legg til event for å utføre command i grid-en.
      *Veiledning: I og med at Formen «Contact Log» er en dialogboks har den ikke mulighet til å lagre endringene selv. Velg derfor ved oppsett av event inn Two Way binding som vist nedenfor:
      ![oppg3fig10.JPG](media/oppg3fig10.JPG)
      Data Binding: 
      ![oppg3fig11.JPG](media/oppg3fig11.JPG)
      4. Legg også till command og event for New og Delete. Her legges også Command på GeneralTab og Event på selve griden.
         1. *Veiledning New: Åpningen av Contact Log i «Create» modus er også two-way bundet. Det betyr at et nytt objekt opprettes i Contact Log formen, men lagringen av dette tas med tilbake til Contact Form’en (hvor man kan trykke lagre knappen). Se screenshot under:*
      ![oppg3fig12.JPG](media/oppg3fig12.JPG)
         2. *Veiledning Delete: Se screenshot under: (hhv Command og Event)*
      ![oppg3fig13.JPG](media/oppg3fig13.JPG)
 
   5. Deploy og test opprettelse, endring og sletting av logginnslag på kontaktperson i klienten.
