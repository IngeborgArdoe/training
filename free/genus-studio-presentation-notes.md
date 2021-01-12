* Forklare hvor man finner hjelp ([www.genus.no](http://www.genus.no/) og flow.genus.net)
* Når vi lager løsning «fra scratch»
 - Hva er forretningsobjektene?
 - Hvordan henger disse sammen?
 - Hvilke egenskaper har de?
 - -> DIAGRAM for DRAFTING OG OVERSIKT
* Objektklasse = Forretningsobjekt
* Objektklasse properties = Egenskaper ved forretningsobjekt
* På forreningsobjekene og egenskapene definerer vi
 - Layout
  - hvordan skal feks «en person» vises i løsningen?
  - Hvordan skal «personer» listes ut?
  - Også mulig å lage komplekse skjermbilder som viser mange forretninsobjekter og tekst – helt skreddersydd. Eksempel er en enkel CRM modul som viser mine selskaper, og for valgt selskap vises detaljer, kontaktpersoner, aktiviteter, epostdialog og dokumenter.
 - Søk (hvilke felter skal være søkbare? Fritekstsøk?)
  - Mulighet for å søke i alle forretningsdata som er definert som søkbare. Kan også søke «avansert» (fritt) i strukturen, eksempelvis «Finn personer som i i år eller i fjor hadde et oppdrag hos en kunde innen Kantinedrift, og som akkurat nå er ledig»
  - Mulighet for sluttbrukere å få lagre søk eller utvalg av objekter (evt at vi setter opp forhåndsdefinerte søk... [Search folders])
 - Forretningslogikk!
  - Handlinger initiert av bruker [ACTIONS]
   - Enkle som feks endre status på en person
   - Avanserte / stegvise prosesser som feks «sett opp lønn og pris, generer arbeidskontrakt og sende dette til person» i en wizard
   - Generering av rapporter, åpning av filer med genererte data (kan også flette inn data i feks word maler -> «arbeidskontrakt» feks), eksport og import av data fra filer og via internett, mmm
   - MULIGHETENE er kun begrenset av byggeklossene i Genus. Dette har løst så og si alle våre kunders funksjonelle ønsker. Om noe ikke er støttet, er ofte Genus fleksible ifht å utvide støtten i rammeverket.
   - En action kan sees på som en metode eller funksjon hvis de drar paralell med programmering – en action kan ha input parametre, og den kan returnere data. Inni en action utføres et sett av effekter i sekvens... evt gjennom iterasjoner.
  - Automatiske regler (trigget av en hendelse) [RULES].
   - MERK: Samme måte og mulighet å sette opp logikk og funksjonalitet som i brukerhandlinger, men trigget av en hendelse, feks at en ansvarlig for en kunde endres -> send epost til forrige ansvarlig.
  - Agenter [AGENTS]
   - Mulighet til å kjøre forretningslogikk på planlagte tidspunkter. Det kan for eksempel være monitorering av tjenester, generering av rapporter eller oppdatering av data mot eksterne systemer.
  - Web services [WEB SERVICES]
   - Konsumere (hente) eller tilby informasjon. Hyppig benyttet som integrasjon mot eksterne systemer. F.eks. oppslag i Enhetsregisteret.
 - Sikkerhet
 - Analyser og rapporter
  - Eget analyseverktøy – «BI i Genus».
  - Brukes til å sette opp forhåndsdefinerte analyser for sluttbrukere, enten det er toppledelse eller noen «på linja».
  - Nevn eksempler på bruk. Norgesgruppen, andre prosjekter...
  - Vert
*-* I tillegg definerer vi menyen i Genus klienten (navigation pane)