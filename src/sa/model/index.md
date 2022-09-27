title
Software Architecture Model
---

# Getting started

You will use [Markdown](https://www.markdownguide.org/cheat-sheetplan) and [PlantUML](https://plantuml.com/) to describe a software architecture model about your own project.

This document will grow during the semester as you sketch and refine your software architecture model.

When you are done with each task, please push so we can give you feedback about your work.

We begin by selecting a suitable project domain.

# Ex - Domain Selection

{.instructions

Submit the name and brief description (about 100 words) of your domain using the following vision statement template:

```
For [target customers]
Who [need/opportunity/problem]
The [name your project]
Is  [type of project]
That [major features, core benefits, compelling reason to buy]
Unlike [current reality or competitors]
Our Project [summarize main advantages over status quo, unique selling point]
```

Please indicate if your choice is:

* a project you have worked on in the past (by yourself or with a team)
* a project you are going to work on this semester in another lecture (which one?)
* a new project you plan to build in the future
* some existing open source project you are interested to contribute to

The chosen domain should be unique for each student.

Please be ready to give a 2 minute presentation about it (you can use a slide but it's not necessary)

Hint: to choose a meaningful project look at the rest of the modeling tasks which you are going to perform in the context of your domain.

}

**Project Name:** *TradAgg*

**Project Type:** I plan to build this web application in near future.

**Vision Statement:** Tradagg is a web application for everyone who would like to have overview about his/her portfolio in stock market. Tradagg is an aggregator for different platforms for trading in stock market.
An user can choose from many platforms such as Robinhood, Trading212, InteractiveBrokers and also from crypto platforms like Coinbase, Binance, etc.
Hence, the user has a completely view about his portfolio in time. He can also get a notification once the value of his portfolio reaches a specific amount of money.

**Additional Information:** Gratitude and credit CS50.

# Ex - Architectural Decision Records

{.instructions

Software architecture is about making design decisions that will impact the quality of the software you plan to build.

Let's practice how to describe an architectural decision. We will keep using ADRs to document architectural decisions in the rest of the model.

Use the following template to capture one or more architectural design decisions in the context of your project domain

Pass: 1 ADR

Good: 2 ADR

Exceed: >2 ADR

}

![Architectural Decision Record Template](./examples/decision-template.madr)

### ADR 1

* What did you decide?
    In order to store data (persistency tier) I need a relational database.

* What was the context for your decision?
    The web application will attract many users. Hence, we need to store the huge amount of data in a secure way.
    Relational database is perfect fit for web application.
    Therefore, the goal is to store data in relational database.

* What is the scope of your decision? Does it affect the entire architecture?
    It affects the the application and database server. User interface stays untouched.

* What is the problem you are trying to solve?
    Where can I store the data?

* Which alternative options did you consider?
    List at least 3 options:

  * Relational database
  * NoSQL database (to store unstructured/semi-structured data, e. g. MongoDB)
  * RDF Triple Stores

* Which one did you choose?
    Relational Database

* What is the main reason for that?
  #### Advantages:
  * High security
  * Multi User
  * Avoid redundancy
  * Easy access to data/Easy query
  * Data integrity
  * Flexibility - CRUD

  #### Disadvantages:
  * High physical memory/storage
  * Hight initial costs

### ADR 2

* What did you decide?
    I pick MySQL in Cloud as relational database to store data.

* What was the context for your decision?
    The web application will attract many users. Hence, we need to store the huge amount of data in relational database.
    It is necessary to choose the relational database which has a good match to Python. Therefore, my goal is to store data in a efficient way with respect to the programming language.

* What is the scope of your decision? Does it affect the entire architecture?
    It affects the application and database server. User interface stays untouched.

* What is the problem you are trying to solve?
    What kind of relational database am I going to choose?

* Which alternative options did you consider?
    List at least 3 options
  * MySQL in Cloud
  * PostgreSQL in Cloud
  * MySQL no cloud

* Which one did you choose?
    MySQL in Cloud

* What is the main reason for that?
  #### Advantages:
  * Good match with Python - Easy use to connect with Python - driver "MySQL Connector"
  * Data security
  * Scalability
  * High performance

  #### Disdvantages:
  * Impedance mismatch between object-oriented and the relational world.
  * Slower performance due to joins.

### ADR 3

* What did you decide?
    I pick Django as Framework.

* What was the context for your decision?
    We have choosen MySQL in Cloud as relational database for web application and python as programming language. MySQL can be easily connected to Python with Django web framework.

* What is the scope of your decision? Does it affect the entire architecture?
    It affects the application server. User interface stays untouched.

* What is the problem you are trying to solve?
    What framework does match to Python and MySQL?

* Which alternative options did you consider?
List at least 3 options
  * Django
  * Pyramid
  * Flask - microframework

* Which one did you choose?
    Django

* What is the main reason for that?
  #### Advantages
  * Django works well with Python and MySQL
  * Better Scalability compared to the Flask

  #### Disdvantages:
  * Monolithic architecture

### ADR 4

* What did you decide?
    I pick Python as programming language.

* What was the context for your decision?
    We have choosen MySQL as relational database for web application. Consequently, we have to choose the programming language. MySQL can be easily connected to Python with Django framework.

* What is the scope of your decision? Does it affect the entire architecture?
    It affects the application server. User interface stays untouched.

* What is the problem you are trying to solve?
    What programming language fits to our needs and experience?

* Which alternative options did you consider?
    List at least 3 options:
  * Python
  * Java
  * C++

* Which one did you choose?
    Python

* What is the main reason for that?
  #### Advantages:
  * Experience with Python, Flask and MySQL - good combination
  * Flexible - intregration with other programming languages
  * Rich standard library
  * Huge Python community

  #### Disdvantages:
  * Speed limitations

# Ex - Quality Attribute Scenario

{.instructions

1. Pick a scenario for a specific quality attribute. Describe it with natural language.

2. Refine the scenario using the following structure:

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle Environment {

[Source] -> [System] : Stimulus

[System] -> [Measure] : Response

}

@enduml
```

*Stimulus*: condition affecting the system

*Source*: entity generating the stimulus

*Environment*: context under which stimulus occurred (e.g., build, test, deployment, startup, normal operation, overload, failure, attack, change)

*Response*: observable result of the stimulus

*Measure*: benchmark or target value defining a successful response

Pass: 3 scenarios

Good: >3 scenarios

Exceed: >6 scenarios using challenging qualities

}


## Example Scenario

Quality: *Recoverability*

Scenario: In case of power failure, rebooting the system should take up to 20 seconds.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "After Power has been restored" {

rectangle "Admin" as Source
rectangle "max 20s" as Measure

Source -> [System] : "Boot"

[System] -> [Measure] : "Online"

}

@enduml
```

## 1 scenario

Quality: *Feasibility - Time to market*

Scenario: Our company makes a certain investment into software development so that the software is ready up to 5 months and can be used by users.


```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Development Time" {

rectangle "Our company" as Source
rectangle "5 months" as Measure

Source -> [Software] : "Investing into software development"

[Software] -> [Measure] : "software is ready"

}

@enduml
```

## 2 scenario

Quality: *Testability*

Scenario: Unit tester performs certain unit test on specific component of the system. Based on the unit test, unit tester will obtain result values within 3 minutes.


```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Development time" {

rectangle "Unit Tester" as Source
rectangle "3 min" as Measure

Source -> [Component of System] : "performs unit test"

[Component of System] -> [Measure] : "provide result values"

}

@enduml
```

## 3 scenario

Quality: *Usability - Learnability*

Scenario: An end user wants to learn the system features of the web application. System was designed according to the various rules of human computer interaction so that the user will learn these system features within 10 minutes.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Runtime" {

rectangle "End User" as Source
rectangle "Within 10 min" as Measure

Source -> [System] : "wants to learn system features"

[System] -> [Measure] : "support learn system features"

}

@enduml
```

## 4 scenario

Quality: *Usability - Memorability*

Scenario: An end user logs in his/her account after 3 months. Even after 3 months the user will manage to use the web application productively within 2 minutes.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Runtime" {

rectangle "User" as Source
rectangle "Within 2 min" as Measure

Source -> [System] : "Log-in after 3 months"

[System] -> [Measure] : "User uses web app productively"

}

@enduml
```

## 5 scenario

Quality: *Security - Authentication*

Scenario: An user tries to log into his account on the web application. The system authenticates the identity of the user so that the user logs in his account successufully within 2 seconds.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Runtime" {

rectangle "User" as Source
rectangle "Within 2 sec" as Measure

Source -> [System] : "Tries to log in"

[System] -> [Measure] : "logged successfully"

}

@enduml
```

## 6 scenario

Quality: *Performance - Throughput*

Scenario: An user sends a request on the web application. The request is processed by the system with latency up to 100 ms.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Normal operation mode" {

rectangle "User" as Source
rectangle "Latency up to 100 ms" as Measure

Source -> [System] : "Send request"

[System] -> [Measure] : "Request is processed"

}

@enduml
```

## 7 scenario

Quality: *Modifiability*

Scenario: Developer wants to change the GUI. Therefore, he needs to change the source code. As a result, the GUI is changed within 2 hours.

```puml
@startuml

skinparam componentStyle rectangle
skinparam monochrome true
skinparam shadowing false

rectangle "Design Time" {

rectangle "Developer" as Source
rectangle "Within 2 hours" as Measure

Source -> [Code] : "Change the GUI"

[Code] -> [Measure] : "GUI changed"

}

@enduml
```


# Ex - Quality Attribute Tradeoff

{.instructions

Pick a free combination of two qualities on the [map](https://usi365.sharepoint.com/:x:/s/MSDE-2022-SoftwareArchitecture/ESVksoXVgMNHtKBKrIwatMYBqorOFaKjxnoqssEy0gNPCg?e=81W7SI) and write your name to claim it.

Then write a short text giving an example for the tradeoff in this assignment.

Pass: 1 unique trade-off

Good: 2 trade-offs

Exceed: >2 trade-offs

}

## Portability vs. Performance (Example)

Developing an app natively for each OS is expensive and time consuming, but it benefits from a good performance. Choosing a cross-platform environment on the other hand simplify the development process, making it faster and cheaper, but it might suffer in performance.

## Complexity vs. Composability
Software can be very complex due to huge amount of connections between the components. More complex the software is, the less easy is to assemble all the components. In other words, it is difficult to have high complexity and composability.

## Complexity vs. Clarity
The complex software can loose the clarity of the software. The software with high complexity, will bring less clarity. In other words, it may be very difficult to understand the complex software.

## Time to Market vs. Usability
Management wishes to launch a software product ASAP. Due to lack of time, the software is not as designed as needed. This may cause a negative effect of usability of the product. Development department is in hurry to deliver a product and so the usability factor is omitted. In other words, it may be impossible to deliver product on the market ASAP with very high usability.

## Interoperability vs. Performance
Interoperability is great quality attribute of a software. Our software product can exchange information with various different computer systems. On the other hand, the performance of our software product decreases due to this  high degree of exchange.

# Ex - Feature Modeling

{.instructions

In the context of your chosen project domain, describe your domain using a feature model.

The feature model should be correctly visualized using the following template:

![Example Feature Model Diagram](./examples/feature.puml)

If possible, make use of all modeling constructs.

Pass: Include at least 4 non-trivial features

Good: Include at least 6 non-trivial features, which are all implemented by your project

Exceed: Include more than 8 non-trivial features, indicate which are found in your project and which belong to one competitor

}

![Feature Model Diagram for trading aggregator](./examples/feature.fml)
 

# Ex - Context Diagram

{.instructions

Prepare a context diagram to define the design boundary for your project.

Here is a PlantUML/C4 example to get started.

![Example Context Diagram](./examples/context.puml)

Make sure to include all possible user personas and external dependencies you may need.

Pass: 1 User and 1 Dependency

Good: >1 User and >1 Dependency

Exceed: >1 User and >1 Dependency, with both incoming and outgoing dependencies

}

```puml
@startuml
!include <C4/C4_Container>

Person(user, "Users")

System_Boundary(boundary, "Trading Aggregator") {

}

System_Ext(trading_platform, "Trading platforms")
System_Ext(graph, "Graph Visualization")
System_Ext(database, "MySQL in Cloud")


Rel(user, boundary, "Requests/Responds")
Rel(boundary, user, "Requests/Responds")

Rel(boundary, trading_platform, "Request", "Stock, Price")
Rel(trading_platform, boundary, "Respond", "Stock, Price")

Rel(boundary, graph, "Request", "Data")
Rel(graph, boundary, "Respond", "Data")

Rel(boundary, database, "CRUD", "Data")
Rel(database, boundary, "Respond", "Data")
@enduml
```

# Ex - Component Model: Top-Down

{.instructions

Within the context of your project domain, represent a model of your modular software architecture decomposed into components.

The number of components in your logical view should be between 6 and 9:

* At least one component should be further decomposed into sub components
* At least one component should already exist. You should plan how to reuse it, by locating it in some software repository and including in your model the exact link to its specification and its price.
* At least one component should be stateful.

The logical view should represent provide/require dependencies that are consistent with the interactions represented in the process view.

The process view should illustrate how the proposed decomposition is used to satisfy the main use case given by your domain model.

You can add additional process views showing how other use cases can be satisfied by the same set of components.

This assignment will focus on modularity-related decisions, we will worry about deployment and the container view later.

Here is a PlantUML example logical view and process view.

```puml
@startuml
skinparam componentStyle rectangle

!include <tupadr3/font-awesome/database>

title Example Logical View
interface " " as MPI
interface " " as SRI
interface " " as CDI
interface " " as PSI
[Customer Database <$database{scale=0.33}>] as CDB 
[Music Player] as MP
[User Interface] as UI
[Payment Service] as PS
[Songs Repository] as SR
MP - MPI
CDI - CDB
SRI -- SR
PSI -- PS
MPI )- UI
UI --( SRI
UI -( CDI
MP --( SRI
CDB --( PSI


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

```puml
@startuml
title Example Process View

participant "User Interface" as UI
participant "Music Player" as MP
participant "Songs Repository" as SR
participant "Customer Database" as CDB
participant "Payment Service" as PS

UI -> SR: Browse Songs
UI -> CDB: Buy Song
CDB -> PS: Charge Customer
UI -> MP: Play Song
MP -> SR: Get Music

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

Hint: How to connect sub-components to other external components? Use this pattern.

```puml
@startuml
component C {
   component S
   component S2
   S -(0- S2
}
interface I
S - I

component C2
I )- C2

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

Pass: 6 components (1 decomposed), 1 use case/process view

Good: 6 components (1 decomposed), 2 use case/process view

Exceed: >6 components (>1 decomposed) and >2 use case/process view

}

## Logical View

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI
interface " " as GVI
interface " " as TPI
interface " " as DBI
interface " " as CCI
interface " " as NI

component "Database <$database{scale=0.33}>" as DB 
component "Trading Aggregator" as TA
component "User Interface" as UI {
    component "Search bar for stock" as AS
    component "Portfolio selection" as VP
    component "Change currency" as CHC
    component "Price alert" as PC
}
component "Graph visualization" as GV
component "Trading platforms" as TP
component "Exchange rate" as ER
component "Notification" as NOT {
    component "Gmail" as GM
    component "WhatsApp" as WA
}



NI -- NOT
TA --( NI
CCI -- ER
TA --( CCI
TA - TAI
GV - GVI
GVI )- TA
TPI -- TP
TAI )- UI
DBI -- DB
TA --( DBI
TA --( TPI

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## Updated Process Views

Use Case: **Add Stock into portfolio**

```puml
@startuml
title "Add Stock into portfolio" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Trading platforms" as TP
participant "Database" as DB

UI -> TA: Search Stock
TA -> TP: Get Stock

alt request positive accepted
TP -> TA: ok
TA -> DB: Store it
TA -> UI: Stock added

else error message
TP -> TA: request failed
TA -> UI: Inform about error message

end

@enduml
```


Use Case: **Visualize portfolio in pie chart**

```puml
@startuml
title "Visualize portfolio in pie chart" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Graph visualization" as GV
participant "Database" as DB

UI -> TA: Select portfolio
TA -> GV: Get portfolio
GV -> TA: What stocks, prices and date
TA -> DB: Choose stocks with prices and date
DB -> TA: Provided information
TA -> GV: Get portfolio
GV -> TA: Provide graph
TA -> UI: Visualize portfolio

@enduml
```


Use Case: **Update prices**

```puml
@startuml
title "Update prices" Process View

participant "Trading Aggregator" as TA
participant "Trading platforms" as TP
participant "Database" as DB

-> TA: every 5 minutes
TA -> TP: Request actual prices
TP -> TA: Prices updated
TA -> DB: Actual prices stored

@enduml
```


Use Case: **Visualize portfolio in EUR**

```puml
@startuml
title "Convert portfolio from USD to EUR" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Graph visualization" as GV
participant "Database" as DB
participant "Currency converter" as CC


UI -> TA: Select EUR
TA -> GV: Get EUR
GV -> TA: What are prices and dates
TA -> DB: Choose prices with dates
DB -> TA: Provided prices with dates
TA -> CC: Convert prices to EUR based on dates
CC -> TA: Prices are converted
TA -> UI: Visualize portfolio in EUR

@enduml
```

# Ex - Component Model: Bottom-Up

{.instructions

Within the context of your project domain, represent a model of your modular software architecture decomposed into components.

To design this model you should attempt to buy and reuse as many components as possible.

In addition to the logical and process views, you should give a precise list to all sources and prices of the components you have selected to be reused.

Write an ADR to document your component selection process (indicating which alternatives were considered).

Pass: Existing design with at least 1 reused components (1 Logical View, 1 Process View)

Good: Existing design with at least 3 reused components (1 Logical View, 1 Process View, 1 ADR)

Exceed: Redesign based on >3 reused components (1 Logical View, >1 Process View, >1 ADR)

}

## Reused components which are free to use:
* 1) Plotly as Python Open Source Graph Library
    * https://plotly.com/python-api-reference/
* 2) Exchangerate.host for exchange & crypto rates
    * https://exchangerate.host/#/#docs
* 3) MySQL as free open source database
    * https://dev.mysql.com/doc/connector-python/en/
* 4) Gmail API
    * https://developers.google.com/gmail/api/reference/rest
* 5) Trading platforms based on OAuth2, e. g.:
    * Coinbase https://developers.coinbase.com/api/v2
    * Binance https://developers.binance.com/docs/login/web-integration
    * Interactive Brokers https://www.interactivebrokers.com/webtradingapi


## Reused components which are charged and thas why I excluded this component:
* 1) WhatsApp API
    * https://www.whatsapp.com/business/api
    * 90 USD / month


### 1) ADR for Graph visualization

* What did you decide?
    Plotly as Python Open Source Graph Library

* What is the problem you are trying to solve?
    How can be data visualized in GUI?

* Which alternative options did you consider?
    List at least 3 options:

  * mpld3 - Python library
  * Bokeh - Python library
  * Plotly - Python library

* Which one did you choose?
    Plotly

* What is the main reason for that?
  #### Advantages:
  * No fees
  * Experience
  * Extensive range for chart types (for future plans)


### 2) ADR for Exchange rate

* What did you decide?
    Exchangerate.host for exchange & crypto rates

* What is the problem you are trying to solve?
    How can be converted the currency?

* Which alternative options did you consider?
    List at least 3 options:

  * www.exchangerate.host
  * www.exchangerate-api.com
  * www.openexchangerates.org

* Which one did you choose?
    Exchangerate.host

* What is the main reason for that?
  #### Advantages:
  * Free
  * Python friendly


### 3) ADR for Database

* What did you decide?
    MySQL as free open source database

* What is the problem you are trying to solve?
    Where can I store the data?

* Which alternative options did you consider?
    List at least 3 options
  * MySQL in Cloud
  * PostgreSQL in Cloud
  * MySQL no cloud

* Which one did you choose?
    MySQL in Cloud

  #### Advantages:
  * Free open source
  * Good match with Python - Easy use to connect with Python - driver "MySQL Connector"
  * Data security
  * Scalability
  * High performance

  #### Disdvantages:
  * Impedance mismatch between object-oriented and the relational world.
  * Slower performance due to joins.


  ## Updated Logical View

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI


component "User Interface" as UI
component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    component "Graph visualization" as GV
    component "Database <$database{scale=0.33}>" as DB 
    component "Exchange rate" as ER
    component "Gmail" as GM
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        component "Binance API" as BAPI
        component "Interactive Brokers API" as IBAPI
    }
    TA -(0- GV
    TA -(0- DB
    TA -(0- TP
    TA -(0- ER
    TA -(0- GM

    Note bottom of DB
        Method signatures
        cursor.execute(adjusted_data)
        cursor.fetchall()
    end note

    Note bottom of TP
        Method signatures
        GET https://api.coinbase.com/v2/accounts/:account_id
        200 OK
    end note

    Note bottom of GV
        Method signatures
        px.pie(data)
        fig.show()
    end note

    Note top of ER
        Method signatures
        request.get(url)
        response.json()
    end note

}


UI --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## Updated Process Views

Use Case: **Add crypto from Coinbase into portfolio**

```puml
@startuml
title "Add crypto from Coinbase into portfolio" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Trading platforms" as TP
participant "Database" as DB

UI -> TA: Add crypto
TA -> TP: GET https://api.coinbase.com/v2/accounts/:account_id

alt request positive accepted
TP -> TA: 200 OK
TA -> TA: Adjust data
TA -> DB: cursor.execute(adjusted_data)
TA -> UI: Stock added

else error message
TP -> TA: request failed
TA -> UI: Inform about error message

end

@enduml
```


Use Case: **Visualize portfolio in pie chart**

```puml
@startuml
title "Visualize portfolio in pie chart" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Database" as DB
participant "Graph visualization" as GV


UI -> TA: Select portfolio
TA -> DB: cursor.execute(sql_query)
DB -> TA: cursor.fetchall()
TA -> GV: px.pie(data)
GV -> TA: fig.show()
TA -> UI: provide pie chart

@enduml
```

Use Case: **Visualize portfolio in EUR**

```puml
@startuml
title "Convert portfolio from USD to EUR" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Database" as DB
participant "Exchange rate" as ER
participant "Graph visualization" as GV


UI -> TA: Select EUR
TA -> DB: cursor.execute(sql_query)
DB -> TA: cursor.fetchall()
TA -> ER: request.get(url)
ER -> TA: response.json()
TA -> TA: convert prices
TA -> GV: px.pie(data)
GV -> TA: fig.show()
TA -> UI: provide pie chart

@enduml
```

Use Case: **Update prices**

```puml
@startuml
title "Update prices" Process View

participant "Trading Aggregator" as TA
participant "Trading platforms" as TP
participant "Database" as DB

-> TA: every 5 minutes
TA -> TP: Request actual prices
TP -> TA: Prices updated
TA -> DB: Actual prices stored

@enduml
```


# Ex - Interface/API Specification

{.instructions

In this iteration, we will detail your previous model to specify the provided interface of all components based on their interactions found in your existing process views.

1. choose whether to use the top down or bottom up model. If you specify the interfaces of the bottom up model, your interface descriptions should match what the components you reuse already offer.

2. decide which interface elements are operations, properties, or events.

Get started with one of these PlantUML templates, or you can come up with your own notation to describe the interfaces, as long as it includes all the necessary details.

The first template describes separately the provided/required interfaces of each component.

![Separate Required/Provided Interfaces](./examples/interface1.puml)

The second template annotates the logical view with the interface descriptions: less redundant, but needs the logical dependencies to be modeled to show which are the required interfaces.

![Shared Interfaces](./examples/interface2.puml)

Pass: define interfaces of all outer-level components

Good: Define interfaces of all outer-level components. Does your architecture publish a Web API? If not, extend it so that it does.

Exceed: Also, document the Web API using the OpenAPI language. You can use the [OpenAPI-to-Tree](http://api-ace.inf.usi.ch/openapi-to-tree/) tool to visualize the structure of your OpenAPI description.

}


```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail" as GM
    interface " " as GMI


    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI
            note bottom of CAPII
            operation:
            ..
            GET https://www.coinbase.com/oauth/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=https://tradagg.com&state=SECURE_RANDOM&scope=wallet:accounts:read
            GET https://example.com/oauth/callback?code=4c666b5c0c0d9d3140f2e0776cbe245f3143011d82b7a2c2a590cc7e20b79ae8&state=134ef5504a94
            POST https://api.coinbase.com/oauth/token
            GET https://api.coinbase.com/v2/accounts
            end note
        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
            note top of BAPII
            operation:
            ..
            GET https://accounts.binance.com/en/oauth/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=https://tradagg.com&state=CSRF_TOKEN&scope=SCOPES
            GET https://domain.com/oauth/callback?code=cf6941ae8918b6a008f1377f36a4557ab5935b36&state=377f36a4557ab5935b36
            POST https://accounts.binance.com/oauth/token?client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET&grant_type=authorization_code&code=STEP3_CODE&redirect_uri=YOUR_REDIRECT_URI
            GET https://accounts.binance.com/oauth-api/user-info?access_token=xxx
            end note     
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
            note bottom of IBAPII
            operation:
            ..
            POST https://www.interactivebrokers.com/tradingapi/v1/oauth/request_token
            POST https://www.interactivebrokers.com/tradingapi/v1/oauth/access_token
            GET https://www.interactivebrokers.com/tradingapi/v1/accounts/{account}/positions
            end note
    }
    interface " " as TPI
    
    TA --( GVI
    GVI -- GV

    note bottom of GVI
    operations:
    ..
    plotly.express.line(data_frame)
    plotly.express.pie(data_frame)
    show()
    end note

    TA --( SCHI
    SCHI -- SCH
    note bottom of SCHI
    operations:
    ..
    schedule.every().day.at("22:00").do(get_current_portfolio)
    schedule.every().day.at("16:00").do(get_current_portfolio)
    --
    events:
    ..
    Time Event
    end note


    TA --( DBI
    DBI -- DB
    note top of DBI
    operations:
    ..
    mysql.connector.connect(user, password, host, database_name)
    cursor()
    cursor.execute()
    commit()
    close()
    --
    events:
    ..
    AFTER UPDATE TRIGGER
    end note
    
    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER
    note top of ERI
    operations:
    ..
    requests.get('https://api.exchangerate.host/latest')
    response.json()
    end note


    TA --( GMI
    GMI -- GM
    note bottom of GMI
    operation:
    ..
    Credentials.from_authorized_user_file()
    build()
    MIMEText()
    base64.urlsafe_b64encode(message.as_string())
    service.users().messages().send(userId=user_id, body=message).execute()
    POST https://gmail.googleapis.com/gmail/v1/users/{userId}/messages/send
    end note
}


API --( TAI 
TAI -- TA

note top of TAI
operations:
..
register(username, password)
login(username, password)
change_password(password)
authentication()
autorization()
add_crypto_platform(platform_name)
add_stock_platform(platform_name)
delete_crypto_platform(platform_name)
delete_stock_platform(platform_name)
get_portfolio()
provide_pie_chart()
provide_line_chart(timeframe)
select_currency_eur()
select_currency_usd()
set_price_alert(price)
set_notification_for_price_alert()
subscribe_for_news_from_markets()
store_email(email)
end note


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

Web API
link: http://api-ace.inf.usi.ch/openapi-to-tree/

![alt text](./api.JPG)


# Ex - Connector View

{.instructions

Extend your existing models introducing the connector view

For every pair of connected components (logical view), pick the most suitable connector. Existing components can play the role of connector, or new connectors may need to be introduced.

Make sure that the interactions shown in the process views reflect the primitives of the selected connector

Pass: model existing connectors based on previous model decisions

Good: model existing connectors based on previous model decisions, write an ADR about the choice of one connector

Exceed: introduce a new type of connector and update your existing process view
(sequence diagram) to show the connector primitives in action

}

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## Original connector view
![Example Connector View Diagram](./examples/connector-view-original.c5)

### ADR

* What did you decide?
    * Web connector between Trading Agregator and Trading Platforms

* What is the problem you are trying to solve?
    * Trading Agregator has to pull the stocks/cryptos and prices from Trading Platforms.

* Which alternative options did you consider?
    List at least 3 options
    * Remote Procedure Call
    * Message Bus
    * Web

* Which one did you choose?
    * Web

  #### Advantages:
    * GET, but also PUT in case of Gmail
    * Immediate response compared to Message Bus - different use

  #### Disdvantages:
    * Limited amount of pull actions within 1 day for some platforms

## Updated connector view - message bus
![Example Connector View Diagram](./examples/connector-view-updated.c5)



## Process view - User subscribes for news from markets
```puml
@startuml
title "Subscribe for news from markets" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Bus" as BUS
participant "Trading platforms" as TP

UI -> TA: subscribe_for_news_from_markets()
TA -> BUS: subscribe
TP -> BUS: publish
BUS -> TA: notify
TA -> UI: provide news

@enduml
```


# Ex - Adapters and Coupling

{.instructions

1. Highlight the connectors (or components) in your existing bottom-up design playing the role of adapter. (We suggest to use the bottom-up design since when dealing with externally sourced components, their interfaces can be a source of mismatches).
2. Which kind of mismatch** are they solving?
3. Introduce a wrapper in your architecture to hide one of the previously highlighted adapters
4. Where would standard interfaces play a role in your architecture? Which standards could be relevant in your domain?
5. Explain how one or more pairs of components are coupled according to different coupling facets
6. Provide more details on how each adapter solves the mismatches identified using pseudo-code or the actual code
7. How can you improve your architectural model to minimize coupling between components? (Include a revised logical/connector view with your solution)

Pass: 1-5 (with one adapter)

Good: 1-6 (with at least two adapters)

Exceed: 1-7 (with at least two adapters)

** If you do not find any mismatch in your existing design we suggest to introduce one artificially.

## Hints

* (1) Should we find cases where two components cannot communicate (and are doing it wrongly) and highlight they would need an adapter?, or cases where we have already a "component playing the role of adapter in the view" and highlight only the adapter?

  *Both are fine. We assumed that if you draw a dependency (or a connector) the interfaces match, but if you detect that the components that should communicate cannot communicate then of course introduce an adapter to solve the mismatch*

* (2) Please show the details about the two interfaces which do not match (e.g., names of parameters, object structures) so that it becomes clear why an adapter is needed and what the adapter should do to bridge the mismatch

* (5-6) These questions are about the implications on coupling based on the decisions you documented in the connector view.
Whenever you have a connector you couple together the components and different connectors will have different forms of coupling

  For example, if you use calls everywhere, do you really need them everywhere? is there some pair of components where you could use a message queue instead?

  Regarding the coupling facets mentioned in question 5. You do not have to answer all questions related to "discovery", "session", "binding", "interaction", "timing", "interface" and "platform" (p.441, Coupling Facets). Just the ones that you think are relevant for your design and by answering them you can get ideas on how to do question 6.

}

## 1. Highlight the connector and components as adapter

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "PostgreSQL Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    [<<adapter>> psycopg2] as PADAPTER #Orange
    interface " " as PADAPTERI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI

    [<<adapter>> Web API] as AADAPTER #Orange
    interface " " as AADAPTERI

    TA -( AADAPTERI
    AADAPTERI - AADAPTER
    AADAPTER -( TPI
    TPI - TP
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( PADAPTERI
    PADAPTERI -- PADAPTER
    PADAPTER --( DBI
    DBI -- DB

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome false
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## 2. Which kind of mismatch are they solving?

### PostgreSQL database not compatible with Python
In order to create a mismatch in my logical view, I replaced mySQL database with PostgreSQL. PostgreSQL is a perfect match for Java. However, I code in Python. Hence, it is necessary to introduce an Adapter the psycopg2, which is a database adapter. This adapter enables to connect to the PostgreSQL database server in Python using the psycopg2.


### Bridge - Web API Adapter
Web API is a kind of bridge between the external component (Trading platforms) and the Trading Aggregator (controller). Tradding Aggregator sends a HTTP request to Web API and Web API forwards it to the Trading platforms. Then the Trading platforms send a HTTP response to the Web API and the Web API forwards it to the Tradding Aggregator.

## 3. Wrapper
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "PostgreSQL wrapper" as PW #Orange {
        component "PostgreSQL Database <$database{scale=0.33}>" as DB
        interface " " as DBI
        [<<adapter>> psycopg2] as PADAPTER
    }
    interface " " as PADAPTERI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading Platforms wrapper" as TPW #Orange {
        component "Trading platforms" as TP {
            component "Coinbase API" as CAPI
            interface " " as CAPII
            CAPII - CAPI

            component "Binance API" as BAPI
            interface " " as BAPII
            BAPI - BAPII
    
            component "Interactive Brokers API" as IBAPI
            interface " " as IBAPII
            IBAPII - IBAPI
        }
        interface " " as TPI

        [<<adapter>> Web API] as AADAPTER
    }

    interface " " as AADAPTERI

    TA -( AADAPTERI
    AADAPTERI - AADAPTER
    AADAPTER -( TPI
    TPI - TP
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( PADAPTERI
    PADAPTERI -- PADAPTER
    PADAPTER --( DBI
    DBI -- DB

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome false
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## 4. Where would standard interfaces play a role in your architecture? Which standards could be relevant in your domain?

### Where and which standards?
* Exchange rate
    * Represantation format - Plain text - Json file
    * Operations - HTTP Method GET
    * Protocols - HTTP
    * Addressing - URL - "https://api.exchangerate.host/latest"

* Trading platforms - Coinbase
    * Representation format - Plain text - Json file
    * Operations - HTTP Methods GET and POST
    * Protocols - HTTP
    * Addressing - "https://api.coinbase.com/v2/accounts"

* Gmail Handler
    * Representation format - MIMEText(), base64.urlsafe_b64encode(message.as_string())
    * Operations - HTTP Method POST
    * Protocols - HTTP
    * Addressing - "https://gmail.googleapis.com/gmail/v1/users/{userId}/messages/send"

## 5. Explain how one or more pairs of components are coupled according to different coupling facets

### User Interface and Trading Aggregator

* Timing
    * User Interface and Trading Aggregator must be available at the same time because it is synchronous call.

* Interaction
    * User Interface is directly connected to the Trading Aggregator.


### Trading Aggregator and Trading platforms

* Timing
    * Both components have to be available at the same time to get portfolio of an user.

* Discovery and binding
    * User interface provides to the Trading Aggregator the Trading Platforms which should be added to his user's account.
    Thus, the Trading Aggregator finds the Trading platforms component BEFORE running time. Hence, Binding is static.

{.feedback

Very interesting. Is the trading aggregator googling for the best trading platforms and following the search engine's result links to the dynamically discovered Trading platforms? :-)

Just a question to provoke a discussion on when the discovery of what takes place.

Same comment applies to the aggregator-fx rate binding.

}

### Trading Aggregator and Exchange Rate

* Discovery and binding
    * Trading Aggregator finds the Exchange Rate component BEFORE running time thanks to the URL which is provided by business entity. By business entity is meant a person or a group of persons in our start-up that makes a decision what Exchange Rate Platform will be used. Hence, Binding is static.

### Trading Aggregator App and Trading Platforms

* Platform
    * If any trading platform changes the programming language, my app will not be affected because I access data over HTTP/JSON - loose coupling.

{.feedback

Why? If you access your data sources over HTTP/JSON, do you really care if they do not support Python?

}

## 6. Adapter solves the mismatch using code or pseudocode


{.feedback

The code is a bit verbose, please highlight or add comments to point to the essential part where the adaptation takes place.

}

#### psycopg2 database Adapter
    pip install psycopg2

    # Import psycopg2 Adapter
    import psycopg2

#### #Establish connection thanks to the Adapter
connection = psycopg2.connect(database="postgres", user='postgres', password='646hkh?kjbk', host='127.0.0.1', port= '5432')

    # Create cursor
    cursor = connection.cursor()

    # Create a database
    cursor.execute('''CREATE database tradagg''')

    # Create users table
    sql_create_table_users ='''CREATE TABLE USERS(
    USERNAME CHAR(20) PRIMARY KEY,
    PASSWORD CHAR(50),
    FIRST_NAME VARCHAR(20),
    LAST_NAME VARCHAR(20),
    PORTFOLIO_NUMBER INT REFERENCES PORTFOLIO(PORTFOLIO_NUMBER) NOT NULL,
    )'''
    cursor.execute(sql_create_table_users)

    # INSERT data into users table
    cursor.execute('''INSERT INTO USERS(USERNAME, PASSWORD, FIRST_NAME, LAST_NAME, PORTFOLIO_NUMBER) VALUES ('tmshts', 'fsfs4979fdasi98798798', 'Tomas', 'Hatas', 1)''')

    # Commit changes in database
    connection.commit()

    # Close the connection
    connection.close()


#### Web API Adapter

    # 1. step Register a new OAuth2 application under https://www.coinbase.com/sign-in

    # Data received after registering my app

    my_id_coinbase = '1532c63424622b6e9c4654e7f97ed40194a1547e114ca1c682f44283f39dfa49'

    my_client_secret_coinbase = '3a21f08c585df35c14c0c43b832640b29a3a3a18e5c54d5401f08c87c8be0b20'

    # 2. step Integrate my app with Coinbase

    ## 1. Redirect users to request Coinbase access

    import requests

    my_uri = 'https://www.tradagg.com'

    my_state_coinbase = '134ef5504a94'

    pload = {
        'response_type': code,
        'client_id': my_id_coinbase, 'redirect_uri': my_uri,
        'state': my_state_coinbase,
        'scope': wallet:user:read wallet:accounts:read
        }

#### #Access to Coinbase thanks to the web API Adapter
authorization_request = requests.get('https://www.coinbase.com/oauth/authorize/get', params=pload)

    ## 2. Coinbase redirects back to your site with temporary code

    # GET https://tradagg.com/oauth/callback?code=4c666b5c0c0d9d3140f2e0776cbe245f3143011d82b7a2c2a590cc7e20b79ae8&state=134ef5504a94

    from urllib.parse import urlparse
    from urllib.parse import parse_qs

    url = 'https://tradagg.com/oauth/callback?code=4c666b5c0c0d9d3140f2e0776cbe245f3143011d82b7a2c2a590cc7e20b79ae8&state=134ef5504a94'
    parsed_url = urlparse(url)
    temporary_code_value = parse_qs(parsed_url.query)['code'][0]

    ## 3. Exchange temporary code for an access token

    dataload = {
        'grant_type': authorization_code,
        'code': temporary_code_value,
        'client_id': my_id_coinbase,
        'client_secret': my_client_secret_coinbase,
        'redirect_uri': my_uri
    }

#### #Get access token thanks to the web API Adapter
access_token_data = requests.post('https://api.coinbase.com/oauth/token/post', data=dataload)

    # Valid Access Token as response

    '''
    {
    "access_token": "6915ab99857fec1e6f2f6c078583756d0c09d7207750baea28dfbc3d4b0f2cb80",
    "token_type": "bearer",
    "expires_in": 7200,
    "refresh_token": "73a3431906de603504c1e8437709b0f47d07bed11981fe61b522278a81a9232b7",
    "scope": "wallet:user:read wallet:accounts:read"
    }
    '''

    # extract access_token and token_type from json file

    import json as js

    json_load = js.loads(access_token_data)

    access_token_value = ''
    token_type_value = ''

    for i in json_load:
        if i == 'access_token':
            access_token_value = json_load[i]
        if i == 'token_type':
            token_type_value = json_load[i]

    # 4. API Call
    authorization_data = {
        token_type_value,
        access_token_value
    }

#### #Get user data thanks to the web API Adapter
user_data = requests.get('https://api.coinbase.com/v2/user/authorization', params=authorization_data)

    # Json file response
    '''
    {
        "data":
        {
        "id": "9da7a204-544e-5fd1-9a12-61176c5d4cd8",
        "name": "Peter Smith",
        "username": "pertersmith88",
        "profile_location": null,
        "profile_bio": null,
        "profile_url": "https://coinbase.com/pertersmith88",
        "avatar_url": "https://images.coinbase.com/avatar?h=vR%2FY8igBoPwuwGren5JMwvDNGpURAY%2F0nRIOgH%2FY2Qh%2BQ6nomR3qusA%2Bh6o2%0Af9rH&s=128",
        "resource": "user",
        "resource_path": "/v2/user"
        }
    }
    '''

    json_load = js.loads(user_data)


## 7. How can you improve your architectural model to minimize coupling between components? (Include a revised logical/connector view with your solution)

### Connector view
![Example Connector View Diagram](./examples/connector-view-updated.c5)

I am not aware of the fact that I can improve my architectural model to minimize coupling between components for the reasons:

* Remote Procedure Call (synchronous call) between User Interface and Trading Agreggator must remain as User Interface is blocked until the call is responded.

* Message bus between Trading Platforms and Trading Aggregator must remain because of subscription for news - less coupled than in case of Remote Procedure Call which is great - ASYNC AVAILABILITY

* Web API between Trading Aggregator and Gmail Handler, Exchange Rate and Trading Platforms must remain because of HTTP requests.

* Asynchronous call between Trading Aggregator and Schedule and Graph visualization since Trading Aggregator can not be blocked for the time waiting for response. Less coupled than in case of Remote Procedure Call.



# Ex - Physical and Deployment Views

{.instructions

a. Extend your architectural model with the following viewpoints:

1. Physical or Container View

2. Deployment View

Your model should be non-trivial: include more than one physical device/virtual container (or both). Be ready to discuss which connectors are found at the device/container boundaries.

b. Write an ADR about which deployment strategy you plan to adopt. The alternatives to be considered are: big bang, blue/green, shadow, pilot, gradual phase-in, canary, A/B testing.

c. (Optional) Prepare a demo of a basic continuous integration and delivery pipeline for your architectural documentation so that you can obtain a single, integrated PDF with all the viewpoints you have modeled so far.

For example:

* configure a GitHub webhook to be called whenever you push changes to your documentation
* setup a GitHub action (or similar) to build and publish your documentation on a website

Pass: 1 physical view, 1 deployment view, 1 ADR (b.)

Good: >1 physical view, >1 deployment view, 1 ADR (b.)

Exceed: 1 physical view, 1 deployment view, 1 ADR (b.) + 1 demo (c.)

}

## a.

### 1. Physical view

#### 1. version

```puml
@startuml
node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
    }
}

node "<<device>> :Web Server" as webnode{
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
}

node "<<device>> :Exchange Rate Server" as exchangenode{
}

node "<<device>> :Gmail Server" as gmailnode{
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
    }
    node "<<device>> :Coinbase Server" {
    }
    node "<<device>> :Interactive Brokers Server" {
    }
}

node "<<device>> :Schedule Server" as schedulenode{
}

node "<<device>> :Graph Visualization Server" as graphnode{
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode --- graphnode : <<internet>>

appnode --- schedulenode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<HTTPS>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome false
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### 2. version

```puml
@startuml
node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
    }
}

node "<<device>> :Web Server" as webnode{
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
}

node "<<device>> :Exchange Rate Server" as exchangenode{
}

node "<<device>> :Gmail Server" as gmailnode{
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
    }
    node "<<device>> :Coinbase Server" {
    }
    node "<<device>> :Interactive Brokers Server" {
    }
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<HTTPS>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome false
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

### 2. Deployment view

#### 1. version

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    component "User Interface" as UI
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

node "<<device>> :Schedule Server" as schedulenode{
    component "Schedule" as SCH
}

node "<<device>> :Graph Visualization Server" as graphnode{
    component "Graph visualization" as GV
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode --- graphnode : <<internet>>

appnode --- schedulenode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<HTTPS>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### 2. version

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    component "User Interface" as UI
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<HTTPS>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## b. ADR

* What did you decide?
    * In order to launch the product on the market I need a deployment strategy.

* What was the context for your decision?
    * The point is that we do not have any version on the market. In other words, we launch our first version of TradAgg on the market.
    Our goal is not to make bad reputation for the entire market. Therefore, we only want to touch a market with few users (friends, acquaintances, fake profiles, etc.) for a limited time. Thus, we will get a feedback from the users and consequently we can make some changes in our software.
    After making some changes, we use the Gradual Phase-In on real users. In this case, we can check the feedback from users and if everything goes according to a plan, we can bring more users, and so on.

* What is the scope of your decision? Does it affect the entire architecture?
    * If some issue appears, it may affect the entire backend or frotend depending on the scope of issue.

* What is the problem you are trying to solve?
    * The best strategy how to deploy my TradAgg application.

* Which alternative options did you consider?
    List at least 3 options:

  * Pilot
  * Gradual Phase-in
  * Canary

* Which one did you choose?
    * Pilot

* What is the main reason for that?
  #### Advantages:
  * Meticulousness - double-check
  * Avoid bad reputation
  * Quick feedback from fake users
  * Real users untouched
  * Time to work on buggs

  #### Disadvantages:
  * Longer time to launch a product for real users


## c. demo
it should work now 4th attempt:)

# Ex - Availability and Services

{.instructions

The goal of this week is to plan how to deliver your software as a service with high availability.

1. If necessary, change your deployment design so that your software is hosted on a server (which could be running as a Cloud VM). Your SaaS architecture should show how your SaaS can be remotely accessed from a client such as a Web browser, or a mobile app
2. Sketch your software as a service pricing model (optional)
3. How would you define the availability requirements in your project domain? For example, what would be your expectation for the duration of planned/unplanned downtimes or the longest response time tolerated by your clients?
4. Which strategy do you adopt to monitor your service's availability? Extend your architecture with a watchdog or a heartbeat monitor and motivate your choice with an ADR.
5. What happens when a stateless component goes down? model a sequence diagram to show what needs to happen to recover one of your critical stateless components
6. How do you plan to recover stateful components? write an ADR about your choice of replication strategy and whether you prefer consistency vs. availability. Also, consider whether event sourcing would help in your context.
7. How do you plan to avoid cascading failures? Be ready to discuss how the connectors (modeled in your connector view) impact the reliability of your architecture.
8. How did you mitigate the impact of your external dependencies being not available? (if applicable)

Pass: 1, 3, 4, one of:  5, 6, 7, 8

Good: 1, 2, 3, 4, two of:  5, 6, 7, 8

Exceed: 1, 2, 3, 4, 5, 6, 7, 8

}


## 1. deployment design so that your software is hosted on a server (which could be running as a Cloud VM). Your SaaS architecture should show how your SaaS can be remotely accessed from a client such as a Web browser, or a mobile app

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>


cloud "Amazon Web Services (AWS)" {
    node "<<executionenvironment>> :PythonVM" as appnode {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}


node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

appnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<network VPC>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

* You are right. Trading Aggregator communicates with Gmail server via gmail protocols IMAP and POP: https://support.google.com/a/answer/9003945?hl=en

```
Are you sure that Gmail server interact with your server using HTTP(S) protocol? Maybe it uses the IMAP/POP3 
```

## 2. Service pricing model

```puml
@startuml
skinparam titleFontSize 22
title
  Pricing model
  |=            |= Starter   |= Professional    |= Expert   |
  | Price/month | Free      | 5 USD            | 10 USD   |
  | Number of platforms | 2 | 4 | unlimited |
  | Number of stocks/cryptocurrencies | 5 | 15 | unlimited |
end title
@enduml
```

## 3. How would you define the availability requirements in your project domain? For example, what would be your expectation for the duration of planned/unplanned downtimes or the longest response time tolerated by your clients?

### Availability
Since we pull the actual prices from the trading platforms 2x a day (4 pm and 10 pm), the availability of our TradAgg app must be available at these hours. The reason is if the user set a price alert for a certain amount, the price will alert at these hours as we pull up-to-date prices and consequently the user will get a notification via email.

In other words, the Trading Aggregator, Trading platforms, MySQL database, Gmail Handler and Schedule components must be available at these hours.
If the Trading Aggregator or Trading Platforms are not available at these hours, the Trading Aggregator component will pull the prices once the Trading platforms are available. Consequently, if a set price is reached, the Gmail handler will notify an user soon or later.
At other hours, the Trading Aggregator, Graph visualization, MySQL database and Exchange Rate components must be available since an user would like to visualize his/her portfolio. If the Graph visualization or Exchange Rate are not available, the user will get a message that it is not possible to visualize a graph at this moment.
In terms of setting a price alert, if MySQL database is not available, the user will get a message that it is not possible to set a price alert at this moment.
In terms of adding stocks/cryptos, if the Trading platforms are not available, the user will get a message that the Trading Platform is not available at this moment.

### Downtimes
The planned downtimes for maintenance should not be at 4 PM and 10 PM. At other hours are not desirable either :) Anyway, it is necessary to inform a client about these planned downtimes in advance.

The unplanned downtimes are unpredictable. The crucial hours are at 4 PM and 10 PM. For another hours are unplanned downtimes undesirable either. If the services are not available, the user will be informed.

We may expect not many users using the TradAgg App at the beginning of our journey. Consequently, we assume that we will not have the remote procedure calls from users all the minutes/seconds. Hence, the downtimes can be tolerated if the users do not use the TradAgg App.

The duration of downtimes if the user wishes to use the TradAgg App has to be minimal.

### Response time
Longest response time tolerated by users can be up to 3 sec since the users are patient/tolerant. In fact, an user has not very high expectation related to response time as he can use just a few calls. An user will rather use this TradAgg app in a relaxed/calm time and not in rush time.

## 4. Which strategy do you adopt to monitor your service's availability? Extend your architecture with a watchdog or a heartbeat monitor and motivate your choice with an ADR.


### Monitor Strategy: Watchdog

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>


cloud "Amazon Web Services (AWS)" {
    node "<<executionenvironment>> :PythonVM" as appnode {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}


node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

node "<<executionenvironment>> :PythonVM" as watchnode{
    component "Watchdog" as WATCH
}


appnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

TA -- watchnode : <<HTTPS>>

watchnode -- platformsnode : <<HTTPS>>

gmailnode -- watchnode : <<HTTPS>>

watchnode -- exchangenode: <<HTTPS>>

watchnode -- dbservernode : <<HTTPS>>

appnode -- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<network VPC>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

### ADR

* What did you decide?
    * Watchdog. We will check the availability of our services periodically by sending a kind of remote procedure call.

* What was the context for your decision?
    * We have to monitor the availability of the services we use. Since the TradAgg is an aggregator, we aggregate many external Trading platforms. Moreover, there are more external services we use in the TradAgg app, such as MySQL, Exchange rate and Gmail.


* You are right, MySQL is not counted as external service. It is our internal component. As a matter of fact, that is the reason, why I did not include MySQL in the task 8 related to the external dependencies.

```
Is the MySQL server an external or an internal component?
```
* What is the scope of your decision? Does it affect the entire architecture?
    * As our application relies on many external services, it affects the entire architecture.

* What is the problem you are trying to solve?
    * To monitor availability.

* Which alternative options did you consider?
    * Watchdog
    * Heartbeat

* Which one did you choose?
    * Watchdog

* What is the main reason for that?
    * There are some issue with the subscription to the heartbeat channel from some trading platforms. Therefore, we have only one option how to monitor the availability of the Trading platforms.
    * We also use a watchdog for MySQL database, Exchange Rate and Gmail as we are not sure whether we can manage to run properly the heartbeat due to the lack of IT skills.

## 5. What happens when a stateless component goes down? model a sequence diagram to show what needs to happen to recover one of your critical stateless components

Exchange rate has had 99.99 % average uptime during last 12 months. In other words, Exchange Rate is very reliable. Hence, we do not expect any downtime. However, if it occurs we use retry strategy how to recover from temporary failure.

We could also add Circuit Breaker so that an user gets a faster response about a failure if an user selects EUR in a while again.

Note: Any timeout is a matter of business rule which can be discussed/modified during time.


```puml
@startuml
title "Exchange Rate goes down" Process View

participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Database" as DA
participant "Exchange rate" as ER
participant "Graph Visualization" as GV

UI -> TA: select EUR
TA -> DA: cursor.execute(sql_query)
DA -> TA: cursor.fetchall()
TA -> ER: request.get(URL)
TA -> TA: timeout 1.3 sec
TA -> ER: retry
TA -> TA: timeout 1.3 sec
TA -> ER: retry

alt response 200 OK during timeout
ER -> TA: response.json()
TA -> TA: convert prices
TA -> GV: px.pie(data)
GV -> TA: fig.show()
TA -> UI: provide pie chart

else no response during timeout
TA -> UI: Inform about unavailability

end

@enduml
```

## 6. How do you plan to recover stateful components? write an ADR about your choice of replication strategy and whether you prefer consistency vs. availability. Also, consider whether event sourcing would help in your context.

### ADR

* What did you decide?
    * Synchronous replication of our database preferring strong consistency over availability.

* What was the context for your decision?
    * In case of loosing data, it is a big problem for our reputation and business in general. Clients may not sue us for loosing data because they can check their portfolio on the Trading platforms separately. But they definitely will not use our TradAgg app anymore. Therefore, we have to have a back-up.
    We assume that our clients are time tolerant. We are meticulous and hence we can not afford any inconsistent data in case the original database crashes or partition between original database and back-up database.

* What is the problem you are trying to solve?
    * How to replicate the database in order to have strong consistency.

* Which alternative options did you consider?
    * Synchronous replication
    * Asynchronous replication

* Which one did you choose?
    * Synchronous replication

* What is the main reason for that?
    * We can not take a risk with asynchronous replication which can provide NOT up-to-date data to an user.
    Writing to back-up can take a while and a client prefers wait for the current result rather than checking old data.
    * In case of partition between original and back-up database, client must wait in order to get up-to-date data.
    * In both above cases, we inform a client by providing a message of the explanation.
    * Our motto: "Consistency is a key."

* Event Sourcing would not be helpful in our context.

## 7. How do you plan to avoid cascading failures? Be ready to discuss how the connectors (modeled in your connector view) impact the reliability of your architecture.

### Connector View Diagram
![Example Connector View Diagram](./examples/connector-view-original.c5)


## Cascading failures

* The Trading Aggregator component is a controller, which controls all the flow and logic behind the TradAgg App. From the graph you can see that the Trading Aggregator component requests something from 1 component and get a response. After that the Trading Aggregator component edits it and transmit it to another component. Therefore, the cascading failures can not happen and thus no need of canary call.

## Reliability

* As you can see from the connector view, Trading Aggregator component uses mostly API for Gmail Handler, Exchange Rate and Trading Platforms. In terms of availability, our strategy is to keep retrying until a reasonable timeout which is about 3 seconds. If Trading Aggregator does not get any response during the timeout, he will inform an user about the current unavailability.
* "We are sorry. At this moment we can not connect to your Trading Platform. We are working on it so that you are able to add your stocks ASAP. Please try it later."


## 8. How did you mitigate the impact of your external dependencies being not available? (if applicable)

### External Dependencies:
* Trading Platforms
* Exchange Rate
* Gmail Handler

### How to mitiage in case external dependencies are not available:
* Trading Platforms - we have no other option to select any alternative if an user has stocks/cryptos in the specific Trading Platform. Hence, we keep retrying for 3 seconds. If there is no response after timeout, we notify an user and he should try later.

* Exchange Rate - we do not suppose that this Exchange Rate would have any downtime because of 99.9 % availability in the last 12 months. However, in case of downtime, we keep retrying for 3 seconds (timeout is a matter of our business rule which can be modified). If there is still no response after 3 seconds, we can use another External Dependency like Exchange Rate. Our requirement would be that the alternative has mainly free service as well.

* Gmail Handler - we could also have another email with different provider, such as Yahoo. In case of downtime of Gmail, we could use Yahoo as External Dependency. The prices are updated at 4 PM and 10 PM and then eventually a notification email is sent to an user in case of price alert. If the Gmail is not available, we just keep retrying for 1 hour (this timeout is a matter of business rule which can be discussed/modified). If there is still no response after 1 hour, we could use our alternative Yahoo. According to Fabio, another option would be a message queue. Once the Gmail is available again, the messages will be pushed to the Gmail server.


* Circuit Breaker could be helpful because we could decrease response time. Once Trading Aggregator calls Circuit Breaker and then call the External Dependency, a failure may occur. Hence, External Dependency does not response. After timeout Circuit Breaker report the failure to the Trading Aggregator. Circuit Breaker remembers the failure. If Trading Aggregator calls the External Dependency later, Circuit Breaker remembers the failture and thus respond the failure faster.


```puml
@startuml
title "Trading Platform goes down" Process View

participant "Trading Aggregator" as TA
participant "Circuit Breaker" as CB
participant "Trading Platform" as TP

TA -> CB: call
CB -> TP: call
destroy TP
CB -> CB: timeout
CB -> TA: longer response - Trading Platform failed
TA -> CB: call
CB -> TA: faster response - Trading Platform failed

@enduml
```

```
Do you plan to use polling for checking the external dependencies or a circuit breaker can help you?
```


# Ex - Scalability

{.instructions

Now that your architecture delivers your software as a service, let's redesign it so that it can scale!

1. Pick one scalability dimension: number of clients, size of input, size of state, number of dependencies

2. How well does your architecture scale along the chosen dimension? Where do you expect the bottleneck to be?

3. Modify your architecture to remove the scalability bottleneck you have identified (show both logical, process and deployment view) - consider whether the API/interface of the bottleneck component should be improved.

4. Write an ADR regarding the scalability pattern you have introduced.

5. Write an ADR regarding the issue of component discovery, choosing one of the alternatives: dependency injection vs. directory. Can you identify an existing component playing the role of directory/dependency injection container? Could you give an example of where you would need to add such component to facilitate dynamic component discovery?

Pass: 1, 2, 3, 5

Good: 1, 2, 3, 4, 5

Exceed: 1, 2, 3, 4, 5 then redo 1, 2, 3 for different scalability dimensions

}


## 1. scalability dimension
### 1. Number of clients

### 2. How well does your architecture scale along the chosen dimension? Where do you expect the bottleneck to be?
We would be happy to face to the huge amount of users. This is a nice problem :)
Bottleneck would be, definitely, the controller. But I can not forward the traffic to the "different" worker. Then I have to live with that in my architecture.
However, I depend on external services which can be overloaded by many requests and hence they are bottlenecks. These external services are Graph Visualization, Exchange Rate and Gmail Handler.
Therefore, I should also use alternatives for these external dependencies.
The schedule is an event-driven external component and is "called" just 2x a day and is independent of amount of requests.
There is no option to use alternatives for the Trading Platforms as there is only 1 Coinbase or only 1 Interactive Brokers.

### 3. Modify your architecture to remove the scalability bottleneck you have identified (show both logical, process and deployment view) - consider whether the API/interface of the bottleneck component should be improved.


#### Logical view before Load Balancing

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Logical view with Load Balancing

* Strategy for Load Balancing is First Available

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization Default" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate Default" as ER
    interface " " as ERI

    component "Gmail Handler Default" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI

    component "Load Balancer for Graph Visualization" as LBGV
    interface " " as LBGVI

    component "Directory for Graph Visualization" as DGV
    interface " " as DGVI

    LBGV --( DGVI
    DGVI -- DGV

    TA --( LBGVI
    LBGVI -- LBGV

    LBGV --( GVI
    GVI -- GV

    component "Graph visualization A1" as GVA1
    interface " " as GVA1I

    LBGV --( GVA1I
    GVA1I -- GVA1

    component "Graph visualization A2" as GVA2
    interface " " as GVA2I

    LBGV --( GVA2I
    GVA2I -- GVA2

    component "Load Balancer for Email" as LBGM
    interface " " as LBGMI

    component "Directory for Email" as DGM
    interface " " as DGMI

    TA --( LBGMI
    LBGMI -- LBGM

    LBGM --( DGMI
    DGMI -- DGM

    LBGM --( GMI
    GMI -- GM

    component "Yahoo Handler A1" as GMA1
    interface " " as GMA1I

    LBGM --( GMA1I
    GMA1I -- GMA1

    component "Email Handler A2" as GMA2
    interface " " as GMA2I

    LBGM --( GMA2I
    GMA2I -- GMA2

    component "Load Balancer for Exchange Rate" as LBER
    interface " " as LBERI

    component "Directory for Exchange Rate" as DER
    interface " " as DERI

    TA --( LBERI
    LBERI -- LBER

    LBER --( DERI
    DERI -- DER

    LBER --( ERI
    ERI -- ER

    component "Exchange Rate A1" as ERA1
    interface " " as ERA1I

    LBER --( ERA1I
    ERA1I -- ERA1

    component "Exchange Rate A2" as ERA2
    interface " " as ERA2I

    LBER --( ERA2I
    ERA2I -- ERA2

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP
}

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Process view before Load Balancing
```puml
@startuml
title "Many requests before Load Balancing" Process View

participant "Trading Aggregator" as TA
participant "Exchange Rate Default" as ERD


TA -> ERD: first request
TA -> ERD: second request
TA -> ERD: third request
ERD -> TA: response of first request
ERD -> TA: response of second request
ERD -> TA: response of third request

@enduml
```

#### Process view with Load Balancing
```puml
@startuml
title "Many requests with Load Balancing" Process View

participant "Trading Aggregator" as TA
participant "Load Balancer for Email" as LB
participant "Directory for Exchange Rate" as D
participant "Exchange Rate Default" as ERD
participant "Exchange Rate A1" as ERA1
participant "Exchange Rate A2" as ERA2

TA -> LB: first request
LB -> D: lookup first request
D -> LB: select first available
LB -> ERD: forward first request
TA -> LB: second request
LB -> D: lookup second request
D -> LB: select first available
LB -> ERA1: forward second request
ERD -> TA: response of first request
TA -> LB: third request
LB -> D: lookup third request
ERA1 -> TA: response of second request
D -> LB: select first available
LB -> ERD: forward third request
ERD -> TA: response of third request

@enduml
```


#### Deployment view before Load Balancing
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    component "User Interface" as UI
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Deployment view with Load Balancing
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    component "User Interface" as UI
    node "<<executionenvironment>> :Browser" {
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate Default" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler Default" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

node "Balancer for Gmail" as emailbalancer{
    component "Load Balancer for Emails" as LBE
    component "Directory for Emails" as DE
}

LBE - DE

appnode --- emailbalancer

node "Balancer for Exchange Rate" as exchangebalancer{
    component "Load Balancer for Exchange Rate" as LBER
    component "Directory for Exchange Rate" as DER
}

LBER - DER

appnode -- exchangebalancer

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

emailbalancer --- gmailnode : <<IMAP>>

node "<<device>> :Yahoo Server A1" as yahoonode{
    component "Yahoo Handler A1" as YHA1
}

node "<<device>> :Email Server A2" as emailnode{
    component "Email Handler A2" as EHA2
}

emailbalancer -- yahoonode: <<IMAP>>

emailbalancer -- emailnode: <<IMAP>>

exchangebalancer -- exchangenode : <<HTTPS>>

node "<<device>> :Exchange Rate A1" as exchangea1node{
    component "Exchange Rate A1" as ERA1
}

node "<<device>> :Exchange Rate A2" as exchangea2node{
    component "Exchange Rate A2" as ERA2
}

exchangebalancer -- exchangea1node : <<HTTPS>>

exchangebalancer -- exchangea2node : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

### 4. ADR for Load Balancer and Directory

* What did you decide?
    * Load Balancer and Directory
    
* What was the context for your decision?
    * To use Load Balancer and Directory in case that my default component is overloaded by many requests.
    In other words, in case of unavailability of my default component, the directory should use the first available component strategy. Consequently, the Load Balancer should forward the request to this component.
    The Stateless variant for Load Balancing is used because every request goes to any external component which is available. However, if the default component is available, the request goes there.
    Since we are dependent on external components, we can not force them to register in our Directory :) Therefore, we have to hard code them in our Directory. There is no Registry step between external components and Directory.

* What is the problem you are trying to solve?
    * Default components are overloaded. Hence the request must be forwarded to alternative external components.

* Which alternative options did you consider?
    * Load Balancing
    * Master/Worker - not possible to divide the requests -> no merge result needed
    * Scatter/Gather - same request sent to different components

* Which one did you choose?
    * Load Balancing

* What is the main reason for that?
    * explained above


### 5. ADR for dependency injection vs. directory

* What did you decide?
    * Using Directory for discovering the external components.
    
* What was the context for your decision?
    * Before Load Balancer can forward the request to the first available component, Directory must find out this component actively. We are looking up the external active component. 
    Since we are dependent on external components, we can not force them to register in our Directory :) Therefore, we have to hard code them in our Directory. There is no Registry step between external components and Directory.

* What is the problem you are trying to solve?
    * How to discover the external component.

* Which alternative options did you consider?
    * Dependency injection
    * Directory

* Which one did you choose?
    * Directory

* What is the main reason for that?
    * We want to control what component we can select and we call - Not following the Hollywood principle: "Don't call us, we'll call you."
    * Our motto: "We need you now, so we call you, now."


## 2. scalability dimension
### 1. Size of state

### 2. How well does your architecture scale along the chosen dimension? Where do you expect the bottleneck to be?
One database can reach full capacity in case of increase in number of users. In other words, it can be our bottleneck.

### 3. Modify your architecture to remove the scalability bottleneck you have identified (show both logical, process and deployment view) - consider whether the API/interface of the bottleneck component should be improved.


#### Logical view before Sharding

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Logical view with Sharding


```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database Switzerland <$database{scale=0.33}>" as DB
    interface " " as DBI

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
    
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }
    interface " " as TPI
    
    component "Query Router" as QR
    interface " " as QRI

    TA --( QRI
    QRI -- QR

    QR --( DBI
    DBI -- DB

    component "Database Germany <$database{scale=0.33}>" as DBG
    interface " " as DBGI

    QR --( DBGI
    DBGI -- DBG

    component "Database Austria <$database{scale=0.33}>" as DBA
    interface " " as DBAI

    QR --( DBAI
    DBAI -- DBA

    component "Shared Database <$database{scale=0.33}>" as DBS
    interface " " as DBSI

    component "Directory for Shard Key" as DforS
    interface " " as DforSI

    QR --( DforSI
    DforSI -- DforS

    DBG --( DforSI
    DBA --( DforSI
    DB --( DforSI



    QR --( DBSI
    DBSI -- DBS  

    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH
   
    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM
}

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Process view before Sharding
```puml
@startuml
title "Size of state before Sharding" Process View

participant "Trading Aggregator" as TA
participant "Database" as D


TA -> D: first query
D -> TA: response of first query
TA -> D: second query
D -> TA: response of second query
TA -> D: third query
D -> TA: response of third query

@enduml
```

#### Process view with Sharding
```puml
@startuml
title "Size of state with Sharding" Process View

participant "Trading Aggregator" as TA
participant "Query Router" as QR
participant "Directory for Shards" as DforS
participant "Database Germany" as DG
participant "Database Switzerland" as DS
participant "Database Austria" as DA
participant "Database Shared" as DSH

DG -> DforS: register
DS -> DforS: register
DA -> DforS: register
TA -> QR: first query
QR -> DforS: lookup shard key
DforS -> QR: shard key based on country provided
QR -> DS: first query
QR -> DSH: first query
DS -> QR: response of first query
DSH -> QR: response of first query
QR -> TA: provide result
TA -> QR: second query
QR -> DforS: lookup shard key
DforS -> QR: shard key based on country provided
QR -> DA: second query
QR -> DSH: second query
DA -> QR: response of second query
DSH -> QR: response of second query
QR -> TA: provide result
TA -> QR: third query
QR -> DforS: lookup shard key
DforS -> QR: shard key based on country provided
QR -> DG: third query
QR -> DSH: third query
DG -> QR: response of third query
DSH -> QR: response of third query
QR -> TA: provide result

@enduml
```

#### Deployment view before Sharding
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Deployment view with Sharding
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

node "<<device>> :Application Server" as appnode {
    node "<<executionenvironment>> :PythonVM" {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

cloud "Amazon Web Services (AWS)"{
    node "Sharding" as shardnode{
        component "Query Router" as QR
        component "Directory for shards" as DforS
    }

    component "MySQL Database Switzerland<$database{scale=0.33}>" as DS
    component "MySQL Database Austria<$database{scale=0.33}>" as DA
    component "MySQL Database Germany <$database{scale=0.33}>" as DG
    component "MySQL Database Shared <$database{scale=0.33}>" as DSH
}

QR - DforS

shardnode -- DS
shardnode -- DSH
shardnode -- DA
shardnode -- DG

appnode -- shardnode


node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

### 4. ADR for Sharding and Directory

* What did you decide?
    * Sharding the data based on the country with Directory which is responsible for providing the appropriate shard key.
    
* What was the context for your decision?
    * To use Sharding and Directory in case that capacity of my single MySQL Database is full.
    In other words, a query will be sent to appropriate database based on the shard key. Shard key will be provided by Directory for Shards which is based on countries. After the Query Router knows the shard key, the query is sent to the country database.

* What is the problem you are trying to solve?
    * My single MySQL database reaches the capacity. Hence, I need more capacity. The question is how can I go beyond my current capacity.

* Which alternative options did you consider?
    * Sharding

* Which one did you choose?
    * Sharding

* What is the main reason for that?
    * explained above


### 5. ADR for dependency injection vs. directory

* What did you decide?
    * Using Directory for providing the country shard key.
    
* What was the context for your decision?
    * Before Query Router can send a query to the appropriate database, Directory must find out the shard key based on the counry actively. We are looking up the country shard key.

* What is the problem you are trying to solve?
    * How to discover the country shard key.

* Which alternative options did you consider?
    * Dependency injection
    * Directory

* Which one did you choose?
    * Directory

* What is the main reason for that?
    * We want to control what database we can select and we send a query - Not following the Hollywood principle: "Don't call us, we'll call you."
    * Our motto: "We need you now, so we call you, now."


# Ex - Flexibility

{.instructions

Only dead software stops changing. You just received a message from your customer, they have an idea. Is your architecture ready for it?

1. Pick a new use case scenario. Precisely, what exactly do you need to change of your existing architecture so that it can be supported? Model the updated logical/process/deployment views.

2. Pick another use case scenario so that it can be supported without any major architectural change (i.e., while you cannot add new components, it is possible to extend the interface of existing ones or introduce new dependencies). Illustrate with a process view, how your previous design can satisfy the new requirement.

3. Change impact. One of your externally sourced component/Web service API has announced it will introduce a breaking change. What is the impact of such change? How can you control and limit the impact of such change? Update your logical view

4. Open up your architecture so that it can be extended with plugins by its end-users. Where would be a good extension point? Update your logical view and give at least one example of what a plugin would actually do.

5. Assuming you have a centralized deployment with all stateful components storing their state in the same database, propose a strategy to split the monolith into at least two different microservices. Model the new logical/deployment view as well as the interfaces of each microservice you introduce.

Pass: 1, one out of 2-5.

Good: 1, two out of 2-5.

Exceed: 1-5.

}

## 1. Pick a new use case scenario. Precisely, what exactly do you need to change of your existing architecture so that it can be supported? Model the updated logical/process/deployment views.
## 1. Use case - Logical / Process / Deployment view
Client wishes to give users a new feature to the TradAgg app which is Bloomberg news.
Solution: Bloomberg news API based on REST architecture with request format: JSON.
On the user interface would be seen a tab named Bloomberg News where will be listed the daily news.

### Logical view with Bloomberg News

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI
   
    interface " " as TPI

    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP
}


component "Bloomberg News" as BN
interface " " as BNI

component "Trading platforms" as TP {
    component "Coinbase API" as CAPI
    interface " " as CAPII
    CAPII - CAPI

    component "Binance API" as BAPI
    interface " " as BAPII
    BAPI - BAPII

    component "Interactive Brokers API" as IBAPI
    interface " " as IBAPII
    IBAPII - IBAPI
}

component "Exchange rate" as ER
interface " " as ERI

component "Gmail Handler" as GM
interface " " as GMI

TA --( ERI
ERI -- ER

TA --( GMI
GMI -- GM

BNI )- TA
BN - BNI

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```
{.feedback

    Is the "Bloomberg News" a backend sub-component or an external one?

}

External component

## Process view with Bloomberg News
```puml
@startuml
title "Reading Bloomberg News" Process View

participant "User" as U
participant "User Interface" as UI
participant "Trading Aggregator" as TA
participant "Bus" as BUS
participant "Bloomberg News" as BN

TA -> BUS: subscribe
BN -> BUS: publish
BUS -> TA: notify
TA -> UI: provide news
U -> UI: read news


@enduml
```

#### Deployment view with Bloomberg News
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

cloud "Cloud"{
        node "<<executionenvironment>> :PythonVM" as appnode {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}

node "<<device>> :Bloomberg Server" as bloombergnode{
    component "Bloomberg News" as BN
}

bloombergnode - appnode : <<HTTPS>>

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## 2. Pick another use case scenario so that it can be supported without any major architectural change (i.e., while you cannot add new components, it is possible to extend the interface of existing ones or introduce new dependencies). Illustrate with a process view, how your previous design can satisfy the new requirement.

User is able to export the data of his wished timeframe in CSV format. Therefore, we have to add a new component that is responsible for transforming data into CSV format. Later, we use this component as extensible component where a client can plugin component.
After exporting the data in CSV file, a client can analyze his portfolio into more depth.

## 2. Use case - export the data in csv format - Process view

```puml
@startuml
title "Exporting data in CSV file" Process View

participant "User Desktop" as UD
participant "User Interface" as UI
participant "Export Converter (default CSV)" as EC
participant "Trading Aggregator" as TA
participant "Database" as D

UI -> TA: select_timeframe()
TA -> TA: prepare_sql_query()
TA -> D: cursor.execute(sql_query)
D -> TA: cursor.fetchall()
TA -> EC: send_data()
EC -> EC: convert_data()
EC -> TA: forward_data()
TA -> UI: data_provided_in_CSV_format()
UI -> UD: data_exported_in_CSV_file

@enduml
```

## 3. Change impact. One of your externally sourced component/Web service API has announced it will introduce a breaking change. What is the impact of such change? How can you control and limit the impact of such change? Update your logical view

Breaking change of one of our external component will no big impact on our software architecture. The only thing which we have to change is the code in Trading Aggregator. Other components should not be affected. This is a great news that a change of one external component will only affect our one component - controller. We will have enough time to modify the source code based on the change of the external component.

In case of change of request format - JSON in Trading platforms, we can not change for another Trading platform. Hence, we would have to use adapter.

If Schedule does not support Python anymore, we could look up for an alternative external component supporting Python or use Adapter.

In terms of Graph visualization, plotly is library in Python. In case of some dramatical change, we would consider to look up another graph provider.

In case of change of request format - JSON in Exchange rate, we would choose another free external component supporting json format or use adapter.

In case of some dramatical change in Gmail, we would consider to look up another email provider.


### Logical view

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    interface " " as TPI

    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
}

component "Exchange rate" as ER
interface " " as ERI

component "Gmail Handler" as GM
interface " " as GMI

component "Bloomberg News" as BN
interface " " as BNI

component "Trading platforms" as TP {
    component "Coinbase API" as CAPI
    interface " " as CAPII
    CAPII - CAPI

    component "Binance API" as BAPI
    interface " " as BAPII
    BAPI - BAPII

    component "Interactive Brokers API" as IBAPI
    interface " " as IBAPII
    IBAPII - IBAPI
}
  
BNI )- TA
BN - BNI

TA --( ERI
ERI -- ER

TA --( GMI
GMI -- GM

TPI )- TA
TP - TPI

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

## 4. Open up your architecture so that it can be extended with plugins by its end-users. Where would be a good extension point? Update your logical view and give at least one example of what a plugin would actually do.


In the 2nd use case I added another component named Export Converter. This component is used as extensible component. Originally, it only converted into CSV file and then this CSV file was exported to the User Interface.

Now, a plugin component can be added to the extensible component thanks to the extension point. The following plugin component is fully compatible with the extension point.

The plugin can do following: export data in many possible formats such as CSV, JSON and Excel (xls).

### Logical view

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI



    component "Export Converter (default CSV)" as EC
    interface " " as ECI

    component "Plugin Converter" as PC
    interface " " as PCI

    interface " " as TPI
    
    PC -( PCI
    PCI - EC
    
    ECI )- TA
    EC - ECI

    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
    TA -( TPI
    TPI - TP

}

component "Trading platforms" as TP {
    component "Coinbase API" as CAPI
    interface " " as CAPII
    CAPII - CAPI

    component "Binance API" as BAPI
    interface " " as BAPII
    BAPI - BAPII

    component "Interactive Brokers API" as IBAPI
    interface " " as IBAPII
    IBAPII - IBAPI
}

component "Gmail Handler" as GM
interface " " as GMI

component "Exchange rate" as ER
interface " " as ERI

TA --( ERI
ERI -- ER

TA --( GMI
GMI -- GM

API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```
{.feedback

    - I guess "Trading Platforms" should not reside inside the backend box. Is it right? 

}

Yes, you are right.

## 5. Assuming you have a centralized deployment with all stateful components storing their state in the same database, propose a strategy to split the monolith into at least two different microservices. Model the new logical/deployment view as well as the interfaces of each microservice you introduce.

We made a decision to have Microservice for each Trading Platforms. The reason is that our controller Trading Aggregator may not handle the huge code in the future or we just want to have tidiness in our code. Hence, we apply "divide and conquer" strategy.

Each Microservices has own database. Microservices communicates with our controller Trading Aggregator.

Each Microservice runs in Container and the Container is located in Cloud. Containers communicates with Trading Aggregator via HTTPS.

The rest of software architecture remains untouched.

Again, for simplification I only use 3 Trading Platforms. But there will be more Trading Platforms.


### Logical view

```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

title "TradAgg" Logical View
interface " " as TAI

component "User Interface" as UI
component "Web API" as API
interface " " as APII

UI --( APII
APII -- API

component "BackEnd" as BE {
    component "Trading Aggregator" as TA
    interface " " as TAI

    component "Schedule" as SCH
    interface " " as SCHI

    component "Graph visualization" as GV
    interface " " as GVI

    component "Database <$database{scale=0.33}>" as DB
    interface " " as DBI

    interface " " as TPI
    
    TA --( GVI
    GVI -- GV

    TA --( SCHI
    SCHI -- SCH

    TA --( DBI
    DBI -- DB
    
}

    component "Exchange rate" as ER
    interface " " as ERI

    component "Gmail Handler" as GM
    interface " " as GMI
  
    component "Trading platforms" as TP {
        component "Coinbase API" as CAPI
        interface " " as CAPII
        CAPII - CAPI

        component "Binance API" as BAPI
        interface " " as BAPII
        BAPI - BAPII
 
        component "Interactive Brokers API" as IBAPI
        interface " " as IBAPII
        IBAPII - IBAPI
    }

    TA -( TPI
    TPI - TP

    TA --( ERI
    ERI -- ER

    TA --( GMI
    GMI -- GM

    rectangle "Microservice Binance" as MB {
            component "Binance Handler" as binance
            database "Database Binance <$database{scale=0.33}>" as DBB
        }
    interface " " as MBI

    MBI -- MB
    TA -( MBI

    binance --> DBB
    DBB --> binance

    rectangle "Microservice Interactive Brokers" as MIB {
        component "Interactive Brokers Handler" as brokers
        database "Database Interactive Brokers <$database{scale=0.33}>" as DBIB
        }
    interface " " as MIBI

    MIBI - MIB
    TA -( MIBI

    brokers --> DBIB
    DBIB --> brokers

    rectangle "Microservice Coinbase" as MC {
    component "Interactive Coinbase" as coinbase
    database "Database coinbase <$database{scale=0.33}>" as DBC
    }
    interface " " as MCI

    MCI - MC
    TA -( MCI

    coinbase --> DBC
    DBC --> coinbase


API --( TAI 
TAI -- TA

skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```

#### Deployment view
```puml
@startuml
skinparam componentStyle true

!include <tupadr3/font-awesome/database>

cloud "Cloud"{
        node "<<executionenvironment>> :PythonVM" as appnode {
        component "Schedule" as SCH
        component "Graph visualization" as GV
        component "Trading Aggregator" as TA
    }
}

node "<<device>> :Web Server" as webnode{
    component "Web API" as API
}

node "<<device>> :ClientPC" as usernode{
    node "<<executionenvironment>> :Browser" {
        component "User Interface" as UI
    }
}

node "<<device>> :Database Server" as dbservernode{
    component "MySQL Database <$database{scale=0.33}>" as DB
}

node "<<device>> :Exchange Rate Server" as exchangenode{
    component "Exchange rate" as ER
}

node "<<device>> :Gmail Server" as gmailnode{
    component "Gmail Handler" as GM
}

node "Trading platforms" as platformsnode{
    node "<<device>> :Binance Server" {
        component "Binance API" as BAPI
    }
    node "<<device>> :Coinbase Server" {
        component "Coinbase API" as CAPI
    }
    node "<<device>> :Interactive Brokers Server" {
        component "Interactive Brokers API" as IBAPI
    }
}


cloud "Cloud for Binance Handler" as cloudbinance {
    rectangle "Container - Microservice Binance Handler" as containerbinance {
        node "<<executionenvironment>>: Python" as pythonbinance {
            component "Binance Handler" as binance
            }
        component "Database Binance <$database{scale=0.33}>" as DBB
    }
}

cloud "Cloud for Coinbase Handler" as cloudcoinbase {
    rectangle "Container - Microservice Coinbase Handler" as containercoinbase {
        node "<<executionenvironment>>: Python" as pythoncoinbase {
            component "Coinbase Handler" as coinbase
            }
        component "Database Coinbase <$database{scale=0.33}>" as DBC
    }
}

cloud "Cloud for Interactive Brokers Handler" as cloudbrokers {
    rectangle "Container - Microservice Interactive Brokers Handler" as containerbrokers {
        node "<<executionenvironment>>: Python" as pythonbrokers {
            component "Interactive Brokers Handler" as brokers
            }
        component "Database Interactive Brokers <$database{scale=0.33}>" as DBIB
    }
}

brokers -- DBIB : <<internet>>

coinbase -- DBC : <<internet>>

binance -- DBB : <<internet>>

containerbrokers -- appnode : <<HTTPS>>

containerbinance -- appnode : <<HTTPS>>

containercoinbase - appnode : <<HTTPS>>

appnode -- webnode : <<internet>>

webnode -- usernode : <<internet>>

appnode - platformsnode : <<HTTPS>>

appnode --- gmailnode : <<IMAP>>

appnode -- exchangenode : <<HTTPS>>

appnode -- dbservernode : <<internet>>


skinparam monochrome true
skinparam shadowing false
skinparam defaultFontName Courier
@enduml
```