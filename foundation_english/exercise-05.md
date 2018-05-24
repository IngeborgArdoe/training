## Exercise 5 - Ribbon
**SESSION BY INSTRUCTOR:** *The instructor will start off by giving you a brief introduction of the topic.*

 ![oppg5fig1.JPG](media/oppg5fig1.JPG)
### Ribbon
In this exercise, you will expand the Company-form with Ribbon-functionality. A Ribbon enhances the user's learning and understanding of a new display (i.e. Form or Table), as relevant actions/commands are made clearly visible.

With a well-defined Ribbon, the user can quickly browse through available actions and get a perception of what the form/table offers in terms of functionality. Consequently, the user gets an incresed feeling of control.
 
**Context Tabs** (see example below) in Forms are tabs that appear only in the Ribbon when the user is in a given context. 

![oppg5fig2.JPG](media/oppg5fig2.JPG)

A context can for example be a Form's tab or grid. When the user opens the tab or clicks on the grid, the defined respective Context Tab - containing only relevant actions - appears in the Ribbon.

A Ribbon is made from scratch for every Form. Accordingly, simple Forms with little functionality will have small Ribbons, while more advanced and complex Forms will have large Ribbons with lots of functionality.

To create a well-functioning Ribbon, it is important to utilize all the customization-options offered. By chosing meaningful groupings of commands (Sections), symbols, texts, sizes of icons (small/large), conditional enablings, screen tips and disabled tips, you can make the life of the user much simpler. For example, you should always try to highlight important and frequently used actions in the Ribbon. 
Finally, it is worth mentioning that the end user can hide the Ribbon if he/she wants more space for content. In that case, it is convenient to have a Quick Access Toolbar where the most important commands are included.

1. Explore the tool for modeling Ribbons in Genus Studio.
   1. Open "Customize Ribbon" in the top menu of the Company-form. Familiarize yourself with the content of the dropdown menu on the left-hand side (General Commands vs Form/View Commands). Also, check out what's available in the dropdown menu on the right. For the Company-form, the relevant items in the latter menu are «Form Tabs», «Context Tab Groups» and «Quick Access Toolbar». Commands that are added to the Form Tabs will always be available in the form, provided that there are no enabling/visibility rules set.
   2. Add Ribbon-commands for deleting and creating Contacts.
	  1. In the left dropdown menu: Select All Form Commands. In the right drowdown menu: Select Context Tab Group.
	  2. Right-click in the Context Tab Groups pane and choose Add Context Tab Group. Name it (by double-clicking) "Contact".
	  3. Right-click on the Contact-group and select Add Tab. Name it "Contact Management".
	  4. Right-click on the Contact Management-tab and choose Add Tab Section. Name it "Contact". Note: You can have several Tab Sections under one Tab. For instance, you can have one Tab Section for commands New and Delete called "Contact", one for status changes called "Status" and one for copy and paste called "Clipboard".
	  5. If you have followed the exercises carefully, you will find a command named "New Contact" on the left-hand side. Mark the Tab Section "Contact" and double-click on the command.
	  6. Equally, you should find a command named "Delete Contact". Double-click on this as well.
	  7. Deploy and check that everything looks as expected. If you have done it correctly, you should see the following when you open a Company and click the Contacts-tab:

     ![oppg5fig3.JPG](media/oppg5fig3.JPG)
2. Add "Change Resposible for Company" to the Quick Access Toolbar.
   1. Select Quick Access Toolbar in the dropdown menu on the right-hand side and add the command.
3. Add a Ribbon-command to the Contacts-table for creating a new Contact.
   1. Open the Contacts-table.
   2. Verify that the Event for making a new contact is named "New Contact". Set Tip = "Contact", and find a suitable symbol (# 1081). 
   3. Place the event under Main Tabs – Home -> New.
4. Optional: Expand Ribbon in form Contact with a Context Tab Group for Contact Log.
