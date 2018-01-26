#Oppgave 6: Logikk og effekter
**SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon Tasks og Effekter (Action Orchestration) i Genus App Platform.**

##Modellering av logikk – prinsipiell oversikt
Vi er nå klare for å legge til og utvide funksjonaliteten i løsningen. Med funksjonalitet i denne konteksten menes «Tasks» som er brukerinitierte handlinger som kjøres når brukeren velger handlingen i «Actions» pane eller trykker på en knapp (dersom handlingen er publisert til en knapp i en Form).

Tasks, eller «Handlinger» på norsk, tilsvarer på mange måter en metode eller funksjon i programmeringsverdenen; En metode kan ha input, og den kalles fra «et eller annet sted» for å eksekvere. Når den kalles eksekveres den sekvensielt, og den kan ha opprettelse av variabler og lister, ha «if»’er med betingelser og den kan ha løkker (for- eller while loops).

Tasks i Genus App Platform modelleres med samme tankesett som når man programmerer en metode; 
-	Man har et sett av Data Sourcer;  disse kan enten kan være input til Tasken (hvis Data Sourcen ikke er private) eller de kan brukes til lesing av data fra databasen, eller de kan brukes til å opprette data. 
-	Man setter sammen en sekvens av Effects (feks «Read Objects», «Create Object» eller «Modify Objects») som kan ligge inni Decision Blocks («IF»-blokker i programmeringsverdenen) eller Enumerator Blocks («For»-løkker i programmeringsverdenen).
-	En Task kan også kalle en annen Task, og data (objekter) kan overføres fram og tilbake.
-	En Task kan opererer kun «in memory» dersom man legger en Scope Block rundt det hele som ikke har Commit (med andre ord, endringer som gjøres persisteres da ikke til databasen), eller alle endringer som gjøres i effektene kan persisteres til databasen ved å ha dem inni en Scope Block som har Commit.
-	En Task kan også ha exception håndtering (Catch Exception, eller Throw Exception) hvis noe går galt
-	En Task kan også ha brukerdialog (vise dialogbokser til bruker med valg, som styrer hvor man skal gå videre i sekvensen av effekter).
I Genus Studio ser du Tasks i seksjonen «Logic». Her ligger Rules, Tasks, Agents og Web Services. Disse settes opp på neste samme måte, men er i sin natur ulike: 
-	Tasks trigges av en brukerinitiert handling, som å trykke på en knapp etc. Unntaket her er tasks (som nevn tidligere kan tasks kalle andre tasks) som gjør noen generisk (feks lagrer et Mail objekt basert på fil-input og objekt-input) og som kalles fra andre tasks, rules, agenter eller web services
-	Rules trigges ved business eventer i løsningen, feks «etter endring av Company.Responsible, kjør denne regelen». Oppsettet av effekter tilsvarende som i tasks.
-	Agents trigges av et klokkeslett – dette er skjemalagte handlinger (feks, hver morgen send en epost til alle brukere med aktivitetspåminnelser)
-	Web Services kan settes opp og trigges av at det kommer inn et web service-kall fra feks et ekstern system. Web Services settes opp på logikknivå likt som tasks, men i tillegg har Web Services definerte Schemas som beskriver strukturen på input og output XMLen (mer om dette i senere sesjon)


Vi begynner med noen enkle tasks.
###Change Responsible for Contact
Denne tasken skal ta som input en eller flere Contacts, og endre Responsible på disse.
1. Data Sources: Her legger du til Object Class «Contact».
   *Veiledning: Høyreklikk i panelet øverst til venstre -> Add -> Object. Velg Contact. I panelet nederst (General) huker du bort «Private». Endre også Name til «Contacts input» for å synliggjøre for «resten av løsningen» (når man skal koble inn denne tasken mot en tabell etc) hva som er input til tasken og kardinaliteten på denne (dette er god «Best Practice» men ikke noe krav).* 
2. Actions: Det første vi ønsker å gjøre er å la brukere angi en input; Brukeren skal angi én User, valgbart fra en dropdown, som skal være ny ansvarlig for kontaktpersonene i data source «Contacts input». Deretter trenger vi en effekt som endrer ansvarlig for kontaktpersonen.
   1. For å kunne la bruker velge en User og bruke dette valget videre trenger vi en «variabel» å lagre dette i. 
      1. Gå til «Data Sources» igjen og legg til et «Local Object» (Add -> Local Object). Gi denne Name = «User Input»
      2. I panelet til høyre legger til til et Field. Sett Display Name til å være «New Responsible» og Data Type til «User». Huk også vekk «Allow blank value» (feltet er påkrevet).
   2. Gå tilbake til «Actions». 
      1. Legg til Effect «Open a Form». 
      2. Dobbeltklikk på effekten etter at den er lagt til, og sett Type = «Local Object Window» og Data Source = «User Input». Huk av for «Create» (vi skal opprette et lokalt objekt i minnet). Trykk på knappen «Modify...» og angi veiledningstekst som skal vises til sluttbruker i vinduet som skal åpnes ved kjøring, feks som under:
      ![oppg6fig1.JPG](media/oppg6fig1.JPG)
 
   Du skal nå legge til en effekt som endrer Contact.Responsible på alle objektene i data sourcen «Contact input» og som lagrere dette til databasen.

   3. Legg til Block «Scope».
      *Merk: Denne har default huket av for «Commit» som betyr at alle endringer (Create eller Modify Objects) som gjøres av effekter inni dette Scopet vil lagres til databasen.*
   4. Legg til Effect «Modify Objects» inni dette Scopet, og sett denne til å endre Data Source «Contacts input» sitt felt «Responsible».
  *Veiledning: Sett opp som i screenshot under. Dette vil ved kjøring generere en SQL som setter Responsible på alle Contacts som finnes i data sourcen «Contacts input».*
     ![oppg6fig2.JPG](media/oppg6fig2.JPG)
 
En ting vi ikke har pratet så mye om ennå (kommer i senere sesjon) er sikkerhet. Det gis tilgang til sikkerhetsgrupper per task. Alle brukere av Genus CRM er medlem av sikkehetsgruppe «Users» og skal ha tilgang til denne tasken. 

3. Gå til File -> Properties (øverst til venstre i tasken) og legg til Security Group «Users» i arkfane Security. Huk av for «Find and List» og «Read and Execute».

*Tasken er ferdig, men er ikke tilgjengelig for sluttbrukere ennå – den må kobles inn i et User Interface som en event.*

4. Gå til table «Contacts». Under «Events» legger du til en event for å kjøre tasken
   1. Effect Type = «Run a Task (Global Scope)»
   2. Effect = “Change Responsible for Contact”
   3. Enabling: Huk av for “On selected objects” (tasken skal være enabled ved valg av flere rader)
   4. Filter Data: sett «Two way binding to objects in the data source: Contact» med Objects: Selected.

      *Merk: Setting av data filter på denne måten er en hurtig måte å si at «tasken sin datasouce Contacts input skal populeres med de kontaktpersonene jeg har valgt i tabellen min». Valgte kontaktpersoner vil nå i klienten, ved å trykke på Action «Change Responsible for Contact» i Actions pane, kopieres inn i tasken «Change Responsible for Contact» og tasken vil eksekvere effektene sine og avslutte.*
5. Legg til Change Responsible for Contact i Ribbon
   1. Navngi eventen i tabellen «Change Responsible»
   2. Gi den symbol #692 med overlay #13
   3. Åpne Customize Ribbon. Under Main Tabs legg til en ny Tab Section. Kall denne Responsible
   4. Marker Responsible-Tab Section-en og dobbeltklikk på Change Responsible-eventen (ligger under «Table Commands».

6. VALGFRITT (men anbefalt!): Gå til Form «Company» og legg til en command for å kjøre tasken. Legg commanden på Contacts-grid-en med riktig enabling. Husk symbol. Legg på event for å kjøre tasken «Change Responsible for Contacts» i grid-en. Gjør kommandoen tilgjengelig også fra Ribbon (Context Tab Group Contact i en ny Section «Responsible Contact».

*Merk: Under Filter Data for commanden setter du hva som skal filtreres inn til Tasken sin datasource «Contacts input». Denne settes Two-Way mot Data Source “Contact” sin Selected Objects.*
  
*At man setter noe “Two-Way” her betyr at endringene tas med tilbake, og hvis endringer i tasken ikke er persistert (committet/lagret) vil man få opp “Lagre” knappen enabled i Contact skjermbildet etter trykk på knappen.*

 
Vi skal nå legge til muligheten for å opprette Mail på kontaktpersoner. Til dette formålet har vi fra før en task «Paste new Mail from file» som tar som input «Mail Message (input)» og «Company». Tasken skal utvides til å også ta «Contact» som mulig input, samt logikk for å lagre en Mail under Contact.

### Paste new Mail from File - lagre e-post under kontakt
«Paste new Mail from File» skal utvides til å kunne lagre epost under kontaktperson
1. Åpne task «Paste new Mail from file». Legg til Contact som Data Source og navngi «Contact (input)»
   *Merk: I og med at det kun pastes ny Mail på én Contact av gangen skal Occurrences på denne Data Sourcen settes til “Allow one object”.*
2. Utvid logikk under Actions
   1. Utvid Condition i den første “Decision” blocken til å også slå til hvis kun Contact (input) har verdi.
   *Veiledning: Man kan lage Conditions med AND og OR. For å få satt opp «Mail Message input skal ha verdi OG (Company input eller Contact input skal ha verdi)» blir utrykket slik (Tips: «Add Group» knappen):*
   ![oppg6fig3.JPG](media/oppg6fig3.JPG)
   2. Utvid logikken i Create Objects effekten til å sette feltet «Company» fra Company (input) hvis den har verdi, eller fra Contact (input).Company hvis Contact (input) har verdi. Sett også feltet Contact fra Contact (input).
   ![oppg6fig4.JPG](media/oppg6fig4.JPG)
3. Legg til command i Mail-tab i Contact Form som trigger på Menu «Paste» og som kjører task «Paste new Mail from File». Legg til event i grid. Legg til event i Ribbon (ny seksjon under Mail Management: Cliboard. Husk passende Name, Tip og Symbol (søk opp paste).

*Veiledning:  Denne settes opp med Effect Type = Run a Task (global scope) og Menu = Paste Special. Under Filter Data setter du tasken sin Mail Message (input) lik «Get objects from the clipboard» og Contact (input) lik Contact.*
4. Legg samtidig på command i Mail-Tab som kaller eksisterende task “Copy Mail to Clipboard as Mail Message». Tilgjengeliggjør via event på grid og i Ribbon.

*Veiledning: Velg her Menu «Copy» og sett Data Filter til tasken sin Mail (input) lik selected objects fra Contact formen sin data source Mail. Ribbon: Søk opp «copy» for å finne passende symbol.*
