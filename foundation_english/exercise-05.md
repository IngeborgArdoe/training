#Oppgave 5 (Stikkord: Ribbon)
*SESJON FRA VEILEDER: Før oppgaven starter skal veileder ha holdt sesjon Ribbon i Genus App Platform.*

 ![oppg5fig1.JPG](media/oppg5fig1.JPG)
##Ribbon
I denne oppgaven skal vi utvide Company-form’en med Ribbon. En Ribbon forbedrer brukernes forståelse og læring av et nytt skjermbilde (Form/Table) da relevante oppgaver/actions i skjermbildet blir mer synlige.

Med en god Ribbon i en Form vil brukeren kunne se over tilgjengelige handlinger i Ribbon-en og kjappere skjønne hva skjermbildet tilbyr av funksjonalitet. Slik får brukeren en økt følelse av kontroll over applikasjonen.

**Context Tabs** (eksempel under) i Forms er egne faner i Ribbon som først dukker opp mens en e	r i en gitt kontekst.  

![oppg5fig2.JPG](media/oppg5fig2.JPG)

En kontekst kan for eksempel være at en bytter en fane i Formen og får opp tilgjengelige handlinger som er relevante for denne fanen, eller at brukeren klikker i en Grid inne i Form-en og da får opp handlinger relevante for objektene listet ut i Grid-en.

En Ribbon blir satt opp fra bunnen av for hver Form. En liten Form uten mye funksjonalitet vil derfor ha en liten Ribbon, mens en avansert og kompleks Form med vil ha en Ribbon som inneholder mye funksjonalitet.

Da er det viktig å bruke de tilpasningene Ribbon tilbyr: Gruppering av kommandoer (Sections), gode symboler og tekster for de ulike kommandoene, størrelse (stor/liten) som indikerer viktighet av kommandoen, conditional enabling, screen tips og disabled tips. 
Sist er det verdt å nevne at brukeren kan skjule Ribbon-en for at den skal ta opp mindre plass. Da er det praktisk at det finnes en Quick Access Toolbar hvor modellerer har lagt de viktigste kommandoene.

1. Utforsk ribbonmodelleringsverktøyet i Genus Studio.
   1. Åpne «Customize Ribbon» i Form Company. Gjør deg kjent med hva som finnes i nedtrekksmenyen til venstre (General Commands vs Form/View Commands) og hva som finnes i høyre nedtrekksmeny.
   I Høyre nedtrekksmeny er det for Company-formen sin del «Form Tabs», «Context Tab Groups» og «Quick Access Toolbar» som er relevant.    Kommandoene lagt i Form Tabs vil alltid være tilgjengelige såfremt de ikke har satt visibility/enabling-regler.
   2. Legg til Ribbon-kommandoer for New og Delete for Contact i Company.
      1. I venstre nedtrekksmeny: Velg All Form Commands. I høyre nedtrekksmeny velg Context Tab Groups.
      2. Høyreklikk under Context Tab Groups og velg «Add Context Tab Group». Gi denne navn (dobbeltklikk) Contact. 
      3. Høyreklikk på Contact-gruppen og velg “Add Tab”. Kall denne Tab-en for Contact Management. 
      4. Høyreklikk på Contact Management-tab-en og velg Add Tab Section. Kall denne Tab Section-en Contact. Merk: En kan fint bruke flere Tab Sections under én Tab. Eksempelvis en som heter kun Contact for New og Delete, en som heter State for statusendringer og en som heter Clipboard for copy og paste.
      5. Om du har fulgt oppskriften nøye tidligere, vil du på venstresiden nå finne en kommando med navn «New Contact». Marker Tab Section Contact og dobbeltklikk på denne kommandoen.
      6. Tilsvarende skal du kunne finne en kommando «Delete Contact». Dobbeltklikk på denne også.
      7. Deploy og test at det ser riktig ut. Om alt er gjort riktig skal det se ut som følger om du åpner Company og går til Contacts-fanen:

     ![oppg5fig3.JPG](media/oppg5fig3.JPG)
2. Legg til «Change Responsible for Company» i Quick Access Toolbar
   1. Velg Quick Access Toolbar på høyresiden i Customize Ribbon og velg inn commanden.
3. Legg til Ribbon-kommando i Contacts-tabellen for å opprette ny Contact
   1. Åpne Contacts-tabellen.
   2. Verifiser at Eventen for New Contact har navn New Contact og Tip Contact og et passende symbol (# 1081). 
   3. Legg eventen i under Main Tabs – Home -> New.
4. VALGFRITT: Utvid Ribbon i Contact-Formen med Context Tab Group for Contact Log
