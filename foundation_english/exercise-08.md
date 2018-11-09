## Exercise 8 - Rules
You will now make a Rule that does the following: If a user checks the «Is Customer» field of a Company, i.e. sets it to "true, the State of that Company should be changed to "Active" (this is to simplify the usage and improve the data quality).

### Create a new Rule (from Studio -> Rules -> New)

#### General: 
Name the rule "Set Company Active when set to Customer". Select "On After Modify" in the dropdown. This is the event that will trigger the rule. 

*Comment: By selecting "On After Modify", the Rule will execute after changes have been stored in the data base.*
#### Data Sources: 
Choose «Company» as object class. Then, select «Is Customer» as property.

*Comment: The Rule will now solely run when a change is made to the «Is Customer» field (and saved). If a property isn't provided, a change to any of the object's (e.g. Company) fields would trigger the Rule. It is also possible to add other Data Sources, which are read during execution, if you want to (even if it's not relevant in this Rule) create logic against these.*

#### Actions: 
   1. You will need an outside Decision with a Condition that is valid when «Is Customer» is equal to "true" AND State is equal to "Inactive". 
      
  *Note: This is the only scenario where we need to change State to "Active".*
      
  2. Add a Modify Objects effect that changes the State to "Active".

  *Note: Remember to put it within a Commit Scope. Otherwise, the change will not be persisted.*

#### Deploy
Deploy to yourself and verify that when you set a Company (which is inactive) to "Is Customer", and save, the State is automatically changed to "Active". 

   
<table>
   <tr><td><a href="exercise-07.md"><- Previous</a></td><td align="right"><a href="exercise-09.md">Next -></a></td></tr>
</table>
