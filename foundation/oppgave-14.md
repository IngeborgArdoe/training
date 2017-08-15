# Oppgave 14 - Diverse
Oppgaven er valgfri samleoppgave av diverse utvidelser for å få løsningen din enda bedre.

**VALGFRIE OPPGAVER:** 

1. Lag 2 nye views i tabellen «Activities» for «My Activities» og «My Recently Completed» som lister ut hhv aktiviteter som ikke er fullført/kansellert som jeg er ansvarlig for og aktiviteter jeg er ansvarlig for som er fullført siste 3 måneder. Legg til shortcut til view-ene i navigation pane (under Company) og rename menyen «Company» til «CRM»
  Tips: En kjapp måte å lage en nytt «nesten lik» table view er å høyreklikke på et eksisterende view og velge «Copy».

2. Lag et nytt table view i tabellen Companies for «My customers» som viser kunder hvor du er ansvarlig for Company eller hvor du er ansvarlig for en Contact. Legg til snarvei til dette view-et i navigation pane.

3. Lag en ny sikkerhetsgruppe «Key Account Managers». Legg til Super Users som medlem av denne gruppa. Gjør feltene «Is Customer», «Annual Sales» og «Annual Revenue» kun redigerbare for denne sikkerhetsgruppa men synlige for resten (Users).
Tips: Får å sette sikkerhet på gruppenivå per Object Class Property, huk av for «Allow granting of permissions for property» inne på arkfane Security på Object Class Property’ene. Deretter kan du legge til permissions i studio på disse (under Security -> Permissions).

4. Legg inn mulighet for å kunne Explore (Browse Paths på Objektklassen) til andre objekter
Company -> Activities, Contacts, Mail og Documents
Request -> Companies, Contacts, Documents og Mail
User -> Activities, Companies, Contacts, Documents, Mail, Requests

  *Tips: Dette gjør at man i klienten kan utforske relaterte data (meny «Explore») når man f.eks. velger en liste av Companies. Dette settes opp i arkfane «Explore» under «Browse Paths» på egenskaper ved en Object Class. Når det explores vil feks Contacts listes ut – men da må Genus vite hvilken Contacts-utlisting den skal benytte. Om du ser i fasitløsningen på feks egenskapene ved Company i arkfane «Explore» under «Views» er det lagt inn et table view som «default view». Det er dette som benyttes når man bruker «Explore» i klienten (enten fra Explore menyen, eller når man dobbeltklikker på et tall i en rapport for å se det bakenforliggende).*

 
