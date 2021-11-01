#REST (and Web) Services

While you may have noticed that some actions, for instance global ones, have effects to consume SOAP or REST services, Genus also lets you build REST Services that can allow external systems to communicate with your Genus system.

If you are unfamiliar with APIs and REST services, these are communication protocols that allow a client (or end user computer) to communicate and exchange data with another system by following a set of rules defined by the host of the data. The host of the API defines a set of resources (available data or actions) and any required input. For instance; If you have the organization number for a company, you can use it as input to request the resource "Company" for all information we have on this company. Any logic or data handling that happens at the data hosts' end is a blackbox to the computer system sending the requests for data.

We will focus on REST services, because few newer APIs are based on SOAP protocols. Genus supports creating REST resources for all the standard REST Methods; GET, PUT, POST, DELETE and PATCH (see the table below for a short description). When creating REST services, you have access to the action editor and can customize data handling etc here. You can also customize request input, headers and error handling and warnings.

By creating REST resources, you can easily communicate with external systems, allowing them to request access to, or even alter, data in your Genus solution.




## HTTP Methods


<table>
<thead>
<th>Method </th>
<th>Use Case </th>
<th>Normal Success Response </th>
</thead>
<tbody>
  <tr>
    <td>GET</td>
    <td> Read </td>
    <td>200 OK - List of elements that meet the input requirements </td>
  </tr>
  <tr>
    <td>POST</td>
    <td>Create</td>
    <td>201 Created - Returns an ID if a new instance was created </td>
  </tr>
  <tr>
    <td>PUT</td>
    <td> Update or Replace </td>
    <td>200 OK </td>
  </tr>
  <tr>
    <td>PATCH</td>
    <td> Update or Modify </td>
    <td>200 OK </td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td> Delete </td>
    <td>200 OK </td>
  </tr>
  </tbody>
</table>

<br/>
