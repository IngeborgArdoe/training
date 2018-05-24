## Exercise 15 - Web Services
**SESSION BY INSTRUCTOR:** *The instructor will give you a brief introduction to the concept of Web Services, how it is set up and how to use the schema editor in Genus Apps.*

This is a fully optional exercise. As a minimum, we recommend you to read through it.

Web Services are easily set up in Genus Apps. A Web Service made in Genus Apps is available on the application server so that other applications can call on it to perform the service operations it provides. Examples can be "GetCompanies" or "CreateActivity", if we want to have an external solution that retrieves or updates data in our Genus CRM solution. A Web Service requires that we have defined the format of both input and output (XML). Accordingly, we first have to set up a schema for this using the schema editor (or we could have imported an existing one).

**OPTIONAL EXERCISE:** Create a Web Service called "GetCompaniesForUser" which takes an XML with a field "UserName" as input and returns an XML with a list of companies with fields "ID", "CompanyName", "OrgNo", "Employees", "AnnualRevenue" and "PostalAddressCity".

To verify that it works, you can use "Test run" in the client. You will have to create an XML-file (with field UserName) in advance which can be utilized as input.

Guidance: Create a Schema in the Schema editor (name it "CompanyServiceSchema"). It should have 2 elements:
* GetCompaniesForUserInput
* GetCompaniesForUserOutput 

While the former contains only 1 element (UserName), the latter must have a list of Companies. You will need a complex type "Company" (containing all the fields), and then a complex type "Companies" (of type Company, minOccurs=0 and maxOccurs=unbounded - giving a "repeated list"). Next, you will have to give the complex type "GetCompaniesForUserOutput" an element "Companies" of type Companies.

Take a look at the solution for help.

Create a new Web Service in Studio. Name it "CompanyService". Add an end point (says something about authentication and communication, use default) and create an Operation ("GetCompaniesForUser").

On Operation "GetCompaniesForUser", select schema-elements from CompanyServiceSchema for request and response (input and output, respectively).

Now that this is set up, you can use Data Sources to filter Companies (if Company.Responsible.UserName = input.UserName) and under Actions you will only need one single Create Objects effect which generates the output XML (map data fields from Companies).

To verify that it works, you will need an XML-file as input when you select Test run -> Web Service -> CompanyService. Open Notepad and add the following text to a file before you save it as "input.xml": <GetCompaniesForUser><UserName>usr1a<//UserName><//GetCompaniesForUser>. Note: Substitute "usr1a" with your username, and make sure you are the responsible of a couple of companies before you start testing.

