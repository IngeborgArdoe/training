#Brukergrensesnitt i Genus App Platform: Forms, Tables, Ribbon og handlinger
**SESJON FRA VEILEDER:** *Før oppgaven starter skal veileder ha holdt sesjon rundt oppsett av Forms og Tables i Genus. Gi beskjed dersom du kommer hit før sesjon er avholdt.
Vi har nå laget objektet Contact, men det er ennå ikke mulig for sluttbruker å se eller å registrere Contacts – vi må legge dette ut i et brukergrensesnitt. Her kommer litt info om brukergrensesnitt i Genus – les dette før du går over på neste oppgave:*

I Genus App Platform har vi to hovedkonstruksjoner vi bruker til å vise informasjon; Tables og Forms. Både Tables og Forms kan bruke Ribbon. En Ribbon er en kommandolinje som viser relevante hjelpemidler og kommandoer i vinduet.

##Table 
Tables brukes for å lage enkle lister eller aggregerte utlistinger som brukes til filtrerte utlistinger eller søk etter data. Tables legges typisk ut i Navigasjonspanelet til venstre i klienten, slik som feks snarveien «Customers» i Genus CRM. 
Tables kan også kobles inn i Forms (kan brukes til å feks liste ut Contacts på et selskap) med til dette formålet har Forms også en egen control (GRID) som er raskere å settes opp. Hvis derimot et objekt skal listes ut i mange Forms kan en table være nyttig å opprette pga gjenbruk på tvers av Forms.

##Forms 
Forms er skreddersydde skjermbilder som kan vise felter, utlistinger, knapper, file-preview m.m. i et og samme skjermbilde, nærmest uten begrensninger på layout (en rekke tradisjonelle og «bleeding edge» layout controllere finnes i verktøykassa til Forms). Forms kan brukes til å vise data for ett til mange objekter i samme view, og man kan også bytte mellom ulike views (for å lage «wizard»-basert funksjonalitet). Man kan også vise grafer etc («dashboards» for sluttbruker). En Form kan være tilpasset Desktop, eller Apps – sistnevnte vil si at man kan modellere opp en hel plattformuavhengig mobil-app eller webside i Genus Studio.

Forms kan i sitt enkleste format være visning av et objekt (feks skjermbildet for detaljer om 1 kontaktperson). Men Forms kan også være basert på Use Cases; For eksempel et skjermbilde for behandling av dine aktiviteter med utlistinger, advarsler, knapper, detaljinfo & preview etc i en og samme skjermflate. 

Inne i en Form finnes to konstruksjoner for utlistinger: GRID og TABLE. Sistnevnte kobler inn en eksisterende table i Formen (feks dersom man skal liste ut samme objekt i mange Forms, kan det være lurt å lage en Table pga vedlikehold og gjenbruk), mens førstnevnte settes opp per Form (man kan da tilpasse kolonneutvalg og tilgjengelige handlinger per Form, men det krever mer arbeid / vedlikehold dersom samme utlisting skal gjentas i ulike Forms).

##Ribbon

I både Forms og Tables er det mulig å lage en brukervennlig menystruktur ved bruk av Ribbon. En Ribbon minner om menystrukturer brukere er vant til å møte i Microsoft Office-verdenen og i Windows (10) generelt. Commands (kommandoer som er satt opp i formen) kan kjøres fra en Ribbon og en kan bruke Context for å vise ulike meny-elementer når en navigerer i ulike deler av grensesnittet.

Oppgavene rundt brukergrensesnitt er ikke så strengt detaljert som resterende modellering, da man står mer fritt til å definere utseende selv. 
