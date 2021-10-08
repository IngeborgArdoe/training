## Exercise 10 - Agents

This exercise is optional. We still recommend you to read through it.

####1. OPTIONAL: Send notification to responsible about Activity

Create an agent that sends out an e-mail to the responsible of an activity if its Reminder Time has passed (and Last Reminder Sent is less than Reminder Time - to avoid spam). The agent should also update Last Reminder Sent on the activity.

*Guidance: The agent should send 1 e-mail per responsible (i.e. it's a bad idea to iterate over Activities and send one e-mail per activity).*

The agent should have the following data sources:
  * Activities (remind), with data filter "all non-completed activities that have Reminder Time < Now and where Last Reminder Sent has no value or is less than Reminder Time".
  * Users, which you will read from Activities.Responsible
  * Activities (temp), to keep track of the activities that the user your are iterating over should be reminded about.

The agent needs an Enumerator effect that iterates over Users at the top level.

For each iteration, all activities that the user is responsible for have to be read into Activities (temp) (in the Read Objects effect, you can choose to read "From Datasource: Activities (remind)" and set the data filter to "Activities (temp).Responsible = User". This way, objects are read in memory rather than from the database, and you don't have to set up the data filter again).

After reading activities, add a "Create a Mail Message"-effect. Compose an e-mail text and a sender (e.g. noreply@genus.nox), and list Activities with activity number and subject.

*Tip: In the e-mail Body, right-click -> Insert Repeating Section. Bind it to Activities (temp). This will generate a list.*

Last but not least, add a Modify Objects effect (remember to put it in a Commit Scope) which updates property Last Reminder Sent to "Now".


<table>
   <tr><td><a href="exercise-12.md"><- Previous</a></td><td align="right"><a href="exercise-16.md">Next -></a></td></tr>
</table>
