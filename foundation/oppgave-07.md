#Oppgave 7 (Stikkord: Enkel modellering av logikk; Rules)
Vi skal nå lage en enkel Rule som gjør følgende: Dersom man huker av «Is Customer» (til «true») på Company, skal også State på Company endres til Active (for å forenkle bruken og forbedre datakvalitet)
1. Lag en ny Rule (fra Studio -> Rules -> New)
   1. General: Denne skal hete «Set Company Active when set to Customer». Velg “On After Modify” i dropdown for å velge hvilken event som skal trigge rulen.
   *Kommentar: Dette sier når Rulen skal kjøre – med andre ord etter lagring av endringene skal denne Rulen kjøres.*
   2. Data Sources: Velg Company som object class øverst. Velg deretter  “Is Customer” som property.
   *Kommentar: Dette vil si at Rulen lytter etter endringer på objektklasse Company og felt «Is Customer». Kun etter lagring endring på feltet «Is Customer» vil denne Rulen kjøres. Man kan (selv om det ikke er relevant i denne Rulen) legge til andre Data Sources som leses opp ved kjøring av Rulen, dersom man skal lage logikk mot andre data sourcer enn Company.*
   3. Actions: 
      1. Vi må ha en Decision ytterst med Condition at «Is Customer» må være satt til True og at State er Inactive.
      *Merk: Det er kun da vi trenger å endre State til Active.*
      2. Legg deretter til en Modify Objects som endrer State til Active

      *Husk Scope rundt, ellers vil ikke endringene tre i kraft.*
   4. Deploy endringene og test dette ved å sette et selskap (som ikke er kunde fra før) til  Inactive, deretter huk av for «Is Customer». Da skal State endres etter lagring.
