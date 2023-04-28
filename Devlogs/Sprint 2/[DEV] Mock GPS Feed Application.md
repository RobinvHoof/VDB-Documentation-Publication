## **Progress Devlog - Mock GPS Feed Application**

No platform is complete without the data to make it work. The same goes for my AMS platform. However, hooking up the actual GPS trackers would require a lot of work since clearance for API keys would have to be acquired at the IT department. For that reason, the decsision was made to set up a mocking platform instead that will simulate a datastream from the tracking units.
#

## Design
First of all, to design a mocking application we'll first need to look at how the data is provided by the actual tracking units, as a mocking platform is not very useful if it doesnt match reality. The API for reading data from the trackers works with an active polling system, meaning the AMS would have to actively request data from the API to get measurements. This is a problem however as the AMS platform also works with active polling.

To make these two applications work together a middleman application, in the form of a scheduler, would have to be introduced. This however comes with the benefit that the form the data gets supplied to the AMS API can be competely customized in this in house application, meaning the form we mock the data in in the mocking application is not crusial and can later be used as template for the middleman application.

Thus, the decision was made to just folow the schemes of the existing API endpoints as is and make further changes as needed.

<br><br>

## Implementation
The next step was implementing the Mock GPS Feed Application. As this is a pretty small application and speed is not crusial I decided implement it in the form of a C# Forms Application, as this type of project allows for very fast paced development of simple applications.

There are a few controls I deemed necessary in the application. These controls are as follow

* Amount of trackers to simulate

The user should be able to set the amount of trackers they want to mock. This can be used to test the throughput of the system with a specific amount of trackers attached, allowing both real world simulation (large amount of trackers at longer intervals) and fictious situations (small amount of trackers at short intervals).

* Interval between messages

The user should be able to set the interval trackes will send their data. This can be used to test the speed the platfrom can handle data. Furthermore, this interval can also be set to 0 to make one continuous stream used for filling the database with data quickly.

* Target address

As the Mock Application requires the AMS platform, and specifically the GPS Service, to run to send the mock data to it, a host address for this service needs to be specified. The default address is a localhost address on the port of the service. However, if the service were to run in a live hosting environment at some point, this target address needs to be changed. Thus an option is given for this.

<br>

The API calls get made using Http request directly to the given target address. When the stream is started, a number of MockTracker classes get made with randomly generated longitudes and latitudes. Every time the data is read, the GPS point shift with a random amount into a semi-set direction to simulate movement over a linear road. 

<br><br>

## Result
Implementing all above mentioned aspects resulted in a working Mock GPS Feed application that can be used to either fill the database with data or fully simulate a stream of GPS data from a set amount of tracking units. What this application looks like can be seen below:

![Mock GPS Feed Application Interface](../../Media/Mock%20GPS%20Feed%20Application%20Interface.png)

<br><br>

## Next
Up next this Mock GPS Feed Application will be used to simulate the GPS trackers to test the system throughout the development process. For now, unless needed, no further changes will be made.
