# Oppgave 13 - Agenter

Oppgaven er valgfri og man må se an tiden man har til rådighet. Det anbefales uansett å lese gjennom oppgaven.

**VALGFRI OPPGAVE:** Lag en agent som sender ut epost til ansvarlige for aktiviteter der aktiviteten sin Reminder Time har passert (samt at Last Reminder Sent er mindre enn Reminder Time for å unnga spam). Agenten må også oppdatere Last Reminder Sent på aktivitetene som blir varslet.

*Veiledning: Agenten bør sende 1 epost per ansvarlige (med andre ord å iterere over Activities og sende en epost per aktivitet er en dårlig ide).*

Agenten bør ha data sources:
  * Activities (all to be reminded) med data filter “alle ikke-fullførte eller kansellerte aktiviteter som har Reminder Time < Now og hvor Last Reminder Send ikke har verdi eller er mindre enn Reminder Time.
  * Users (les opp fra Activities.Responsible)
  * Activities (temp for user), brukes i effektene for å lese aktivitetene som skal påminnes for brukeren du itererer over.
  
Agenten ha en Enumerator effekt ytterst som itererer over Users. 

For hver iterasjon skal aktivitene for brukere leses opp (i effekten kan du velge å lese «From Datasource: Activities (all to be reminded)» i tillegg til å sette data filter Activities (temp for user).Responsible = User – da leses dette opp i minnet istedenfor fra databasen, og du trenger heller ikke sette opp data filter på nytt. 

Etter at dette er lest opp, kjør en Create a Mail Message effekt hvor skriver en tekst og avsender (feks noreply@genus.nox) samt lister ut Activities med aktivitetsnummer og subject. Tips for sistnevnte: I Body på eposten høyreklikk -> Insert Repeating Section som du binder til Activities (temp for user). Da vil det genereres en liste. 

Til slutt kjører du en Modify Objects (husk Scope som commit’er) som setter Last Reminder Sent til Now.
