## **Progress Devlog - Basic GPS Handeling**
The core functionality of the AMS is handling the GPS data from the tracking units and processing this data in the platform. This devlog covers the setup of the basic GPS handling of incomming calls from the GPS tracking unit or middleman applications.
#

<br><br>

## Design
First of all, we need to determine what functionality is needed for handling incomming GPS data API calls. The most important part is a single API endpoint that needs to be created which the GPS tracking units or middleman applications will make calls to. This will be the 'Feed' endpoint. In theory, this will be the only accessible endpoint the GPS data will be send to, as all calls should come in in the same format and thus on one centralised endpoint.

The endpoint will accept calls from a middleman application that relays the information from the tracking units. This means that the format the data will come in can be customized based on the platforms needs. This also means that theres complete freedom in terms of the required data format for the endpoint.

Next up decison were made on what data should be provided in a request to the endpoint and what data (and in what form) needs to be saved to the database. Two diagrams were made as seen below. The first describes what data is required when making the API call to the endpoint. The second diagram shows what data and how it gets saved in the database:

| Endpoint model | Database model |
| :-- | :--- |
| ![Endpoint Model](../../Media/GPS-Datapoint%20Endpoint%20Model.png) | ![Database Model](../../Media/GPS-Datapoint%20Database%20Model.png) |


<br><br>

## Implementation
In terms of implementation the first step was making the API endpoint itself. The endpoint will take an object as described above (Endpoint Model) as body in an HTTP request and will then be processed. Currently there are two posibilities for the timestamp depending on what situation will be applicable in practice:

The first situation is the middleman application polling the data from a GPS unit every ten minutes and getting data from that exact timestamp. If this is the case the 'timestamp' field in the API call does not have to be provided and instead a timestamp of the moment the API call is made can be recorded.

The second situation is the middleman application polling the data from the tracking unit supplier every ten minutes, and getting a list of datapoint that were taken in those ten minutes. If this is the case, using a timestamp of when the API receives the call would not be accurate and would not represent the real tracking unit location. In this situation a timestamp would have to be provided with the API call.

<br>

I decided to go for an approach where both are possible: If a timestamp is proved with the API call that timestamp will be used for the request. If none is provided, the current timestamp on request arrival will be used. This way, regardless of what kind of middleman application is used.

<br>

Next up the was the tackeling of when to actually process an incomming datapoint. If every single data point is processed and saved every time one comes in a vast amount of useless data will built up in the database. For example, a tracking unit that is stationairy for a long time (parked in storage for example), it will over the span of multiple days or weeks create thousands of entries of the exact same location. Thus we need a way to filter when to process a datapoint.

I introduced a filter that looks at the distance from the last GPS datapoint. If this distance is less then roughly 100 meters the GPS point will be deamed as 'being the same location' and not be handled. However this poses an issue: If a tracking unit is just barely outside a destination geofence on one measuring point, drives into the geofence but stays within 100 meters of the last datapoint it will never be concidered to have arrived. Thus, a failsafe needs to be implemented. This was done by adding an override to the previous rule if the GPS datapoint is withing any geofence.

If both above mentioned conditions are true the datapoint will be handled by the service and saved to the database.

<br><br>

## Result
Implementing all above mentioned features resulted in a working API that can handle incoming data from tracking units, determine if they need to be handled, determine if they are inside any geolocations and if so save the data sent.

<br><br>

## Next
Up next a feature will be implemented in this service to send out HTTP calls when a GPS datapoint is determined to be inside a geolocation. Other than that this feature is deemed finalized and will not be further developed unless needed.