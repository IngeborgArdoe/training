# Facility Management
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction to the topic, but this page will serve as a reference if you wish to lookup some information during the course.*


Throughout the course material, we will be working within a Property Management environment. We have a base solution in Genus, and will expand functionality and user interfaces to provide Facility Services to property tenants. Facility services typically provide tools to support property functionality, safety and infrastructure. It often includes, but is not limited to, fire safety, maintenance, cleaning services, operating cafeterias, custodial services and servicing property infrastructure.

The course environment provides a web application interface providing property tenants an overview of ongoing maintenance and services, and a very basic "backroom" application for administration of code domains, data and users.


## Starting Point

The core business entities that are already introduced in the solution are;

* **Company** representing companies tied to the solution, either through active agreements or as prospects. These companies can have different functions. <br/>
  *Service Providers* provide services on a schedule or on-demand, usually linked to agreements. <br/>
  *Service Subscribers* typically tenants that have an interest in maintenance and equipment related to the property they are leasing.
* **Agreement** representing agreements signed with Service Providers.
* **Property** representing an active or prospected property in the Property Manager's portfolio.
* **Component** representing equipment components, such as fire alarms, doors or the electrical installations.
* **Task** representing work that needs to be done on the properties, or related to customer relations.


## Expansion
We want to improve the solution by allowing tenants to submit concerns about the properties through their web application. These concerns can be followed up though tasks, if action is required from the property manager.

Concerns are reported by service subscribers, or even other representatives of the tenants eventually, and connected to their property location. Finally, we would like to enable uploading photos and support communication between the concern reporter and the property management.


<br/>
<br/>



<table>
   <tr><td><a href="installation-of-sql-server-mgmt-studio.md"><- Previous</a></td><td align="right"><a href="e1.1-genus-clients.md">Next -></a></td></tr>
</table>
