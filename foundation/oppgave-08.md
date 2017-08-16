#Oppgave 8 Documents, Send Mail
Vi skal nå utvide løsningen med mulighet for å dra inn dokumenter i en arkfane på Company. 

Dette krever at vi modellerer opp et objekt Document (a la «Mail») som lar oss lagre filen i databasen samt handlinger for «drag & drop» inn og ut av Genus CRM.

1.	Modeller opp Object Class «Document».

  *Veiledning: Vedlagt er SQL’en for å opprette tabellen for å spare tid. Viktig ved modellering er at Data Interpretation på File Name, Fila Data, File Extension og File Size settes (til de innebygde data typene i Genus med samme navn).*

  SQL: 

  CREATE TABLE Document

  (DocumentID uniqueidentifier PRIMARY KEY,

  FileName varchar(240), 

  FileData varbinary(max), 

  FileSize int, 

  FileExtension varchar(30), 

  CreatedDate datetime, 

  CreatedByUserID uniqueidentifier, 

  ModifiedDate datetime, 

  ModifiedByUserID uniqueidentifier, 

  CompanyID uniqueidentifier

  )

2.	Legg til Document.File Data som et søkefelt på Company.

  *Veiledning: Dette gjør at man fra søk i Selskap kan gjøre fritekstsøk i fildataene på tilhørende dokumenter. Dette setter du opp ved å legge til Document.File Data i «Search» arkfanen på egenskapene for Object Class «Company». *

  OBS: For at man skal få opp «Full text» søkeoperatorer når man søker i feltet, må man inn på Object Class Property «Document.File Data» og sette på «Full Text and Like operators» i arkfane «Data Filtering».

3.	KJØR EN DEPLOY TO ALL. Grunnen er at det snart skal settes opp et «File Preview» - og da benyttes noen kall mot serveren som krever at serveren har kjennskap til denne nye objektklassen.
4.	Lag en ny Task: **Paste new Document from File** som tar Company og File(s) som input, og oppretter Document(s).
  Tips: Her trengs 3 datasources; en av typen Company (navngi denne «Company (input)», kardinalitet one), en av type General File (navngi denne «General file (input)», kan være unbounded) og en av typen Document (som skal lages, kan være many). Tasken har meget enkelt logikk, her trengs kun et scope og en effekt Create Objects. Se eventuelt på tilsvarende handling «Paste new Mail from file». Husk også å sette sikkerhet på tasken etter opprettelse.

  Et annet tips: Vi får fil-input med kardinalitet «unbounded». For hver fil skal vi lage et Document. Her kan man enten benytte en enumerator som looper gjennom fil-input data sourcen ELLER (enklere) vi kan lage en Create Object på data source Document som vi binder mot General File-data sourcen på toppnivå – da får vi opprettet et document per instans av fil i data sourcen for fil-input!
  ![oppg8fig1.JPG](media/oppg8fig1.JPG)
5.	Lag en ny arkfane for grid-utlisting av dokumenter på Company-formen. Legg til passende kolonneutvalg og sortering, og legg til handlingen du laget over som en Command i Document-tab og med Event i Grid’en. Legg også til command+event for Delete og Invoke a file (dobbeltklikk og åpne dokumentet). 
  Lag også et «File Preview» til høyre for Griden som forhåndsviser filen (se arkfane «Mail» for tips).
  Tips: For at eventen skal trigge på «paste» til Griden, velger du «Menu: Paste Special» på eventen. Merk at du på data filter som input til tasken sin «General File» data source kan filtrere vekk fil typene mail message og calendar item – dette fordi du ikke ønsker disse filtypene lagret som «Document» (men som Mail eller Activity):
  ![oppg8fig2.JPG](media/oppg8fig2.JPG)
6.	VALGFRI OPPGAVE: Lag en task **Copy Document to Clipboard as File** tilsvarende «Copy Mail to Clipboard as Mail Message» som du publiserer til document Griden. 
  Tips: Tasken tar Documents som input og oppretter General Files, publisert til Grid på Meny «Copy».
7.	VALGFRI OPPGAVE: Legg til **delete og paste i Ribbon.**
  Tips: Ny Section under Context Tab Group Document, Tab Document Management: Tab Section Manage for Delete og Tab Section Clipboard for paste. Husk symboler og enabling condition (for Delete).

  Vi skal nå lage funksjonalitet for å sende epost til en kontaktperson og lagre eposten som «Mail». Denne oppgaven er også valgfri, men det anbefales å i det minste se i fasitløsningen hvordan denne er løst.
8.	VALGFRI OPPAVE: Opprett en ny task: «Send Mail to Contact» som du publiserer til en knapp på Contact form’en samt på en knapp i Griden for kontaktpersoner i Company Formen. 
  1.	Opprett tasken. Tasken skal åpne et mailvindu, og ved trykk på send skal mailen lagres som et Mail objekt.
  
  Veiledning: Tasken trenger «Contact» som en datasource (many). I tillegg trengs en File datasource av typen «Mail Message» som er outlook-filen som skal opprettes i minnet og sendes ut. Etter at denne er sendt ut skal den lagres ned som Mail objekt – en fil per Contact. Vi trenger altså en datasourc e Mail (many).
  
  Tasken trenger videre effektene «Create a Mail Message» (som oppretter et Mail Message fil med kontaktenes epostadresse i To-feltet og lagrer til data sourcen «Mail Message»), en «Open a Form» effekt (som åpner Mail Message window fra fildata feltet til «Mail Message» og en «Create Objects» effekt (som lagrer Mail objekter).
  
  Se fasitløsningen for ytterligere veiledning. Husk sikkerhet på tasken!
