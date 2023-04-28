## **Process Devlog - Logging Service**

One of the three major microservices of my project is the Logging Service. This service will function as main point for reporting and collecting all server messages, from user actions to server outage notifications.
#

## Design
For startes a plan was made on what exactly the functionality of the Logging Service should be. As mentioned before, the service is the centralized service that logs all events within the system. Thus the service should have functionality for creating and storing logs, later reffered to as event-logs.

Furthermore, making event-logs are not very useful if you do not in turn have a way to display these in some meaningful way. Thus functionality should be made to retreive event-logs from the service which will likely be implemented as an API endpoint that the frontend can address to request a list of event-logs to show.

To get an overview of all needed functionality I made a diagram of the service and its different endpoints. This diagram can be seen down below besides the event-log EER diagram.

<br>

## Implementing
Up next I started implementing the Controller as described in the Endpoint Overview. This first started off with making the Controller and the Methods, all while giving myself a refresher course on ASP.NET Core Web API projects. During the creation of all methods XML comments were written describing the functionality and usage of each endpoint so Swagger could use these XML comments to automatically document each endpoint.

After a first version of all methods without database interaction was made I set up a Unit Testing project to test all the different functionalities. This Testing Project uses a mock database to replace the interaction with the actual database and ensures functionality of all logic code behind each endpoint.

After setting up the Unit Tests I proceeded to add the database onto the Logger Service using Microsoft's Entity Framework. Why this approach was used is talked about more in the devlog [[DEV] Data-storage](./%5BDEV%5D%20Data-storage.md). I made an overview of what information an event-log should contain in the for of an EER diagram. This diagram was used as base for the Model for the EF Context:

| Event-log EER Diagram | Logging Service Endpoint Overview |
| --- | --- |
| ![EventLog EER Diagram](../../Media/EventLog%20EER%20Diagram.png) | ![Logging Service Enpoint Overview](../../Media/Logging%20Service%20Endpoint%20overview.png) |

Then functionality was added to the GET method for getting event logs from the service to filter and sort the provided events in meaningful ways. For example, an option for maximum amount of logs to be provided in a request was implemented, and possibilities for only showing a specific level of log was implemented. These parameters can be supplied through URL parameters when making the API request.

Finally a display section for the logs was implemented in the frontend. A page was made for this that allowed the user to see logs and apply the above mentioned filters to the shown logs. This page was based off of the design sketched made earlier in this sprint as described in the reading guide.

<br>

A lot of the logs that need to be made to the Logging Service will originate from the other services. This will require an implementatoin of exatly the same logging code in every service that will be made in the future. To prevent this and avoid repetitive code I decided to look into moving this funtionality to a seperate Class Library that can then be imported into every project. This resulted in the creation of the *HttpLogger* Library, who's .dll is imported in every microservice and used for reporting events to the logger service.

<br><br>

## Result
All the above mentioned steps resulted in a fully funtioning Logging Service that can be easily addressed by other services through the HttpLogger library and the frontend through API calls. A quick demo of what the result of this service looks like to the user can be seen below:

*This showcase is played at a playback speed of 1.5x* <br>
![Logging Service Showcase](../../Media/Showcases/Logging%20Service%20Showcase.gif) <br>
The full video at 1x playback speed can be found [here](../../Media/Showcases/Loggin%20Service%20Showcase%20Full%20Video.mp4).


<br><br>

## Next
Up next I will keep implementing this service into all other microservices through use of the HttpLogger library. The goal of this is to make sure all noteable events are logged and kept track of.