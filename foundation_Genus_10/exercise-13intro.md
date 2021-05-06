## Exercise 13.1 - Introduction to Web modeling

An increasing number of applications are moving to the web browser, because of the ease of access, independence from operating systems and new user habits. Users are also increasingly demanding to access their applications using mobile devices. In this exercise, you will learn how to create a web application that can be accessed from any browser. Before we start, let's introduce some new terms. 

### Main terminology

Below is a figure of the terms used in web modeling, and the relationship between them. The terms will be further explained in the sections below.

![oppg13fig0.JPG](media/oppg13fig0.JPG)

The arrows in the figure indicates reference direction, e.g. a Group refers to an Area, which is the same as saying that one Area can have many Groups (one-to-many relationship). Thus, a double arrow line indicates that both refers to each other, constituting a many-to-many relationship.

#### App
An App is a named Sitemap, which provides access to Pages and more, to support a business process or function.

An App has fields like Name, Title and Path Segment.

The Path Segment is the last part of an App's URL, to be able to open the App directly without going through the Start Page.

A Sitemap - and thereby also an App - has a Landing Page, which is the Page that opens by default when you launch the App.

#### Sitemap
A Sitemap provides access to destinations like Pages, Analysis and URLs.

A Sitemap consists of a hierarchical structure composed of Areas, Groups and Links. Area is the topmost level, followed by Group and then Link. However, a Link does not need to be connected to a Group, thereby making Group an optional level in the Area - Group - Link hierarchy.

A Link points to an Analysis, an URL or a set of one or more Pages.

If a Link points to more than one Page, the user can choose (switch) Pages at run time. This is useful for Pages users change between quite often, instead of adding the Pages as new Links to the Sitemap (and thereby "cluttering" the Sitemap).

You will probably most often link your Links to Pages of type View, which presents data in a tabular format.

#### Page
A Page is a visual presentation of data for displaying, editing and deleting data.

A Page can be of three types, namely View, Form and Canvas.

* View: A collection of data presented in a tabular format used for presenting more than one object, but also searching among objects.
* Form: Presents data in a schematic layout typically used for presenting and editing one object (and any related objects).
* Canvas: For solving problems involving multiple object types of equal importance.
A View can be used as a default presentation of a collection of objects. A Form can be used as a default presentation of a single object (and any related objects). A Canvas cannot be used as a default presentation.

A Page can be used in more than one App. As such, it is often useful to think of an App as a collection of Pages.

A Page always belongs to a Module, and all data for View, Form and Canvas are limited to the Data Sources made available through the Page's Module (and any data restrictions on those Data Sources).

Within a Page you can determine which data the Page should operate on by specifying:

* A Public Interface: A Public Interface consists of Data Sets received from "the outside" of the Page. These Data Sets are always filled when a Page opens.
* Private Data Sets: Private Data Sets, on the other hand, are internal to the Page and not visible outside the Page.
* Private Data Sets can be of three types:

* Filtered Data: These are subsets of data from the Page's Module Data Sources and are filled when a Page opens.
* Writable Set: These are subsets containing objects and can - as the name implies - be edited during the lifetime of a Page.
* Refined Set: These are criteria based subsets of data from either Public Interface Data Sets, Filtered Data or Writeable Sets. * Refined Sets are read only and contains all objects which satisfies the given criteria at any time.
All Data Sets (whether public or private ) need to be within the data restrictions set for the Data Sources given by the Page's Module.

#### Page type View
A View presents data in a tabular format like a Table or Repeating Container.

A View also supports search and pagination. Pagination is the process of retrieving and presenting data in chunks, where each chunk continues where the previous finished.

A View has a Master Data Set which connects to a Data Source. A View can be used as a default presentation of a collection of objects for a Data Source.

#### Page type Form
A Form presents data in a schematic layout, where you can place traditional UI controls and Components rather freely.

A Form has - similar to View - a Master Data Set which connects to a Data Source. A Form can be used as a default presentation of a single object (and any related objects) for a Data Source.

Unlike a View, you can do the following inside a Form:

Specify a Viewport. A Viewport divides your Form into a grid of rows and columns.
Reuse Components. Components are assemblies of UI controls reusable across all types of Pages.

#### Page type Canvas
Both View and Form are focused on specific tasks and both optimized for handling a single Data source (through the concept of a Master Data Set). A Canvas does not have a Master Data Set, and thus cannot be used as a default presentation of an object.

Not having a single Master Data Set, makes the Canvas suitable for solving problems involving multiple object types of equal importance.

#### Component
A Component is an assembly of UI controls that can be reused in Pages within the same Module or in other Modules.

Components can be of the three same types as Page, namely Form, View or Canvas, and the meaning of these three types are similar, i.e.:

Canvas: For solving simpler or more unstructured problems than provided by View or Form.
View: A collection of data presented in a tabular format used for presenting more than one object, but also searching among objects.
Form: Presents data in a schematic layout typically used for presenting and editing one object (and any related objects).
Components - unlike Pages - cannot be used in a Sitemap (and thereby not in an App), but has to be placed inside other Pages or other Components. In such respect, Component is a concept on the same level as UI controls, which also can be placed in the content area of Pages or Components. This means that a Component can contain other Components.

A component belongs to a Module, but can be reused in other Modules, i.e. by Pages and Components in other Modules.

In summary, Component is a powerful building block in your user interface. Special-built Components rich of end user functionality can be reused in other parts of your solution, and thus reduce the need for remodelling.

#### Client Action
A Client Action is a sequence of side effects initiated by an event in the user interface, such as a click on a button. Various side effects are provided to support common tasks such as CRUD operations for objects, navigation between pages and dashboards, displaying messages and notifications, uploading and downloading files, and executing other Client- and Server Actions.

Block constructs such as decisions, for each loops, and catch exception provides functionality for conditional execution, enumeration of objects, and handling exceptions.

Within a Client Action you can determine which data the Client Action should operate on by specifying:

* A Public Interface: A Public Interface consists of Data Sets received from "the outside" of the Client Action. These Data Sets are always filled when a Client Action is invoked.
* Private Data Sets: Private Data Sets, on the other hand, are internal to the Client Action and not visible outside the Client Action.
* Private Data Sets can be of two types:

* Writable Set: These are subsets containing objects and can - as the name implies - be edited during the lifetime of a Client Action.
* Refined Set: These are criteria based subsets of data from Public Interface Data Sets or Writeable Sets. Refined Sets are read only and contains all objects which satisfies the given criteria at any time.
Server Action
As the name implies, these actions are executed on the server side. The set of side effects supported by Server Actions is a bit more powerful than the set supported by Client Actions, and some of the effects are not possible to execute on the client side.

A Server Action can be defined within a Module (Local Server Action), or as an action which can be used from anywhere in your solution (Global Server Action). Local Server Actions can access data within your module. Global Server Actions cannot, but they provide a public interface for exchanging data.

Server Actions can be executed from a Client Action using the "Run a Local Server Action" and "Run a Global Server Action". This makes it possible to share business logic in a hybrid desktop/web experience.

#### Module
Modules are a way to split the functionality of your Common App Model into separate parts. For example, in a CRM solution, you can put sales management in a different module than customer and product management. Genus Studio does not enforce any kind of module structure. It is up to you to choose how to split the functionality into different modules.

The purpose of modules is to avoid too tight coupling between parts of larger Apps, or common app models including many apps. That is, there should be low coupling between modules and high cohesion within them. Modularity also allow for larger teams of Business Engineers working together on a common app model. Well-chosen modules bring together elements of the common app model with particularly rich conceptual relationships. This high cohesion of objects with related responsibilities allows modeling and design work to concentrate within a single module.

Modules are interchangeable and can be used for assembly of apps of differing size, complexity, or function. Pages and components within a module can be defined as public or private. Public pages and components can be reused in other modules. In addition, all public pages can be reached from the sitemap within an app. In a mature common app model you will probably reuse existing modules when composing a new app.

Within a module you can define the following elements:

A Module is a named collection or boundary containing the following elements:

* Data Sources: These define a space of data that all elements within a Module are restrained to. None of the elements below can read, change or delete data outside of the Data Source space.
* Pages: A visual presentation of data for displaying, editing and deleting data.
* Components: An assembly of UI controls that can be reused in Pages or other Components.
* Client Actions A sequence of side effects initiated by an event in the user interface, and executed on the web client.
* Server Actions A sequence of side effects initiated by an event in the user interface, and executed on the server.
* Data Filters: Restrictions on data that are guaranteed to be SQL compatible at the time of definition. In a future version of Genus, it will be possible to define such filters at the place of use, effectively removing the need for explicitly named Data Filters here.
The elements above cannot exist outside a Module, i.e. all elements above must be connected to a single Module.

#### Data Source
A Data Source is a description of a type and based on or extends concepts like Object Class, XML Schema and File.

#### Data Set
A Data Set is a collection of objects based on a Data Source.

#### Data Filter
A Data Filter is a critera for restricting the selection of objects in a Data Set.