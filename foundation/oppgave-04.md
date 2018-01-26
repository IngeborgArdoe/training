# Oppgave 4 (Stikkord: Enkel modellering av brukergrensesnitt; Tables)
Vi skal nå lage en table for utlisting av mine kontaktpersoner, og tilgjengeliggjøre denne for sluttbruker som en menysnarvei i navigasjonspanelet
1. Lag en ny Table som du kaller «Contacts».

   *Veiledning: Fra Studio -> User Interface -> Tables -> New (Basic Table)*.
   1. Under Data Sources: Legg til “Contact”. Huk bort “Private”.
   2. Layout: Her legger til hvilke rader og kolonner som skal være tilgjengelig. Dra inn Data Sourcen (fra høyre) inn i Rows, og dra inn First Name, Last Name, Company, Mobile, Mail, Responsible, State, Position, Created og Modify-feltene inn som Columns.
   3. Views: 
      *Et View er en tilpasning av Layout inkludert filtrering av data og innstillinger rundt søk etc. Det er Viewene som benyttes når en Table legges ut i navigation pane, eller når table legges inn i en Form.*
      1. General: Endre navn på Viewet til My Contacts. Under “Columns” huker du bort “Visible” på Created og Modified feltene.
      Kommentar: Dette gjør at feltene default ikke vises, men kan velges inn.
      2. Data Filters: Sett Default Filter til å være kontakter hvor Contact.Responsible = Active User Account. Sett også på sortering (First Name, Last Name).
      *Kommentar: Default filtre kan endres av bruker i klienten. Med andre ord hvis man åpner tabellen i klienten kan man feks foresta et søk og få opp Contacts hvor du ikke er responsible. Hvis man setter på et Mandatory filter vil tabellen alltid begrenses til Contacts hvor du er responsible (dette kravet legges da alltid på søket du gjør).*
      3. Search: Huk av for Enable Search, og legg til Contact under Data Sources her
      *Kommentar: Dette gjør at det blir mulig å søke i Contacts når man står i utlistingen «My Contacts» i klienten.* 
      4. Filter Pane: Huk av for «Show Filter Pane» og legg til Contact under Data Sources her.
      *Kommentar: Dette gjør at man kan se Default Filteret nederst når man åpner «My Contacts» i klienten.*
   4. Events:
      1. Legg til et Event for å åpne Formen for en Contact ved dobbeltklikk (Open in a New Window)
         *Veiledning: Merk at Command og Event er sammenslått i Tables. Effect Type = Open a Form, Effect = «Contact», Meny = «Open in New Window». I tillegg må Data Filters settes iht screenshot under:*
        ![oppg4fig1.JPG](media/oppg4fig1.JPG)
      2. Legg til event for å lage ny Contact.
      Veiledning: Name: New Contact. Symbol: # 1081. Enabled: Yes. Visibility: Yes
      Menu = «New» og Create Data settes iht screenshot under:
      ![oppg4fig2.JPG](media/oppg4fig2.JPG)
2. Lagre og lukk tabellen. Gå til Studio -> Navigation Pane. Høyreklikke på node «Companies» og legg til Shortcut til Table Contacts (View: My Contacts). Trykk Next. Endre navn her til “My Contacts” (navnet på snarveien i navigation pane slik den vises). Du kan også (valgfritt) legg på et ikon for snareveien. Trykk Finish.
3. Deploy til deg selv og verifiser at du får opp dine kontakter, samt at du får åpnet disse og opprettet ny.
4. Vi ønsker også å merke rader for Inaktive kontaktpersoner «grå». Hvis du går til Layout og velger Row «Contact» har du et valg nederst til venstre: «Automatic Formatting». Trykk på denne. Legg til en ny rule med Name =  «Inactive». Under «Foreground» velger du en gråfarge. Under «Condition» setter du Contact.State = Inactive.

Deploy igjen og test dette ved å sette en kontaktperson inaktiv i klienten.
