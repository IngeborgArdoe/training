# Oppgave 15 (Stikkord: Web Services)
*SESJON FRA VEILEDER: Før oppgave 13 starter skal veileder ha holdt sesjon rundt oppsett av Web Services hvor konseptet forklares og schemaeditoren i Genus App Platform vises.*

Hele denne oppgaven er valgfri, og du må se an på tiden du har til rådighet. Viktigst er det at du leser igjennom oppgaven.

Web Services settes enkelt opp i Genus App Platform. En Web Service satt opp i Genus App Platform ligger tilgjengelig på applikasjonsserveren slik at andre applikasjoner kan kalle løsningen vår for å utføre web service operasjonene vi tilbyr. Dette kan eksempelvis være «GetCompanies» eller «CreateActivity» dersom vi skal ha en ekstern løsning som skal hente eller oppdatere data i vår Genus CRM løsning. En Web Service krever at vi har definert opp formatet på input og output fra web servicen (xml), så vi må ha satt opp schemaet for dette i schemaeditoren først (eventuelt importert et eksisterende schema hit først).

**VALGFRI OPPGAVE:** Opprett en web service «GetCompaniesForUser» som tar som input en xml med et felt: brukernavn, og returnerer som output en xml med en liste av companies med felter: ID, CompanyName, OrgNo, Employees, AnnualRevenue og PostalAddressCity.

For å teste denne kan du benytte «Test run» i klienten hvor du på forhånd lager en xml-fil med UserName som input.

Veileding: Først må du laget et Schema i Schemaeditoren (navngi denne feks «CompanyServiceSchema»). Denne bør ha 2 elementer:
* GetCompaniesForUserInput
* GetCompaniesForUserOutput 

Førstnevnte har 1 element under seg (UserName) mens sistnevnte må ha en liste av Companies. Da trenger du en complext type «Company» (med feltene under seg), deretter en complex type «Companies» (av typen Company, med minoccurs=0 og maxoccurs=unbounded – dette gir en «repetert liste»). Deretter gir du complex type «GetCompaniesForUserOutput» et element «Companies» av type «Companies».

Se gjerne i fasiten her.

Deretter lager du en ny web service i studio. Navngi denne «CompanyService». Legg til et endpoint (sier noe om autentiseringen og kommunikasjonen, bruk default her), og lag deretter en Operation («GetCompaniesForUser»).

På Operation «GetCompaniesForUser» velger du schema-elementene fra CompanyServiceSchema for request og response (hhv input og output elementene).

Nå som dette er satt opp kan du benytte Data Sources til å filtrere opp Companies (hvis Company.Responsible.UserName = input.UserName) og under Actions kan trenger du kun en enkel Create Objects effekt som oppretter output xml’en (hvor du mapper inn data felter fra Companies).

For å teste denne i klienten trenger du en xml-fil som input når du velger Test run -> Web Service -> CompanyService. Bruk Notepad og legg inn denne teksten og lagre fila som input.xml (bytt ut usr1a med ditt brukernanv, og sett deg selv som ansvarlig for et par selskaper først): <GetCompaniesForUser><UserName>usr1a<//UserName><//GetCompaniesForUser»

