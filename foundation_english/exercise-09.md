#Oppgave 9: Request

Vi ønsker nå å lage et nytt forretningsobjekt «Request» som lar oss registrere forespørsler fra kunder. Request skal brukes videre i oppgavesettet til blant annet å generere ordrebekreftelse og i rapporter, så her er det viktigst at objektet modelleres opp. Oppgavene vil bestå av noen påkrevde og noen valgfrie oppgaver – de valgfrie tar du dersom tid og lyst.

Før vi modellerer opp Request lager vi objektene for kodeverket etc til Request, slik at vi kan sette Data Interpretation korrekt umiddelbart ved modellering av objektklasse Request.
1. Opprett et nytt Code Domain «Request State». Legg til verdier «Open» (value 10), «Closed» (value 20) og «Canceled» (value 30).

   *Veiledning: I Genus Studio, høyreklikk på «Object Classes» -> Velg «Code Domain».*
2. Opprett et nytt Code Domain «Request Type». Legg til verdier «Order» (value 10) og «Service» (value 20).

   *Kommentar: Requestene kan dermed klassifiseres som enten bestillinger (Order) eller forespørsler om hjelp / annet (Service).*

Vi ønsker også å ha et «ordrenummer» som settes ved opprettelse av Request, og som er en sekvensiell teller. Til dette kan man opprette et «Identifier Domain» (fra Studio -> høyreklikke «Object Classes» -> New -> velg «Identifier Domain». Dette er en objektklasse i Genus App Platform som krever en tabell i databasen som holder på siste ordrenummer. Tabellen har et navn (feks «OrderNoCounter») og et felt (feks «Order No») av typen integer. Et Identifier Domain kan benyttes til kalkulering av felter, og Genus vil da hente siste nummer i sekvensen fra databasen, og samtidig oppdatere dette med 1.

3. Opprett et nytt Identifier Domain med navn «Order No Counter» med et felt «Order No» (int).
  
   *Veiledning: Opprett tabellen i databasen først, og samtidig insert innslaget for «første ordrenummer» i tabellen ved å kjøre følgende script*:

   create table OrderNoCounter (OrderNo int)

   go

   insert into OrderNoCounter values (10000)
  
  I wizarden for opprettelse av nytt Identifier Domain, velger du «Sequential Counter» i steg 2:
  ![oppg9fig1.JPG](media/oppg9fig1.JPG)
 
  Og i steg 3 velger du kolonnen som skal inneholder telleren:
  ![oppg9fig2.JPG](media/oppg9fig2.JPG)
  Trykk Finish.
  
4. Opprett Object Class «Request». Husk å sette korrekt Data Interpretation i wizarden ved opprettelse av nytt objekt.

   *Kommentar: SQL Script for opprettelse er allerede kjørt i databasen din – dette for at vi kunne generere litt data å gjøre rapporter/analyser på i senere oppgave.*
   1. Sett også default verdi for feltet «Order No». Her velger du «Custom Id Generator» og velger «Order No Counter» i listen. Sett også Subject, State og Type påkrevd. Defaultverdier for State og Type bør også settes. I tillegg bør Received Date settes til «Now» som default, men være mulig å endre i etterkant. Agreed Delivery Date og Expected Delivery Date bør settes med data interpretation «Date» (ikke Date and Time) slik at brukeren ikke trenger å ta stilling til klokkeslett.
   
   Etter opprettelse av objektklassen, sett Default verdier for «Created» feltene, samt Data Calculation for «Modified» feltene . 
   *Kommentar: Sistnevnte gjør at man ved opprettelse setter ordernummer som det siste nummeret som ligger lagret i «Order No Counter» tabellen, og deretter oppdaterer (øker) verdien lagret i «Order No Counter» tabellen med 1 automatisk.*
   
   2. På egenskapene ved Objektklassen «Request» (høyreklikk -> Open på Object Class «Request») setter du på 
      - Search (setter søkeegenskaper, under «Search Properties» på arkfane «Search») 
      -	Events -> Auditing (ønsker å loggføre alle endringer på Request objekter, huk av for «Enable Auditing» under arkfane «Events») 
      -	Display -> Naming (Feltet «Subject» før ihvertfall være en del av navngivningen, dette angir du i arkfane «Display»)
      -	Data Sorting (Feks default sortering på «Company» ascending og «Received Date» descending, finnes i arkfane «Data Sorting»).
  
Vi har nå opprettet objektet Request. Vi ønsker også å kunne dra inn dokumenter og epost på en Request.

5. Utvid objektklassene Mail og Document med *nytt felt Request*

   *Veiledning: SQL for å legge til nytt felt på Document tabellen: «alter table Document add RequestID uniqueidentifier». Kjør tilsvarende for Mail-tabellen. Modeller så opp feltet på begge Object Classene i Studio.*
6. Utvid handlingene «Paste new Mail from file» og «Paste new Document from file» til å ta inn Request som input, og sette referanse til Request ved opprettelse.

   *Veiledning: Samme utvidelse som i oppgave 5.2.b): Utvid med å fylle inn fra Request (input) til Mail.Company, Mail.Contact og Mail.Request dersom Request (input) har verdi. *

Vi er nå klare til å lage Formen for Requests, liste ut Requests i portalen (Navigation Pane) samt liste ut Requests i Company Formen.

7. Opprett en **Form for Request**. Legg til Command+Eventer for opprettelse av Mail og Document ved Paste i de respektive Grid’er, samt for sletting og åpning av epost og dokument fra disse.
   Tips: Formen bør ha en Tab Sheets container ytterst, med en generell arkfane først, deretter Documents og Mail. For å få en velfungerende Ribbon (valgfritt) vil det være lurt å legge command på de respektive arkfanene. Husk da også god navngiving av command og symbol.
   Man kan bruke mye tid på en Form både på utseende, dynamikk (feks dynamiske labels og visibility conditions) og ytlsesoptimalisering (forsinket lesing).
   
8. Legg til **Requests-utlisting** i en ny arkfane på Company Formen. Husk å få med command+event for opprettelse av Ny og for å åpne Request Formen (ved dobbeltklikk på rad). Vi tillater ikke sletting av Requests. Griden bør filtrere vekk Requests i State «Canceled».
  *Veiledning: Gjerne også legg til «Ny»-handling i Ribbon. Finner du et godt symbol for Request?*
  
9. La en ny Table for Requests med et view som lister ut alle «Open» Requests.
   *Veiledning: Se eventuelt tidligere Table oppgave. Pass på å få med et fornuftig kolonneutvalg i Layout, og på View’et setter du Data Filter og at Search skal være enabled. Under Events legger til til Event for «Open a Form» ved menu «New» (husk Create Data) og «Open in New Window» (husk Data Filter).*
   
10. Lag en ny View Button i Navigation Pane (navn «Requests»). Legg til snarvei til «Open Requests» table viewet under denne menyen. Husk å legge på sikkerhet på View Button først, da arver menyinnslagene under sikkerheten. Velg et passende symbol (f eks 1972).
  ![oppg9fig3.JPG](media/oppg9fig2.JPG)
  
11. VALGFRI OPPGAVE: Lag en Rule: **Set Closed Date and Canceled Date when State changed**. Denne skal endre Closed Date hvis State er satt til Closed (og til NULL ellers) samt sette Canceled Date hvis State er satt til Canceled (og til NULL ellers).

12. VALGFRI OPPGAVE: Gjør feltet Request.State «Read Only» og lag handling for «Close Request», «Re-open Request» og «Cancel Request» som endrer State på Requests i henhold. Publiser handlingene på en knapp i Request Form’en (ved siden av State feks) samt i Company Form’en (under Grid’en). Legg også på enabling conditions på knappene som sier feks at «Close Request» er enabled hvis State = Open, «Re-open Request» er enabled hvis State er Closed eller Canceled, «Cancel Request» er enabled hvis State er Open eller Closed.

13. VALGFRI OPPGAVE: Gjør feltene i Request Form’en **Read Only** dersom State ikke er lik Open.
    *Tips: Når du er på en Control i Formen, har du mulighet til å sette condition for property «Read Only» til venstre i Form editoren. Dette trenger ikke settes «per felt» man kan settes på Group’en som ligger rundt feltene. Alt inni Groupen blir da Read Only dersom condition’en slår til.*
    
14. VALGFRI OPPGAVE: Gi arkfanene «Mail» og «Documents» i Request formen en **dynamisk label som teller antall objekter** listet ut (eksempelvis «Mail (3)» og «Documents (1)»).
    *Veiledning:  Her kan det være lurt å bruke fasitløsningen som bistand.*
    1. Du trenger en data source av type Local Object (navn: feks «Label values»). Denne får 2 felter: Mail Label og Documents Label med Type = Function og Data Calculation satt som en Formula (for eksempel, ‘’Mail  (‘’ + Misc.ifNull(mail.size(),0).toString() + ‘’)’’)
    2. Data Filter på det lokale objektet kan ikke leses fra basen, men du kan her sette Data Filter = «Run a local task». Lag en Local Task (under «Tasks») som kun har en Create Objects (av objektet «Label Values»). Koble deretter inn denne tasken i Data Filter på «Label Values»
    3. På property «Label» på arkfanene «Documents» og «Mail» kan du (istedenfor hardkodet navn på label) binde inn hhv feltet «Label Values.Documents Label» og «Label Values.Mail Label». 
Deploy og test! Nå er navngivning av arkfanene dynamiske.
