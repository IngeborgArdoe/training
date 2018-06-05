




# Data Mart Part Two – Manipulate Data

#### SESSION BY INSTRUCTOR

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
#### Total amount > $200 ####
 1. Enter the *Subsets* shortcut in the navigation pane. Click the "New" icon, either in the action menu or by right clicking the main window
 2. Add a name (e.g. *Yellow Trip > $200*), and optionally a description
 3. Open *Data Filter* to edit the filter properties for this subset
		 -  add a filter for the *Yellow Trip* data source
		 - in the condition window, click *"Add"*, choose *Total amount*  as left operand, and enter 200 as a right operand
		 - the expression should read *"Yellow Trip.Total amount **is greater than** 200"*

Notice that you can add filters for many data sources per subset.

#### Tip amount > $50
Create a similar subset for taxi trips that were awarded with more than $50 tip.

#### Weekdays
Create a subset on the Weekday data source, that only includes Saturday and Sunday


### Create Calculated Fields ###
We are going to create four calculated fields in this exercise: *"Trip speed"* on the *"Yellow Trip"* data source,  and *"Average trip speed per PU Community"*,  *"Average Trip speed per PU Community, tip > $50"* and *"Total average trip speed”* on the *Community District PU* data source.
#### "Trip speed" ####
1. Enter the *Calculated Fields* shortcut in the navigation pane.
2. Right click the *Yellow Trip* data source and click "New"
 Enter a suiting name for the calculated field (*"Trip speed"*)
3. In the *Expression* window, start by typing *"yellowTrip"* followed by "*.*" and notice that data source properties appear.
4. Mathematical operators (+, -, *, /, mod, …) can be used in combination with the data source properties and numbers to express your 
5. Trip speed is defined as distance divided by duration
	- the expression should read: *yellowTrip.distance / yellowTrip.duration_Hours*

#### Average trip speed per PU Community District
Calculated fields can be accessed across data sources. We want to calculate the average trip speed per pickup community, by using the *"Trip speed"* field that we calculated in the previous step.

1. Add a new Calculated Field to the *Community District PU* data source. Name it *"Average Trip speed per PU Community"*
2. Start typing "*yellowTrip.*". Properties will appear, among them *"tripSpeed"'*. 
3. Notice the error message saying *"The expression is expected to be of type 'Real', but this expression is of type 'Bag(Real)"*. This means that the current expression returns more than one value – which we would expect, considering that we are are looking at all the trips per community
4. Add "*.*" behind the expression to render accumulation methods for the values
5. Choose *average*, and notice that the error message disappears
	- alternatively, you can choose *sum*, and divide by *count*
	- The expression should read: "*yellowTrip.tripSpeed().average()*"


#### Average trip speed per PU Community District when Tip amount > $50, using *keep*
The *keep* keyword can be used in expressions to make use of subsets. Here we want to calculate the Trip speed for Yellow Taxi Trips where the Tip amount exceeded $50.

1. Add a new calculated field to the Community District PU data source and name it *"Average Trip speed per PU Community, tip > $50"*
2. Start typing *"yellowTrips."*, this time followed by "*keep(Subsets.)*". Notice that the subsets you created appear. Choose *tipsAmount__50*
	- Now, the calculation will only consider yellow taxi trips where the tip amount exceeds $50
3. add another "*.*" to access the properties of the *Yellow Trip* object class. As in the previous step, choose *"tripSpeed"*, followed by "*.*" and *average*. 
	- The expression should read: "*yellowTrip.keep(Subsets.tipAmount__50).tripSpeed().average()*"

#### Total Average Trip speed using *ignoreContext* #####
The previous calculated fields have been contextualized: We have calculated the average speed *per* trip, and *per* community district. Sometimes we want to ignore the context, for example in order to calculate the total average trip speed (aka. "average average trip speed"). We can do this by using the *ignoreContext* keyword.

1. Add a new calculated field to the Community District PU data source and name it *"Total average trip speed"**
2. Start by typing "*yellowTrip.ignoreContext()*". 
	- The connection between the *Community District PU* data source and *Yellow Trip* is now ignored. Instead, all *Yellow Trip* objects are included in the calcuation 
	- Complete the expression by selecting the *tripSpeed* field, and choosing *average* as accumuluation method
		- The final expression should read: "*yellowTrip.ignoreContext().tripSpeed().average()*"

