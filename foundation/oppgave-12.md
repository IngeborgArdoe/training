# Oppgave 12 - Mail Merge
*SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon rundt Mail Merge hvor konseptet forklares og schema-editoren i Genus App Platform vises.*

Oppgaven er valgfri og man må se an tiden man har til rådighet litt. Det anbefales uansett å lese gjennom oppgaven.

**VALGFRI OPPGAVE:** Lag en ny handling «Order Confirmation» som tar Request som input og som genererer en ordrebekreftelse (et word dokument) fra Requesten. Informasjon som skal flettes inn er Order No, Subject, Description, Expected Delivery Date, Order Value NOK og Company Name, Org No, Contact Name (bestiller), ResponsibleName (navn på brukeren).

1. Opprett et schema “Order Confirmation” med “OrderConfirmation” som rotnode og feltene i beskrivelsen over som Elements (alle kan være av data type String)

   *Veiledning: Her kreves at du har fått gjennomgang i hvordan sette opp Schemas. Et Schema er en beskrivelse av hvordan en xml skal se ut. Når man senere benytter «Create Objects» mot dette schemaet som en data source, vil det laget en xml. Denne xml’en kan brukes som input til «Merga Data to a Document» effekten sammen med en word fil. Denne word-filen inneholder tag’er med samme navn som xml-elementene, og da vil effekten flette inn data i disse feltene. Se eventuelt fasitløsningen på hvordan dette schemaet skal se ut.*

2. Opprett et Word dokument for Order Confirmation med flettefelter ihht navn på feltene i schema i punktet over. 
   *Veilening: Du setter inn «merge field» i word ved å markere stedet du vil legge inn feltet i dokumentet og deretter gå til meny Insert -> Quick Parts -> Field. Deretter velger du «Merge Field» fra lista, og skriver inn feltnavnet (samme som i schema) i «Field Name».*

   Du må alltid starte dokumentet med et merge field med Field Name = «TableStart:OrderConfirmation» hvor «OrderConfirmation» er navnet på rotnoden i schemaet (eller noden som inneholder feltene du skal flette inn). Tilsvarende må det på slutten av dokumentet ligge et merge field med field name «TableEnd:OrderConfirmation». Imellom disse to flettefeltene kan du legge inn merge field med feks field name «OrderNo». Tips, du kan kopiere flettefelter og deretter høyreklikk og «Edit Field...», da går det raskere.

   Spør eventuelt veileder om å få tilsendt dette word-dokumentet om du ikke ønsker å bruke tid på å lage en word mal for ordrebekreftelse.
   
3. Opprett task «Order Confirmation». Publiser denne på en knapp i Request Form’en.

   *Veiledning: Tasken trenger data sources «OrderConfirmation» (xml schema), Request (input) og Document (to be created) og General File (temp, skal brukes som midlertidig output i flette-effekten før Document creates). Tasken trenger effektene «Create Objects» (som creater OrderConfirmation or mapper verdier til feltene), «Merge Data to a Document» (hvor du legger inn word dokumentet ditt som «Embedded file», OrderConfirmation som «XML Document» og General File som» Output Document») og en ny «Create Objects» (som oppretter et Document objekt med fildata fra General File objektet), samt til slutt en «Invoke a file» (som åpner Document.File Data i word).*

4. **EKSTRA:** Lag en handling «Send Order Confirmation» som lar bruker få blant eksisterende Order Confirmations (Documents på Requesten), og deretter åpner outlook med dokumentet som et attachment. Handlingen bør også lagre Mail objektet. Publiser tasken til Ribbon i Request formen.
  
   *Veiledning: Tasken trenger data sources Request (input),, Mail (to be created), Document (bekreftelsesdokumentet som skal legges ved eposten), Mail Message (temp file som åpnes i outlook og som brukes til opprettelse av Mail-objektet etter sending).

   Tasken bør ha effektene:
   * Effekt “Read Object” på data source Document med user interaction (la brukeren velge blant documents knyttet til requesten)
   * Create a Mail Message (som setter verdier for To-feltet, Subject, legger ved attachment (Document.File Data) og setter forslag til eposttekst). Effekten skal ha innstilling «Write message to a data source» (Mail Message (temp)) slik at eposten ikke sendes ennå. 
    
   Dette for at vi skal ta vare på Mail Message filen i en datasource slik at det ved eksekvering lagres tilbake til tasken de endringer gjort i din outlook. Her kunne det vært brukt en Open a Form effekt direkte, men det er mer visuelt å lage epost-filen via «Create a Mail Message» effekten.
   * Open a Form (velg Mail Message Window) og Modify. Huk av for “Wait until the form is closed”. Denne åpner outlook med foreslått epost og vedlegg (gitt av forrige effekt) og pauser eksekvering til brukeren har trykket på “Send” i outlook.
   * Create Objects (Mail). Mapp inn felter fra Mail Message (temp) for å lagre epost objektet.*
