## **Reading Guide - Van den Bosch Address Management System**
### Robin van Hoof
#

This document will describe my progress through the "Address Management System" (AMS) project for my internship at Van den Bosch. This project will be a predecessor for an in house made AMS Van den Bosch will be making in Juli of this year, either using my prototype as a basis to start on, or using my research and results as a stepping stone to build a new platform off of.

<br><br>

# Project & Documentation setup

## Devlogs
The documentation about the progress of this project will be done through the use of devlogs: Short bits of documentation that cover the what, hows and whys of the process of the implementation of a single feature. This project will have two types of devlogs: Research devlogs and process devlogs. 

- Research devlogs

Each of theses types of devlog will be built up to answer five predefined questions:

- What was the challenge?
- What methods were used to solve this challenge?
- What was the result?
- How were these results validated?
- What will be done with these results?

The main purpose of these devlogs is to answer a research question and do something with said result.

- Process devlogs

These types of devlog describe the steps taken in developing a feature. These devlogs do not persee answer a question but instead just give a general idea of progress and an insight on the thought process behind certain made decisions.

<br>

To describe what methodology is used to achieve steps in a devlog the [DOT Framework](https://ictresearchmethods.nl/The_DOT_Framework) will be used. In every devlog where research happened, the used DOT strategy will be identified using one (or multiple) of the five following icons representing their corresponding DOT strategy:

| <img src="https://ictresearchmethods.nl/images/8/87/Logo-library.png" width="50px" /> | <img src="https://ictresearchmethods.nl/images/d/d4/Logo-field.png" width="50px" /> | <img src="https://ictresearchmethods.nl/images/a/ac/Logo-lab.png" width="50px" /> | <img src="https://ictresearchmethods.nl/images/2/22/Logo-showroom.png" width="50px" /> | <img src="https://ictresearchmethods.nl/images/e/ea/Logo-workshop.png" width="50px" /> |
| :---: | :---: | :---: | :---: | :---: |
| Library | Field | Lab | Showroom | Workshop |


<br><br>

## Sprints
The development process of this project will be done through sprints: The devision of the project over short sprints of 2 weeks that focus on a single objective. As mentioned before, I've decided on a sprintlength of 2 weeks per sprint, mainly to allow for very high-paced development of the many smaller features defined in for this project.

As a result of these two week sprints the project will have a total of 9 sprints, devided in 3 phases: 

- Definition-phase

Sprint 0, in this phase I will focus on defining what the project will entail together with my internship company, set up the bounds of the project and make agreements on what to document and what will be expected of me.
- Development-phase

Sprint 1 to 8, in this phase I will focus on developming the features establish in the project plan. Alongsides the development a lot of documention of the developed features and research will be made during this phase.
- Finalization-phase

Sprint 9, in this phase I will focus on finalizing the project and internship. This will entail mainly setting up all needed transfer documentation, reflecting on the project and preparing the finaly delivery of the assignment.

<br>

### Development-phase
As mentioned before the development phase will consist of a total of 8 sprints. A plan has been made on what each of these sprint will focus on:
| Sprint | Focus |
| :---: | :--- |
| Sprint 1 | Front- and Backend application setup, Swagger settup |
| Sprint 2 | Login and Authorization |
| Sprint 3 | Handling incomming GPS-data-stream |
| Sprint 4 | Geofence generation, importing existing geofences  |
| Sprint 5 | Analyzing incomming GPS-data, refining geofence generation |
| Sprint 6 | Sending notifications of arrivals/departures to third parties |
| Sprint 7 | Front-end optimalization, [C] processing extra data fields |
| Sprint 8 | Back-end optimalization, [C] implementing Active Directory SSO | 

Tasks marked with a "[C]" tag are tasks that are concidered 'Could Haves' In the project specification and will thus only be done if time allows for it.


<br><br><br><br>

# Sprint Progression
The rest of this document will in chronological order take you through the progress of the asignment, linking to the different devlogs made throughout the different sprints.

<br>

## Sprint 0
As mentioned before sprint 0 mainly focused on the definition of the project together with the company and school. This was done through setting up a Project Plan and Requirements, detailing exactly what is expected of the student throughout the project.

I also set up my working environments in this sprint. This was mainly the DevOps envrionment including but not limited to Backlogs and testing pipelines. Furthermore I spent some time setting up hosting environments in the form of a docker hosting environmnet 

Furthermore, due to quite a bit of time being left over in this sprint I moved forward one of the tasks of sprint 1 to this sprint and started on implementing the Authorization into the frontend of the system. This process is described in the devlog [[DEV] Frontend Authorization](./Devlogs/Sprint%200/%5BDEV%5D%20Frontend%20Authorization.md).

<br>

### Products
| Product | Link |
| :--- | :--- |
| Project Plan | [File](./Delivery/%5Bv2.0%5D%20Projectplan%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch.pdf) |
| Requirements | [File](./Delivery/%5Bv2.1%5D%20Requirements%20Document%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch.pdf) |
| Authorization Devlog | [Devlog](./Devlogs/Sprint%200/%5BDEV%5D%20Frontend%20Authorization.md) |

<br><br>

## Sprint 1
Sprint 1 mainly focused on getting the project going. In this sprint I worked on setting up the basics of both front- and backend applications. This started with making architectural design of the backend services. 

I split up the backend functionality into three distinct microserverices with each its own role. This was mainly done for one reason: One of the main microserverices, namely the GPS service, needs to be able to handle it very large load as the amount of tracking units increases. To allow for expansion later on I isolated all functionality for the GPS-units in one service so in case more capacity is needed, more instances of the service can be deployed. This did however require isolation of these functionalities. The architectural design of the backend can be found [here](./Delivery/%5Bv1.0%5D%20Backend%20Architectural%20Design.jpg).

Furthermore I also made designs for the different frontend pages that would be made throughout the project. I also sketched out different recursive components like a navigation bar. These designs can be found [here](./Delivery/%5Bv1.0%5D%20Frontend%20Designs.jps.jpg).

I also set up Swagger for automated API endpoint documentation in this sprint. I set it up in such a way that XML comments could be used on all different objects and would automatically be translated to the appropriate endpoint remarks and comments in the different Swagger pages. An example of this Swagger generation can be found [here](./Media/Swagger%20auto-documentation%20example.png).

<br>

In terms of development quite a bit of progress was made in this sprint, even some development that was initally planned for a later sprint. 

First of all, a map for displaying information about the Tracking Units was implemented in the frontend. In the end Google Maps API was chosen for this. More about this, including research on the reserach toppic of *"What technology can be used to display a worldmap where the administrator can draw geofences on?"*, can be found in the devlog [[DEV] Frontend Map Implementation](./Devlogs/Sprint%201/%5BDEV%5D%20Frontend%20Map%20Implementation.md).

Second of all, an implementation for database integration and data-management was done. Entity Framework was chosen for this. More about this, including research on the research toppic of *"What storage-media can best be used to store all relevant data for this project?"*, can be found in the devlog [[DEV] Data-storage](./Devlogs/Sprint%201/%5BDEV%5D%20Data-storage.md).

Additionaly, in this sprint the Logging Service was implemented and for the time being finalized. This service will function as a general point for all services and applications to report possible errors or actions to. More about the development of this service can be found in the devlog [[DEV] Logging Service](./Devlogs/Sprint%201/%5BDEV%5D%20Logging%20Service.md).

Furthermore, in this sprint the first part of the Frontend Support Service was implemented. This service is responsible for providing the frontend with all needed infomration and handling request from the frontend for processing certain data. In this sprint the functionality of managing push notification endpoints was implemented. More about the development of this feature can be found in the devlog [[DEV] Push Notification Endpoint Management](./Devlogs/Sprint%201/%5BDEV%5D%20Push%20Notification%20Endpoint%20Management.md).

<br>

### Products
| Product | Link |
| :--- | :--- |
| Backend Architectural Design | [Image](./Delivery/%5Bv1.0%5D%20Backend%20Architectural%20Design.jpg) |
| Frontend Designs | [Image](./Delivery/%5Bv1.0%5D%20Frontend%20Designs.jps.jpg) |
| Swagger Automated Documentation Generation | [Image](./Media/Swagger%20auto-documentation%20example.png) |
| Mapping Solution Research | [File](./Delivery/%5Bv1.0%5D%20Mapping%20Technology%20Research%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch%20AMS.pdf) |
| Frontend Map Devlog | [Devlog](./Devlogs/Sprint%201/%5BDEV%5D%20Frontend%20Map%20Implementation.md) |
| Data-storage Devlog | [Devlog](./Devlogs/Sprint%201/%5BDEV%5D%20Data-storage.md) |
| Logging Service Devlog | [Devlog](./Devlogs/Sprint%201/%5BDEV%5D%20Logging%20Service.md) |
| Push Notification Endpoint Management Devlog | [Devlog](./Devlogs/Sprint%201/%5BDEV%5D%20Push%20Notification%20Endpoint%20Management.md) | 

<br>

### Demo Result Sprint 1
*This demo is played at a playback speed of 2.5x* <br>
![Sprint 1 Result Demo](./Media/Demos/%5BS1%5D%20Result%20Demo.gif) <br>
The full video at 1x playback speed can be found [here](./Media/Demos/%5BS1%5D%20Result%20Demo%20Full%20Video.mp4).

<br><br>

## Sprint 2
Sprint 2 focused on getting the basics of GPS handling working on the platform. This included both backend-sided functionality to receive GPS datapoints from a tracking unit or simulator of one, and the frontend-sided functionality to visualize the GPS data to users.

Furthermore in this sprint a lot of research was done mainly on how to effectively and efficiently handle the GPS data, but also on how to store the geofences in the system and how the means of storage would effect and could be used to check if a GPS point is within a geolocation.

Finally a big step was made in project organisation. Previously all the different applications, meaning the frontend and each api service, lived on the same GIT repository split up using folders. However, I realised different repositories could be made within one project. Thus, I spent time sperating each application putting each onto their own repository with custom workflows. Because this move the HTTPLogger library made in the previous sprint was not available anymore. This was solved by publishing the library as a NuGet library and making it accessibly through NuGet.

<br>

In terms of development a lot of progress was made again, once again even more then was origionally planned for this sprint resulting in the project running about 4/5 weeks ahead in schedule. This quick progression was discussed with my internship coach and a suggestion to start thinking about what additional features they might want was made. Any developments in this field will be documented.

First of all, as discussed before the basics for handling incomming GPS data were implemented. This was done in one major API endpoint that can be called by the middleman software that communicates with the trackers. More about the development of this feature can be found in the devlog [[DEV] Basic GPS Handling](./Devlogs/Sprint%202/%5BDEV%5D%20Basic%20GPS%20Handling.md).

Second of all, an implementation of visualising the GPS data to the user was made in the frontend. Two crusial parts of imformation are displayed in here: The most recent location of every tracker registered in the system, and the option to get more detail about one tracker and see its location history. Setting up this feature also included creating a new endpoint in the Frontend Support Service responsible for providing the frontend with the needed GPS data. More about the development of this feature can be found in the devlog [[DEV] Visualizing GPS Data](./Devlogs/Sprint%202/%5BDEV%5D%20Visualizing%20GPS%20Data.md).

Finally, a middleman mocking application was made that will be used throughout the development of this platform to mock the data the trackers would provide in the final solution. This application sends calls to the GPS Feed endpoint in the same way the middleman application will later on, thus simulating a feed of tracking-unit data without needing the actual data. More about the development of this feature can be found in the devlog [[DEV] Mock GPS Feed Application](./Devlogs/Sprint%202/%5BDEV%5D%20Mock%20GPS%20Feed%20Application.md).

<br>

### Products
| Product | Link |
| :--- | :--- |
| Basic GPS Handling Devlog | [Devlog](./Devlogs/Sprint%202/%5BDEV%5D%20Basic%20GPS%20Handling.md) |
| Visualizing GPS Data Devlog | [Devlog](./Devlogs/Sprint%202/%5BDEV%5D%20Visualizing%20GPS%20Data.md) |
| Mock GPS Feed Application Devlog | [Devlog](./Devlogs/Sprint%202/%5BDEV%5D%20Mock%20GPS%20Feed%20Application.md) |

<br>

### Demo Result Sprint 2
*This demo is played at a playback speed of 2.5x* <br>
![Sprint 2 Result Demo](./Media/Demos/%5BS2%5D%20Result%20Demo.gif) <br>
The full video at 1x playback speed can be found [here](./Media/Demos/%5BS2%5D%20Result%20Demo%20Full%20Video.mp4).

<br><br>

## Sprint 3
Sprint 3 focused on setting up the foundations for creating and using geofences in the AMS platform. This includes both the backend side of creating, requesting and editing geofences and the frontend side of allowing the user to create new and edit existing geofences.

Furthermore, user research was done this sprint in terms of how to represent the geofences to the user to make both the displaying of and creation/editing of geofences intuitive and easy to understand. More about this research can be found in the research document [Frontend Geofence User Research]().

<br>

In terms of development quite a few big steps were made on the aspect of geofences. First of all, a complete implementation of the geofences in terms of backend handling was made. This includes creating, storing, getting and editing geofences through API endpoints and Entity Frameworks Toplogoy suite. More about this feature can be found [here]().

Up next, a complete implementation of the geofences in the frontend was made. This included designing and creating a frontend page, splitting up the existing map component to allow multiple implementations of the map with different functionalities (GPS- and geofence display) and implementing the backend API into the frontend to supply the needed data. More about this feature can be found [here]().

Finally a tool to measure the capacity of the platform was created. This tool can be used on a running instance of the API to test the maximum capacity it can handle in terms of requests per minute. More about this feature can be found [here]().

<br>

### Products
| Product | Link |
| :--- | :--- |
| Frontend Geofence User Research | [File]() |
| Backend Geofence Implementation Devlog | [Devlog]() |
| Frontend Geofence Implementation Devlog | [Devlog]() |
| Capacity Testing Tool Devlog  | [Devlog]()  |

<br>

### Demo Result Sprint 3
*This demo is played at a playback speed of 2x* <br>
![Sprint 3 Result Demo](./Media/Demos/%5BS3%5D%20Result%20Demo.gif) <br>
The full video at 1x playback speed can be found [here](./Media/Demos/%5BS3%5D%20Result%20Demo%20Full%20Video.mp4).

<br><br>

## Sprint 4
Sprint 4 focused on a lot of different small aspects not related to development of the AMS project. Instead, I focused this sprint on other smaller chores either requested by the company or in support of the Address Management System Project. 

First of all, a request from the company was made to do research into how A/B testing could be used and deployed in Azure environments. Currently many of the services produced by the company run in an Azure environment, but no A/B testing is applied here. I was asked to look into how to set up A/B testing for this environment. This resulted in an extra research toppic and research document that can be found [here](./Delivery/%5Bv1.2%5D%20Azure%20AB%20Testing%20Research%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch%20AMS.pdf).

Second of all, a big part of this sprint was focused on database maintance. The biggest achieved goal here was implementing the existing Geolocation database from Bulkio into my AMS platform database. This process is described in the [Bulkio Geolocation Database Importing Devlog]().

Finally, a big overhaul of all data in the database was done. This included filtering out a vast amount of incomplete entries, correcting incorrect datafields where possible and cleaning up all entries. All these steps resulted in a cleaned up uniform database that was easier to use and gives users a better user experience.

<br>

### Products
| Product | Link |
| :--- | :--- |
| Azure A/B Testing Research | [File](./Delivery/%5Bv1.2%5D%20Azure%20AB%20Testing%20Research%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch%20AMS.pdf) |
| Bulkio Geolocation Database Importing Devlog | [Devlog]() |

<br>

### Demo Result Sprint 4
As no real progress was made this sprint on development of the AMS platform a sprint demo is not applicable.

<br><br>

## Sprint 5
Sprint 5 focused on finishing up a lot of the big features of the AMS project and polishing features implemented throughout the project. In terms of new features a few ease of use features in addition to the last additions to complete the MVP were added.

First of all, one of the final MVP aspects was added, namely Endpoint typing. Before, endpoints could be subsribed to receive notificatons from the GPS service whenever a tracking unit arrived at or departed from a geolocation. However, when an endpoint was subscribed, it would always be subscribed to recieve *all* notifications from the service, even ones that are not relevant for the service. A featue was implemented where each endpoint subscription can additionally subcribe for individual events to further refine the external notification system. This process is further described in the [Notification Endpoint Typing Devlog]().

Second of all, two features for monitoring trackers and geolocation were added: First a log of all geolocation a tracker has been at, second a log of all tracking units that have been at a geolocation. This allows for better in depth monitoring of both objects. The monitoring happends on the Logging Service which is subscribed as an external endpoint to receive Arrival/Departure events from the GPS Service. This was also the first major external endpoint added to the AMS system and can be used to ensure the functionality of the external endpoint notification system. More about this feature can be found in the [Geolocation and Tracking Unit History Devlog]()

<br>

### Products
| Product | Link |
| :--- | :--- |
| Notification Endpoint Typing Devlog | [Devlog]() |
| Geolocation and Tracking Unit History Devlog | [Devlog]() |

<br>

### Demo Result Sprint 5
*This demo is played at a playback speed of 2x* <br>
![Sprint 5 Result Demo](./Media/Demos/%5BS5%5D%20Result%20Demo.gif) <br>
The full video at 1x playback speed can be found [here](./Media/Demos/%5BS5%5D%20Result%20Demo%20Full%20Video.mp4).

<br><br><br><br>
<hr>

## Versions
| <div style="min-width=150px;">Version</div> | <div style="min-width=150px;">Date</div> | Changes |
| :---: | :---: | :--- |
| 1.0 | 03-03-2023 | Document setup, project & documentation setup, sprint progression sprint 0, sprint progression sprint 1 |
| \| | 06-03-2023 | Versions, distribution, mapping solution research |
| \| | 17-03-2023 | Sprint progression sprint 2 |
| \| | 29-03-2023 | Sprint progression sprint 3 |
| \| | 03-04-2023 | Sprint 3 demo, sprint progression sprint 4 |
| \| | 28-04-2023 | Sprint progression sprint 4, sprint progression sprint 5, sprint 5 demo |


<br>

## Distribution
| <div style="min-width=150px;">Version</div> | <div style="min-width=150px">Date</div> | <div style="min-width=150px;">To</div> | Goal |
| :---: | :---: | :--- | :--- |
| 1.0 | 20-03-2023 | Marcus Krielen | Format feedback |
| \| | 28-04-2023 | Marcus Krielen | Midterm portfolio feedback |
