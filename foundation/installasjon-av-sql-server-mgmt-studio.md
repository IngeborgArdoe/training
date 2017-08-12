## Installasjon av SQL Server Management Studio

For å utvikle («modellere») i Genus App Platform må man ofte lage nye tabeller og felter i databasen. Til dette trengs SQL Server Management Studio installert på egen PC.

Hvis du ikke ønsker å installere dette eller ikke har mulighet, vil det stå en PC i kurslokalet hvor du kan kjøre SQL’ene dine på (det er ikke så mange av dem), eller du kan be veileder kjøre dem for deg. Men vi anbefaler, hvis mulig, at du installerer dette på egen PC.

###Last ned siste release av SQL Server Management Studio (SSMS) 
https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms
*Etter installasjon, start SQL Server Management Studio lag en ny connection med connection string: “192.168.121.109,1458» (merk, samme connection string brukes for alle miljøer – alle databaser er samlet på samme databaseserver), som i eksempelet under:*

![installklient1.JPG](media/installklient1.JPG) 
 
Benytt «din» bruker for innlogging “eduXY” (hvor XY er nummeret på miljøet du har fått utdelt) med passord “L3arn1ng!”. Spørringene skal kjøres mot database «GenusCRM_EDUXY_Data». Dette velger du etter innlogging i boksen øverst til venstre, etter at du har trykket på «New Query»:
 
 ![installklient2.JPG](media/installklient2.JPG) 
