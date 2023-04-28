## **Progress Devlog - Push Notification Endpoint Management**

One of the major functionalities of my project is the sending of notifications to thrid party platforms whenever a tracking unit arrives or departures from a key shipping location. This means calls will have to be made to applications outside of the scope of my own platform.
#

## Design
To start off on implementing this feature a plan of action was made. First of all, to implement this feature, in essence all that was needed from a backend development perspective was were some prety basic CRUD API endpoints. These endpoints were to be implemented in the Frontend Support Service. In terms of data, not a lot of information needs to be stored about these endpoints: as for now all thats needed is a display name for managing purposes and the actual host-address of the endpoint. The EER diagram for the endpoint database model can be found below.

Furthermore, I decided to leave out the 'Update' part as the data that was being handled here was so primitive, having only two datafields, that simply removing and adding a new field in case data needed to be edited made way more sense.

Up next a design for the frontend side of managing the endpoints was made. This page is part of the settings page:

| Endpoint EER Diagram | Endpoint Management Frontend Design |
| --- | --- |
| ![Endpoint EER Diagram](../../Media/Endpoint%20EER%20design.png) | ![Endpoint Management Frontend Design](../../Media/Push%20calls%20frontend%20design.png) |

<br>

## Implementing
Up next I started implementing the Controller and frontend as described above. This first started off with implementing the CR~~U~~D endpoints into the Frontend Support Service. These endpoints use Enity Framework to process the data in the database and allows for very versitile use of my data if ever needed in the future. These endpoints were implemented pretty quickly as I've done these many times before.

After setting up the endpoints all that was left to do was implement the frontend section that allows the user to manage the endpoints in the database. I used the visual design as seen above as starting point for this. However, I ended up slighly veering off in a few minor ways:
- The 'Add endpoint' button was replaced with direct input fields and a submit button in the header section of the page.
- As for now, a selector for what data to send to an endpoint was not yet implemented as the backend could currently not do anything with this data yet.


<br><br>

## Result
All the above mentioned steps resulted in a fulling functioning push notification endpoint management system that allows the user to create and remove different endpoints that push notifications should get made to. A quick demo of what the result of this looks like to the user can be seen below:

*This showcase is played at a playback speed of 2x* <br>
![Endpoint Management Showcase](../../Media/Showcases/Endpoint%20Management%20Showcase.gif) <br>
The full video at 1x playback speed can be found [here](../../Media/Showcases/Endpoint%20Management%20Showcase%20Full%20Video.mp4).


<br><br>

## Next
Up next I will expand upon this server if needed later in the future. One of the features that will possibly get implemented is the ability to select what information should be shared with different endpoints. However, since data fields themselves do not get processed in the platform yet and these are part of a 'could' priority requirement, this functionality was not yet implemented.