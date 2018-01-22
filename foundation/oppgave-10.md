# Oppgave 10 Business Intelligence
*SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon på BI-verktøyet Genus Discover sin rapportfunksjonalitet i Genus App Platform.*

I Genus App Platform har vi et produkt «Genus Discovery». Dette er et rapporterings og analyseverktøy. Rapporteringsdelen benyttes i hovedsak for å sette opp forhåndsdefinerte rapporter  for sluttbrukere. 

Verktøyet kan også være tilgjengelig fra klienten for dedikerte brukergrupper slik at også sluttbrukere kan sette opp rapporter selv eller endre eksisterende.

Vi skal nå gjennom et par oppgaver i oppsettet av rapporter. **En kort oppsummering av rapportfunksjonaliteten i Genus Discovery og hva som kreves for å sette opp rapporter er gjengitt her:**

*Du lager en ny Rapport fra Genus Studio -> Discovery -> Reports -> New. Strukturen i verktøyet er logisk strukturert som i screenshot under:*
![oppg10fig1.JPG](media/oppg10fig1.JPG)
 
*For at en Object Class skal bli tilgjengelig som en dimensjon må dette være angitt på Object Class nivå (properties på objektklassen, arkfane «Data Aggregation». For at et Measure skal være mulig å telle på (ref No Of Activities i eksempelet over) må det finnes en Object Class Property ved samme navn som har huket av «Enable as  Measure» (fra eksempelet over: i arkfane «Data Aggregation» når du ser på properties på Activity.No of Activities skal dette være huket av).*

I tillegg må man i rapporten si hvordan No of Activities skal grupperes per måned (det kan jo være basert på «Created date» eller «Completed date». Denne koblingen («Connection») settes opp i rapporten. 

Tilgjengelige koblinger defineres under objektklasse i Studio:
![oppg10fig2.JPG](media/oppg10fig2.JPG)
 
*Merk: Man trenger ikke angi kobling fra Activity til Company da verktøyet selv skjønner at denne skal være tilgjengelig (da Activity har et felt Company). Men dersom No of Activities feks skal grupperes per Country, må man lage en Connection fra Activity til Country via Company.

I rapporten settes koblinger fra No of Activities til “Month” og “Company” dimensjonene opp ved å høyreklikke på No of Activities -> Connections:*
 ![oppg10fig3.JPG](media/oppg10fig3.JPG)

I tillegg har vi satt på filtrering av Activities (kun de i state Completed) under «Local Filters» i screenshot over.

Merk også at når du jobber i Genus Discovery så jobber du i klienten. 

Hvis du legger til en ny Connection feks må du deploye endringene for at du skal ha den ny Connection’en tilgjengelig i rapporten.

1. Lag en ny rapport «Activities per Company Speciality YTD». Rapporten
skal telle antall fullførte aktiviteter per måned per Company Speciality hittil i år. Rapporten skal også summere opp antall aktiviteter horisontalt og vertikalt. Rapporten skal kunne vises som tabellform og som linjediagram for sluttbruker. 

  *Tips: Du trenger her å lage en ny Connection fra Activity til Company Speciality (via Company) slik at verktøyet skjønner hvordan den skal joine seg ut til Company Speciality ved kjøring. Du trenger også å gjøre objektklasse Company Speciality tilgjengelig som en dimensjon i rapporter («Allow this Object Class to be used as a dimension when aggregating data» huket av i arkfane «Data Aggregation» på objektklasse Company Speciality).*

  For å sette på summering kan du høyreklikke på «No of Activities» i rapporten -> Series Calculation og velge å summere både for Months og for Company Specialities. For å få «sum av sum» nederst å høyre hjørnet (sum av aktiviteter for alle Company Specialities for alle måneder YTD) kan du gå inn på begge Sum-funksjonene og huke av for «Calculate intersections»:
  ![oppg10fig4.JPG](media/oppg10fig4.JPG)
 
  For å styre hvilke knapper som skal være tilgjengelig for sluttbruker kan du huke av dette under «Buttons» (øverst til høyre). Velg her mulighet for å shifte periode fram og tilbake, Explore, Normal view (tabell,) Line (linjediagram) og Filter Pane. Merk at brukeren med dette (Normal View + Line) kan velge å se trenden som en linje per Company Speciality eller tabularisk per måned per Company Speciality.

  *Kommentar: Vi har ikke sagt hvordan «No of Activities» er satt opp som Object Class Property – den er den del av «startløsningen» du har fått tildelt. Hvis du åpner Object Class Property «No of Activities» fra Studio kan du se at feltet er av type «Function» - det er med andre ord ikke referert til et feltnavn i databasen (Provider Name), men har i arkfane Data Calculation satt på et RDBMS expression «\*», samt at det i arkfane Data Aggregation er sagt «Count» som aggregation method. Det som skjer når No of Activities brukes som et measure i en rapport er at det lages en SQL som kjører en «select count(\*) from..» og grupperer på dimensjonene satt opp i rapporten.*

2. Lag en ny rapport «Sales per Company last 3 months”. Rapporten skal ha measure «Order Value NOK» og dimensjonene «Month» (velg forrige måned og to måneder tilbake) og «Company». Det skal kun vises Requests av typen «Order» og med state «Closed», og koblingen mot måned skal være basert på Received Date.

  *Tips: Du må gjøre Request.Order Value NOK tilgjengelig som et measure først. Du må også lage Connections fra Request til Month. Sistnevnte finnes det en snarvei for i Genus Studio: Høyreklikk på Received Date -> Create Calendar Connections. Du må også huke av for at Request skal være tilgjengelig som en dimensjon i Data Aggregation.*

3.	Lag en rapport «Company Benchmark» som viser measures «Annual Sales» og «Employees» fra Company, og benytter Company som vertikal dimensjon til å vise et Plot diagram.

  *Kommentar: Se eventuelt på fasiten. Denne rapporten kan benyttes til å spotte selskaper med potensiale og de man bør holde seg unna. Plot diagrammet viser alle Annual saled plotted mot Number of Employees for alle selkaper – et punkt «over kurven» er et selskap som gjør det bra (mye omsetning per ansatt)*

4.	VALGFRI OPPGAVE: Lag en rapport «Sales and Activities per Employee YTD» som har No of Activities, Sales (fra Request.Order Value NOK) og Avg Sales per Request (Formula basert på Order Value NOK / No of Requests).

  Legg også inn et Measure (formula) “Sales Increase” som viser økning eller reduksjon i salg i forhold til forrige måned.

  *Tips: Du må lage en ny object class property på Request: No of Requests (tilsvarende No of Activities). For å få til Avg Sales per Request må du benytte en Formula i rapporteringsverktøyet. I en Formula kan du kun sette opp uttrykk basert på de Measures som er lagt ut i rapporten (under «Values») – derfor trenger du å legge inn No of Request her, og sette denne Hidden.

  For å lage formula for Sales Increase trenger du et Measure som viser Sales forrige måned. Du kan kopiere «Sales» (høyreklikk -> copy), rename denne til «Sales (last month)» deretter gå til instillingen «Period Shift» og legge til «-1». Deretter lager du Formula som «Sales» - «Sales (last month)».

  Pass også på at du på measure for Sales filtrerer kun Requests i State «Closed» og Type «Order». Dette kan du gjøre «per measure» (høyreklikk -> Local Filters) ELLER du kan legge inn Request State og Request Type i seksjon «Filters» i rapporten og sette filter her. Sistnevnte gjør at hvis Measurene (for Sales) har en connection mot disse, og disse har filtrering vil også measurene filtreres i henhold. For å slippe å sette opp Connection «hver gang» for hvert measure for sales kan du på Object Class «Request» sette opp default connections i arkfane «Data Aggregation» - da settes connections for deg i rapporter.*

5. **VALGFRI OPPGAVE: Legg til snarveier til rapportene i Navigation Pane.**
*Kommentar: Alle rapportene (gitt at du har rettigheter på dem – det ligger i likhet med Tasks sikkerhet per rapport også) er uansett tilgjengelig fra meny «Discover» i klienten. Men enkelte rapporter av høy viktighetgrad eller som benyttes ofte kan man legge inn snarveier til i Navigation Pane. Se eventuelt fasitløsningen hvordan det er valgt å legge ut rapporter her.*

<br>
<table>
   <tr><td><a href="oppgave-09.md"><- Previous exercise</a></td><td align="right"><a href="oppgave-11.md">Next exercise -></a></td></tr>
</table>
