## **Progress Devlog - Data Storage**
The platform needs to handle and retain a lot of information to be able to offer all the needed functionality. For this, some form of data storage needs to be implemented. 
#

## Design
First of all, a decision on what type of data storage medium to used needed to be made. The process of figuring out what possibilties were available and what the advantages and disatvantages of each are can be found in the research document [Data storage reserach](). The choice to use Entity Framework using an MSSQL database was made.

In terms of design, first of all a general overview of the database design was made in an EER Diagram. This digram can be seen below.

![Databaes EER Overview](../../Media/Database%20EER%20overview.png)

However, since Entity Framework works using a code-first approach to database design all tables and such could not be created beforehand and need to be created when implemented into the service. This does also come with a great advantage: If changes turn out to be needed later on, the database can very easily be changed as this can be done using migrations.

<br>

## Implementation
The next step was implementing the database context and Entity Framework setup into every microservice. In terms of database hosting the initial plan was hosting a dockerized SQL server on my local at-home server, which all microservices used. The reason for this was because I work two days from home, where I work from my PC and not my Laptop, one singular database could be used for both so one doesnt need to be set up locally on each system. However, after testing this approach it turned out the office network security in the Bulkio office is set up in a way that it doesnt allow these kinds of connections. Thus, this plan was scrapped and a switch to local databases was made.

I set up the Entity Framework implementations using EF's migration system. This started with setting up a context for each microservices that detailed the data structure of the data the microservice needs. This context is then put into the database using an EF migration. Furthermore, a migration step was introduced in the startup of each microservice, which will automatically try to migrate the latest context of the application to the database.

Finally, a problem arose with the database setup. Namely the fact that some parts of the database, for example the GPS data, need to be accessed by two microservices. At first, this doesnt seem like a problem, however when one service makes the database entry using a migration and another service (and thus another context) tries to migrate its own copy, the table already exists with different content then expected causing a fatal error during migration. To fix this I started working with a master-context setup, where one service will take charge over a bit of data. Whenever another service needs access to the data, it can be defined in the context, but specifically in a way where it can only read and/or write data and not make changes to the structure. This should (for now) fix this issue.

<br><br>

## Result
Implementing the above mentioned features resulted in a working database for the AMS platform to use. Even though this implementation works, there are quite a few limitations that in a production environment would have to drastically change. Mainly the fact that currently the databases run locally on the development systems. This would have to transition to one singular hosted production database.

<br><br>

## Next
Up next the database implementation will be used to store and supply the AMS platform with all the data transactions needed. If changes need to be made in the future this will be done through migrations. 