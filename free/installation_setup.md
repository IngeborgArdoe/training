
# Installation of Genus and URLs to the environments

### Installation
In case you haven't installed Genus Apps on your computer yet: Open the web browser and type https://free-**\<username\>**-origin.free.genus.net/download/Setup.exe. This will download Genus.	

### Log into your Environment
You can access your environment through the URL https://free-**\<username\>**-origin.free.genus.net/

When you log in for the first time, please select **Forgot password?**, type in your username and select **Send email**. You should receive a link to set your password soon.


### Database access
To access the database, you will need SQL Server Management Studio (SSMS). If you do not have that installed it can be downloaded here: https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms 

In the connection dialog, use the following information:

* Server name: genus-free.database.windows.net, 1433
* Authentication: SQL Server Authentication
* Login: **\<username\>** (received in e-mail)
* Password: **\<password\>** (received in e-mail)
* Options >> Connect to database: **\<username\>**_data

![installation_1.jpg](media/installation_1.jpg) 


![installation_2.jpg](media/installation_2.jpg) 
 
