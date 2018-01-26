# Introduksjon til modellering
Første del av oppgavene vil gå ut på å modellere opp nye objektklasser. En Genus App Platform-applikasjon levert til en kunde, vil typisk støtte opp hele eller deler av kundens forretningsmodell. Eksempelvis kan en applikasjonsmodell for vikarbransjen dekke store deler av deres forretningsmodell gjennom å støtte hele saksbehandlingen, rapporteringsbehov, dokumentarkiv, kommunikasjonskanal (mail/sms), og integrasjon mot eksterne systemer. Hos noen kunder kan rapporteringsdelen ha større fokus, mens andre kunder igjen har søk i forretningsdata som hovedfokus.  

Felles for alle applikasjonsmodeller, enten dette er “full-skala” saksbehandlingsløsninger, Business Intelligence-rettede løsninger (virksomhetsstyring med rapporter og analyser som fokus), eller med tekniske integrasjonsløsninger, så har alle disse en objektmodell. 
En objektmodell er forretningsobjektene til kunden, koblet sammen. Objektmodellen tilsvarer ofte datamodellen vi ser i databasen, men denne er modellert opp («gjenspeilet») i Genus App Platform, og kan ha ytterligere logiske koblinger, tilleggsinformasjon, og til og med objektklasser som kun finnes i Genus App Platform (ikke i databasen). Fordelen med å lage objektmodellen i Genus App Platform, er at Genus App Platform da vedlikeholder koblinger, avhengigheter, primærnøkler, datakonsistens, datatyper, opprettelse, endring og sletting av data. Regler for sletting, duplikatregler, valideringsregler, automatiserte regler (tilsvarende “triggere” i databasespråket) – alt dette holdes styr på i Genus App Platform. 

Objektmodellen eksponeres mot sluttbruker gjennom oppsett av tabeller eller «Forms», kombinert med handlinger, søk m.m., gjennom Genus Desktop klienten (som du ble kjent med i oppgave 1). Utvikler setter opp objektmodell, logikken i handlinger, søk, og GUI gjennom verktøyet Genus Studio (som du nå skal bli mer kjent med).

I Genus Studio refererer vi til et objekt (feks «Company») som en «Object Class». Egenskapene til Company (som eksempelvis «Name» eller «Org No») kalles «Object Class Property» eller «Property». 
Genus CRM fasit har en enkel objektmodell beskrevet i Case-beskrivelsen (kapittelet over). Det som mangler i din EDU løsning er Contact, Contact Log, Document og Request. Første del av oppgavene i Studio blir å utvide objektmodellen med Contact & Contact Log.

 
Fig.1.1.: Objektmodellen for Genus CRM i initiell versjon. Diagrammet fås opp fra Studio: Velg noden “Object Class Diagram».  Her ser vi 5 Object Classes, hver med en rekke Object Class Properties. 
MERK: Et diagram er kun et tegnebrett hvor man kan visualisere et utvalg av objektene i løsningen (alle objekter som finnes er listet noden «Object Classes» i studio). Her får man automatisk opp relasjonene. Om man sletter et objekt fra diagrammet blir det kun borte fra diagrammet («tegningen») du har åpent – objektet fjernes ikke fra løsningen.


##Oppgave 2 (Stikkord: Enkel modellering; Object Classes og Properties)
Du skal nå modellere opp Object Class «Contact» med de Object Class Properties som kreves og er naturlige for en kontaktperson. For å opprette en Object Class, kreves det at det finnes en tilsvarende tabell i databasen som objektklassen kan referer til.

Det finnes to måter å lage en ny Object Class på.
- Alt 1: Du vet hva du skal lage, og er stødig på SQL: Du skriver da en SQL for å opprette tabellen og felter for «Contact» i databasen. Deretter oppretter du objektet (Object Class or Object Class Properties) i Genus Studio.

- Alt 2: Du ønsker å kladde objektet i Genus Studio først, for deretter å få generert opp SQL’en som skal kjøres i databasen for å lage tabellen.  Til dette benyttes Object Class Diagrammet – her kan man lage «Draft» Object Classes og Object Class Properties som ennå ikke finnes i noen database. Dette er nyttig når man er i en design-fase av en hel eller deler av en objektmodell, og ønsker å gå QA-runder på objektmodellen før man beslutter å lage tabellene i databasen. Det er nemlig enklere å gjøre endringer på Draft objekter enn det er å gjøre endringer etter at man har laget tabellen tilhørende Object Class(es). Sistnevnte krever endringer 2 steder for å for eksempel fjerne eller legge til et felt – både i databasen og i Genus Studio.

I første oppgave går vi veien om Alternativ 2 for å gjøre dere kjent med denne muligheten. I resterende oppgaver vil vi gå rett på Alternativ 1 (lage tabellen eller feltet i databasen først, deretter modellere opp dette i Genus Studio).

1. Opprett en Draft objektklasse for «Contact».
   *Veiledning: Gå til «Object Class Diagram». Høyreklikk -> Insert -> Class (Draft). I dialogboksen som kommer opp setter du Logical Name lik navnet på objektet i Genus (“Contact”) og Physical Name lik navnet på tabellen som skal lages (“Contact”).*
  ![oppg2fig2.JPG](media/oppg2fig2.JPG)
 
   Draft objektet «Contact» er nå laget, og du ser at denne er gråfarget til forskjell fra Object Class’ene som allerede finnes i diagrammet. Det lages automatisk 1 property for objektet: «ID», som er primærnøkkelen for tabellen / objektet. 

2. Legg til følgende Properties på Contact:	
   1. FirstName (varchar(60))
   2. LastName (varchar(60))
   3. Company (Outbound reference til objektet “Company”)
   4. Mail (varchar(120))
   5. Mobile (varchar(20))
   6. Position (varchar(100))
   7. State (Outbound reference til objektet / code domainet “Object State”. Dette er et internt kodeverk bestående av «Active» eller «Inactive»)
   8. Created Date (datetime)
   9. Created By (Outbound reference til objektet «User»)
   10. Modified Date (datetime)
   11. Modified By (Outbound reference til objektet «User»)

*Veiledning: Du kan nå legge på Object Class Properties på Draft objektet ved å høyreklikke på:*

  «Contact» -> Insert -> Property (Draft) (evt CTRL -Shift - +). 
  
Referanser til andre klasser kan «dras» inn i en Object Class Draft ved å holde inne Alt-tasten, markere et objekt og dra det inn. Da får man automatisk med seg den riktige datatypen og outbound reference blir satt for deg.

  ![oppg2fig3.JPG](media/oppg2fig3.JPG)
  ![oppg2fig4.JPG](media/oppg2fig4.JPG)

Når man legger til en ny draft Property angir man Logical Name (navnet på feltet i Genus CRM), Physical Name (navnet på feltet i databasen), Outbound reference (hvilket objekt feltet peker mot dersom det er referanse til et objekt i løsningen, feks «Company»), Data type (feks «varchar(120)» der 120 er antall tegn, «int» for heltall, uniqueidentifier dersom det er en primærnøkkel eller ID-referanse.. Datatypen settes automatisk dersom man velger Outbound Reference). Trykk OK.

Best Practice på navn på felter i databasen (Physical Name): Samme som Logical Name, men uten space og «camel case». Feks: Logical Name «First Name» får «FirstName» som Physical Name. Unntaket er referanser til andre objekter: Propertyen “Company” bør ha Physical Name “CompanyID” for å indikere at feltet er en referanse til ID’en til et annet objekt.

3. Gå til menyen «Actions» (øverst i Studio)-> «Forward Engineering» og velg objektet «Contact» i dialogen. Trykk Next to ganger. Du får nå generert opp et SQL script for å opprette tabellen «Contact» i databasen. Kopier dette scriptet og kjør det (i SQL Server Management Studio) mot databasen (GenusCRM_EDUXY_Data).

Vi har nå laget tabellen for «Contact» i databasen. Vi skal nå modellere opp selve Object Class’en for Contact.

Vi presiserer igjen at man ikke må opprette Draft objektklasser, men at vi her gjør det da det er god rutine for å verifisere objektmodellen sin mot andre (internt / kunder) før man oppretter tabeller i databasen og modellerer opp de faktiske objektklassene. Det er lettere å endre en Draftmodell enn det er å endre objektmodellen straks objektene ikke er drafts lenger. Vi bruker alltid en del tid på objektmodellen når vi designer forretningsapplikasjoner – da det som kjent er mer kostbart å endre en applikasjon på «datalaget» straks brukergrensesnitt og logikk har blitt lagt på.

4. Opprett objektklassen «Contact» i Studio.
  *Veiledning: Gå til noden Object Classes i Studio og høyreklikk -> New -> Object Domain. Gå gjennom wizarden.* 
   1. Første steg: Velg databasen det skal leses fra (settes default dersom kun 1 database, men en applikasjon i Genus kan ha tabeller liggende i flere ulike databaser.)
   2. Andre steg: Velg tabellen du skal modellere opp («Contact»). Her har man mulighet til å overstyre navnet på objektet vist i Genus CRM (feks dersom tabellen har et teknisk navn)
   3. Steg «Table columns»: Velg her hvilke av kolonnene i databasetabellen du ønsker å modellere opp. Her er default alle valgt, trykk Next.
   4. Steg «Primary key»: Velg her inn property «Contact ID» og huk av for «generate identifier automatically» -> Dette gjør at Genus håndterer unikhet og opprettelse av primærnøkkel.
   5. Steg  «Property definitions»: Dobbeltklikk hver rad for å se og evt endre data type og data interpretation. Her er det vikig at Data interpretation blir endret der det er nødvendig. For eksempel – feltet «Created by» skal være en referanse til objektet «User».. Dette skjønner ikke Genus med mindre du selv angir det. Dobbeltklikk på denne raden og endre data interpretation til å være «User». (Data Interpretation -> User. Når du gjør dette vil Display name også endres til «User», endre dette navnet til «Created by»).  Gjør tilsvarende for feltene Company (interpretation «Company»), State (interpretation “Object State”), Modified By (interpretation “User”) og Mail (interpretation “E-mail”). Sistnevnte gjør at Genus skjønner at feltet er et epostfelt – da får du validering av epostadresser gratis med på kjøpet.
   6. Steg «Naming»: Dette er propertyen som angir standard navngivning av objektet. Her kan du trykke Add.. og  legge til First Name og Last name. Trykk Finish.

Hvis du nå utvider noden «Object Classes» i Studio ser du objektet Contact. Hvis du utvider noden Contact og trykker på Properties, finner du listen med Object Class Properties for Contact objektklassen.

5. Endre følgende innstillinger på Property-ene til Contact (ved å dobbelklikke på property-en):
   1. Company, First Name og Last Name: Arkfane «Data Validation», huk vekk «Allow blank value». Feltet blir med andre ord påkrevd.
   2. Created Date:
      1. Arkfane “Security”, huk av for “Read”. Feltet blir med andre ord Read Only for sluttbruker. 
      2. Arkfane «Data Calculation»: Set Default = Time Stamp. Feltet settes til gjeldende tidspunkt på serveren ved opprettelse av en Contact, og dette er heller ikke redigerbart i etterkant.
   3. Created By: Sett samme Security som Created Date, men sett Default verdi til «Active User Account Stamp». Feltet settes med andre ord til pålogget bruker, og er ikke redigerbart i etterkant
   4. Modified Date:
      1. Arkfane «Security», huk av for «Read».
      2. Arkfane «Data Calculation», set Formula = Time Stamp. Formulas oppdateres her gang et objekt endres, med andre ord så oppdateres Modified Date nå automatisk hver gang en bruker gjør en endring på en Contact.
   5. Modified By: Samme Security som Modified Date, men sett Formula = Active User Account Stamp. Feltet settes altså til pålogget User hver gang en Contact endres.
   6. State: Arkfane «Data Calculation»: Sett Default = Active. Feltet settes altså til Active når en kontaktperson opprettes, men kan endres i etterkant. Merk også at feltet har Data Type int: Det betyr at det i basen lagres et tall, som i Genus mappes opp til Code Domain «Object State» som sier at 1 vises som «Active» og 2 vises som «Inactive». Dette kan du se ved å høyreklikke på object class «Object State» -> Open -> Data Entries.
   7. Mail: Vi ønsker at feltet kan være blankt, men at det skal komme en tekst ved blankt om at «feltet bør ha verdi»:
      1. Arkfane «Data Validations», trykk «Add»
      2. Legg til en Condition «Contact.Mail has no value»
      3. Huk av Impact = “Notify user and ask for confirmation for proceed” og “Notification Message” (skriv en passende tekst, “Mail should be set” etc).

Vi har nå laget objektet «Contact» nesten ferdig. Siste steg er å sette noen egenskaper ved selve objektklasse «Contact»

6. Høyreklikk på Object Class «Contact» -> Open.
   1. Arkfane “Events”. Huk av for “Enable auditing” og deretter “Mandatory” på “Modify”. Trykk Apply. Dette gjør at han i klienten kan høyreklikke på en Contact, og se endringshistorikk for kontaktpersonen – hvilke Users har gjort hvilke endringer.
   2. Arkfane «Data Sorting» -> Trykk «Add..» og legg til First Name deretter Last Name. Dette gjør at det vil default sorteres for fornavn og etternavn der det i løsningen listes ut kontaktpersoner uten at sortering er angitt. 
   3. Arkfane «Data Filtering», under «Auto Complete» -> Trykk «Add..» og legg til First Name, Last name og Mail. Dette gjør at i et felt hvor Contact skal angis, feks som kundekontakt på en forespørsel (kommer senere i oppgavene), kan skrive deler av fornavn, etternavn eller epost og trykke Tab for å gjør en lookup på kontaktpersoner som matcher det du har skrevet inn på et av disse feltene.
   4. arkfane «Data Integrity», trykk «Change» på «Uniqueness Contstraint». Trykk “Add”. I vinduet som åpnes kan man sette krav til unikhet på kontaktpersoner som opprettes.  Her kan du si at «hvis Epost har verdi» sjekk om det finnes andre kontaktpersoner med samme epost og gi en advarsel til brukeren.

    *Veiledning: Se screenshot under*
    ![oppg2fig5.JPG](media/oppg2fig5.JPG)
 
   Her møter du «Condition editoren» til Genus for første gang. Den brukes hver gang man skal stille krav til noe, og den vil her generere en SQL som sjekker om det finnes en Contact i databasen med samme epost som det du forsøker å lagre før lagring av en Contact. Hvis det gis treff, vil bruker få en advarsel. Her får brukeren likevel lov til å lagre kontaktpersonen iom at det øverst er huket av for «Notify user and ask for confirmation to proceed» i motsetning til valget over (der man ikke får lov å lagre før epost er endret).
   5. Arkfane «Search», seksjon «Search Properties» -> Trykk «Modify», og legg til egenskapene som skal være søkbare (ihvertfall Company, First name, Last Name). Her kan du legge til propertes som skal dukke opp i søkepanelet øverst i klienten når man foretar et søk etter Contacts. 
    
  **Trykk OK.** Objektet Contact er nå komplett og klart for å legges til i grensesnitt og eventuelt få lagt på ytterligere funksjonalitet. 

Merk at man når som helst kan gå tilbake og justere egenskapene ved Object Class og Object Class Properties med noen få unntak (feks Data Interpretation på Object Class Property – hvis denne skal endres i etterkant nå propertyen slettes og legges til på nytt). Man kan også legge til ny Object Class Properties på en Object Class i etterkant (feks om man ønsker å legge til Photo på Contact) ved å kjøre wizard «Add object class properties» fra høyreklikk på objektklassen i Studio – men man må da ha utvidet tabellen i databasen med det nye feltet i forkant.

7.	Vi kom nå på at vi mangler et felt for ansvarlig bruker på kontaktperson. 
   1. Lag et nytt felt på Contact: Responsible.
   *Veiledning: Feltet må legges til i databasen først: Det kan gjøres ved å kjøre SQL «alter table Contact add ResponsibleUserID uniqueidentifier». Gå deretter til Object Class «Contact» -> Høyreklikk -> «Add Object Class Properties..». Trykk Next i første dialog. I andre dialog leser Genus opp felter fra tabellen som ikke er modellert opp ennå. Trykk Next. I dialogen «Property Definitions», dobbeltklikk på raden og endre Data Interpretation til «User» (pass på å endre Display Name til «Responsible» igjen etterpå). Trykk OK og Finish*.
   2. Sett Default verdi for Responsible til  «User (User Account)» (Active User Account).
Veiledning: Merk, dette er ikke det samme som «Active User Account Stamp».  Active User Account Stamp vil si (tilsvarende Time Stamp) at default verdien settes på server-side, og vi får dermed ikke mulighet til å endre feltet i klienten. Velg isteden F3 (se screenshot under) – deretter kan du velge User (User Account) som er pålogget brukerkonto på klienten.

  ![oppg2fig6.JPG](media/oppg2fig6.JPG)
 

8. Draft-objektet du laget i Oppgave 2.2 trenger du ikke lenger. Gå til Object Class Diagram -> Høyreklikk på Draft objektet «Contact» og velg «Replace Draft». I dialogen velger du Object Class «Contact». Draftet slettes, og på tegningen erstattes det av den modellerte objektklasse Contact
