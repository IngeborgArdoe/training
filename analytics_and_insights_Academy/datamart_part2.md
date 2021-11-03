# Data Mart Part Two – Manipulate Data

#### Session by instructor

_In this session, we will take a closer look at the data mart, and explore ways to create custom calculations that can be used readily in analysis._  

#### Agenda
- Subset
- Calculated field
    - Keep
    - IgnoreContext
    - Ignore selections
    - Ignore all selections


### Subset
Subsets are used to access only specific parts of the data source. In this case, we want to create a subset that only includes Yellow taxi trips with a cost higher than $200, and another subset for trips that were tipped for more than $50.

The effect of subsets can be compared to the effect of making selections in an analysis. An important difference is that the filtration is done in advance in the case of subsets, wheareas for an analysis the filtration is executed during runtime. To have the filtration done in advance, can be beneficial when dealing with large data sources.

### Calculated Fields ###
A calculated field is a data mart specific extension of a data source. As with formulas in an analysis, they are defined as mathematical expressions. Calculated fields are normally used when the mathematical operation needs to be performed at object level, as opposed to a formula in analysis, which operates on an aggregated level. Additionally, the calculations are done during data mart load, as opposed to formulas in analysis, which are calculated at run time.

## Exercise

### Create a subset ###
#### Cost > $6 000 ####
 1. Enter the *Subsets* shortcut in the navigation pane. Click the "New" icon, either in the action menu or by right clicking the main window
 2. Add a name (e.g. *Cost > $6 000*), and optionally a description
 3. Open *Data Filter* to edit the filter properties for this subset
		 -  add a filter for the *Task* data source
		 - in the condition window, click *"Add"*, choose *Cost*  as left operand, and enter 6 000 as a right operand
		 - the expression should read *"Task.cost **is greater than** 6 000"*

Notice that you can add filters for many data sources per subset.

#### Duration > 13 Days
Create a similar subset for taxi trips that were awarded with more than $50 tip.

#### Summer
Create a subset on the Month data source, that only includes June-August


#### Summer
Create a subset on the Day data source, that only includes Mondays


### Create Calculated Fields ###
We are going to create a calculated fields in this exercise: *"Cost per Day"* on the *"Task"* data source,  and *"Average cost/day per Category"* on the Task Category source.
#### "Cost/day" ####
1. Enter the *Calculated Fields* shortcut in the navigation pane.
2. Right click the *Tasks* data source and click "New"
 Enter a suiting name for the calculated field (*"Cost per Day"*)
3. In the *Expression* window, start by typing *"Task"* followed by "*.*" and notice that data source properties appear.
4. Mathematical operators (+, -, *, /, mod, …) can be used in combination with the data source properties and numbers to express your
5. Trip speed is defined as distance divided by duration
	- the expression should read: *Task.cost / task.daysToResolve

#### Average cost/day per Task Category
Calculated fields can be accessed across data sources. We want to calculate the average trip cost/day for specific categories, by using the *"Cost per Day"* field that we calculated in the previous step.

1. Add a new Calculated Field to the Task Category* data source. Name it *"Average Cost/Day"*
2. Start typing "*Task.*". Properties will appear, among them *"CostPerDay"'*.
3. Notice the error message saying *"The expression is expected to be of type 'Real', but this expression is of type 'Bag(Real)"*. This means that the current expression returns more than one value – which we would expect, considering that we are are looking at all the trips per community
4. Add "*.*" behind the expression to render accumulation methods for the values
5. Choose *average*, and notice that the error message disappears
	- alternatively, you can choose *sum*, and divide by *count*
	- The expression should read: "task.CostPerDay().average()*"


#### Average days to resolve


#### Average days to resolve per Task Category when cost > 6 000, using *keep*
The *keep* keyword can be used in expressions to make use of subsets. Here we want to calculate the Days to resolve tasks that cost over 6 000.

1. Add a new calculated field to the Community District PU data source and name it *"Average days to resolve, cost > 6 000"*
2. Start typing *"task."*, this time followed by "*keep(Subsets.)*". Notice that the subsets you created appear. Choose *cost_6000*
	- Now, the calculation will only consider tasks where the cost exceeds 6000
3. add another "*.*" to access the properties of the *Task* object class. As in the previous step, choose *"DaysToResolve"*, followed by "*.*" and *average*.
	- The expression should read: "*task.keep(Subsets.cost_6000).daysToResolve.average()*"

#### Total Average Trip speed using *ignoreContext* #####
The previous calculated fields have been contextualized: We have calculated the cost or time to resolve *per* task, and *per* category. Sometimes we want to ignore the context, for example in order to calculate the total average (aka. "average average trip speed"). We can do this by using the *ignoreContext* keyword.

1. Add a new calculated field to the Tak Category data source and name it *"Total average Days to Resolve"**
2. Start by typing "*task.ignoreContext()*".
	- The connection between the *Category* data source and *Task* is now ignored. Instead, all *Task* objects are included in the calcuation
	- Complete the expression by selecting the *daysToResolve* field, and choosing *average* as aggregation method
		- The final expression should read: "*task.ignoreContext().daysToResolve.average()*"
