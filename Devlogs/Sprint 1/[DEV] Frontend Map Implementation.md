## **Progress Devlog - Frontend Map Implementation**

A big part of this project is the frontend interface for users. This interface will be used for conveying information from the system to the user, but another major part is allowing the user to configure certain aspects of the service. This includes for example configuring geofences. This is done through a map implementation on the webpage. This devlog will talk about the implementation of this map.
#

## Design
The first step in implementing a map into the frotend was to decide what map to use. This process was done through research made this sprint which is described in the research document [Mapping Technology Research](../../Delivery/%5Bv1.0%5D%20Mapping%20Technology%20Research%20-%20Robin%20van%20Hoof%2C%20Van%20den%20Bosch%20AMS.pdf). This research landed on the use of Google Maps API.

Up next designs were made for all pages that use the maps. Currently there are two pages that use a map elements with each their own functionality:

* Home page

The home page will have a map that displays realtime information on the loctions of the trackers. It will display the latest collected GPS datapoint of each tracker in the system, and additionaly has an option to zoom into a single tracker and look at its history. In terms of functionality the one main functionality this map needs is markers, and additionaly a filter option to filter on tracker IDs.

* Geolocations page

The geolocations page will have a map that displays existing geofences and allows the user to create new and customize existing/geofences. In terms of functionality this map need the ability for shapes to be drawn on it by the system, the ability for the user to draw shapes and location searching.

For both these pages frontend designs were made. These design can be seen below

| Home page | Geolocations page |
| :--- | :--- |
| ![Home page design](../../Media/Homepage%20frontend%20design.png) | ![Geolocations page design](../../Media/Geolocation%20page%20frontend%20design.png) |

<br>

## Implementation
Up next was the implementation step for the mentioned above features and pages. First of all, since the map that needed to be used was going to be a reoccuring part of the page with many overlapping functionality I made the map into its own seperate component that can be drawn into a page. This has the advantage that only one implementation of the map needs to be made, however this also comes with the disatvantage that the one singular map component needs to in some way posess the functionality of both maps.

For implementing the Google Maps API I made use of a library specifically made for Angular for implementing this features called 'Angular Google Maps', AGM in short. This library gives the developer the tools to implement the maps without needing to manually set everything up themselves manually.

The map AGM offers is only a very basic map that does not offer the additionaly features I needed for my maps out of the box. Up next I implemented a location searchbar. This searhbar uses the Google Map Locationi API to convert addresses or locations typed in by the user to coordinate points, which the map can then navigate to when the users looks up a location or place.

Furthermore, the functionalty for placing markers needs to be implemented. Using the data collected from the API endpoints of the AMS backend, a list of GPS datapoints can be collected. Then, using the Angular 'ng' functionalities were used to draw all the individual datapoints into the map in one coherent form.

Next, the ability to zoom into markers (specifically for the homepage) to show a history of GPS points for trackers was implemented. The markers for these get drawn in a similar way, however the markers in this view use different icons to make them less blocking, and the labels are replaced by timestamps of the GPS datapoint. Furthermore, a functionality was added that when the user is in the history view and zooms out, the amount of shown markers reduces the more the user zooms out to avoid cluttering the map.

Finally two last features were implemented mainly focused on optimalization. First of all, the list of markers was changed to work in a way that **only** the markers that are actually visible on the current bounds of the map get shown, as the amount of markers present was greatly impacting the performance of the map and site.

Second of all, marker grouping was implemented. This entails that whenever a user zooms out on the map, markers that are close together get grouped up together. AGM provides this functionality internally.

<br><br>

## Result
Implementing all the above mentioned features resulted in a fully working functioning map component. As the geolocations map is not yet a goal for this sprint, the functionality for drawing geofences was not yet made, as this will be done in a later sprint. A demo of the result can be seen below:

*This showcase is played at a playback speed of 2x* <br>
![Frontend Map Showcase](../../Media/Showcases/Frontend%20Map%20Showcase.gif) <br>
The full video at 1x playback speed can be found [here](../../Media/Showcases/Frontend%20Map%20Showcase%20Full%20Video.mp4).

<br><br>

## Next
Up next the implementaton for the geolocations map will be made when I get to the relevant sprint. The homepage map is currently finalized unless it is later on determined that other features are still needed.