# Studio

# Introduksjon til modellering
Første del av oppgavene vil gå ut på å modellere opp nye objektklasser. En Genus App Platform-applikasjon levert til en kunde, vil typisk støtte opp hele eller deler av kundens forretningsmodell. Eksempelvis kan en applikasjonsmodell for vikarbransjen dekke store deler av deres forretningsmodell gjennom å støtte hele saksbehandlingen, rapporteringsbehov, dokumentarkiv, kommunikasjonskanal (mail/sms), og integrasjon mot eksterne systemer. Hos noen kunder kan rapporteringsdelen ha større fokus, mens andre kunder igjen har søk i forretningsdata som hovedfokus.  

Felles for alle applikasjonsmodeller, enten dette er “full-skala” saksbehandlingsløsninger, Business Intelligence-rettede løsninger (virksomhetsstyring med rapporter og analyser som fokus), eller med tekniske integrasjonsløsninger, så har alle disse en objektmodell. 
En objektmodell er forretningsobjektene til kunden, koblet sammen. Objektmodellen tilsvarer ofte datamodellen vi ser i databasen, men denne er modellert opp («gjenspeilet») i Genus App Platform, og kan ha ytterligere logiske koblinger, tilleggsinformasjon, og til og med objektklasser som kun finnes i Genus App Platform (ikke i databasen). Fordelen med å lage objektmodellen i Genus App Platform, er at Genus App Platform da vedlikeholder koblinger, avhengigheter, primærnøkler, datakonsistens, datatyper, opprettelse, endring og sletting av data. Regler for sletting, duplikatregler, valideringsregler, automatiserte regler (tilsvarende “triggere” i databasespråket) – alt dette holdes styr på i Genus App Platform. 

Objektmodellen eksponeres mot sluttbruker gjennom oppsett av tabeller eller «Forms», kombinert med handlinger, søk m.m., gjennom Genus Desktop klienten (som du ble kjent med i oppgave 1). Utvikler setter opp objektmodell, logikken i handlinger, søk, og GUI gjennom verktøyet Genus Studio (som du nå skal bli mer kjent med).

I Genus Studio refererer vi til et objekt (feks «Company») som en «Object Class». Egenskapene til Company (som eksempelvis «Name» eller «Org No») kalles «Object Class Property» eller «Property». 
Genus CRM fasit har en enkel objektmodell beskrevet i Case-beskrivelsen (kapittelet over). Det som mangler i din EDU løsning er Contact, Contact Log, Document og Request. Første del av oppgavene i Studio blir å utvide objektmodellen med Contact & Contact Log.


![oppg1fig1.JPG](media/oppg1fig1.JPG)
*Objektmodellen for Genus CRM i initiell versjon. Diagrammet fås opp fra Studio: Velg noden “Object Class Diagram».  Her ser vi 5 Object Classes, hver med en rekke Object Class Properties. 
MERK: Et diagram er kun et tegnebrett hvor man kan visualisere et utvalg av objektene i løsningen (alle objekter som finnes er listet noden «Object Classes» i studio). Her får man automatisk opp relasjonene. Om man sletter et objekt fra diagrammet blir det kun borte fra diagrammet («tegningen») du har åpent – objektet fjernes ikke fra løsningen.*