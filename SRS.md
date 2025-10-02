# Software Requirements Specification

## Structure
Document Conventions:

1.	Section Numbering: Sections will be numbered in hierarchical format (e.g., 1, 1.1, 1.2, etc.) 
2.	Requirement Identification: Functional and non-functional requirements will be labeled as FR-x or NFR-x respectively.
3. This document aims to follow IEEE 830-1998 which is the standard for SRS documents.
   
### "DirectionsMQ" Mobile app
 
 Team - Wobbie FC

 - Parth Bhatia
 - James Cheung
 - Mst Asma Ul Husna
 - Tsenguun Tsengel
   
### Vision statement
Our vision is to provide students and visitors at Macquarie University a seamless and intuitive mobile direction navigating app to make campus life easy. “DirectionsMQ” will be connected to real-time GPS and Wi-Fi location to deliver precise data, this app will provide it’s user , about on foot directions along with vehicle directions that  will help users find their way to specific buildings, rooms, and points of interest across campus. Our app will go beyond traditional mapping services by offering personalized route options, such as the ability to take the driest path during wet weather or to explore scenic routes. Through integration with the MQ-Directions-Service, our app will continuously adapt to campus changes, ensuring that users always have the most up-to-date and accurate navigation information. We visualize “DirectionsMQ” as the go to solution for navigating Macquarie University, making it easier for everyone to reach their destination efficiently and comfortably.

### Change Log

| Version | Date           | Description                         | Committed By                     | Approved By                      |
|---------|----------------|--------------------------------------------------|-----------------------------------|----------------------------------|
| 1.0     | 22 August 2024  | Added minutes for 22nd August                    | Jc2026 (James Cheung)             | LondonCowboys (Parth Bhatia)     |
| 1.1     | 29 August 2024  | Added functional requirements for Team B         | LondonCowboys (Parth Bhatia)      | Asmabristy (Mst Asma Ul Husna)   |
| 1.2     | 29 August 2024  | Added minutes for 29th August                    | Asmabristy (Mst Asma Ul Husna)    | tstsenguun (Tsenguun Tsengel)    |
| 1.3     | 2 September 2024| Added use case diagram                           | Asmabristy (Mst Asma Ul Husna)    | tstsenguun (Tsenguun Tsengel)    |
| 1.4     | 4 September 2024| Added discussion in SRS                          | tstsenguun (Tsenguun Tsengel)     | LondonCowboys (Parth Bhatia)     |
| 1.5     | 5 September 2024| Added minutes for 5 September                    | Asmabristy (Mst Asma Ul Husna)    | Jc2026 (James Cheung)            |


### Section 1: Introduction

1.1 Purpose:

The main purpose of this SRS document is to provide the software specifications for our “Directions MQ”  application and serve as a legally binding document upon the client’s approval. We are aiming to satisfy user expectations and facilitate the development of a software system that will cater to our stakeholders needs and interests while creating a net positive impact to wider society. In terms of the intended readership, this document is mostly addressed to our stakeholders and beneficiaries such as university students, teaching staff, campus visitors and software developers responsible for the implementation. We aim to faciliate a seamless integration phase from concept to full implementation.

1.2 Conventions:

Our SRS conventions will follow the industry standard by focusing on functional and non functional requirements which are based on IEEE 830-1998 to ensure the quality and structure of our document. Our goal is to reduce development efforts, provide a realistic cost basis, act as a contract baseline, facilitate development of the software and make sure that there is a clear understanding of project objectives for all stakeholders. 

1.3 Scope:

The Document Scope will clearly describe both functional and non-functional needs of the “Directions MQ” app as specified by our stakeholders and only focuses on app development. The apps focus is to use GPS and WIFI-Positioning and enable main functionalities such as user navigation, waypoint navigation (storage of interim and destination waypoints) and choice of routes (scenic route or shortest route).  Furthermore, we will include user assumptions and software dependencies that can affect the development of the app. 


### Section 2: Terms and Definitions

SRS: Software Requirements Specification  

IEEE 830-1998: An industry-standard for Software Requirements Specification 

GPS: Global Positioning System – A satellite-based navigation system used for determining the exact location of the user on Earth.  

MQ-Directions-Service: A routing service on the Macquarie University campus.  

MQ-Directions-Service Serve: A server for routing on the Macquarie University campus. 

API (Application Programming Interface): Protocols that allows for intercommunication between software applications.   

ETA (Estimated Time of Arrival)   
Anonymous Uploading: App specific feature allowing for privacy by not using identifying metadata.

RTK (Real Time Kinematic): An extremely accurate navigation technique used from a base station. 

WPS (WiFi Positioning System): Determines the location of a device by using nearby WiFi access points.

GIS (Geographic Informaiton System): System that maps, stores and displays geographical data.  

Restful API: APIs that follow constraints to ensure resource efficiency.

### Section 3: Assumptions

It is not the intention of this document to explore the architectural design of this application, and these will be the key assumptions of this document as follows:

External Dependencies:
-	We assume that all servers linked to the application will always be fully operational and that stakeholders are aware of this assumption. Note that malfunction of servers will affect this apps performance.

Server Development 
-	We will not be developing a central server and instead rely on route calculation to be handled by an external server called MQ-Directions-Service. Our app will interact with this server, but we are not responsible for building or maintaining this server. 
-	MQ Directions service will provide route calculation and navigation after GPS and WIFI Positioning determines real time user location. 

Navigation Scope:
-	Directions MQ will only be available on campus and is not intended as a general navigational application

Security:
-	All users will have have their route information stripped of identifying metadata unless they choose to share their data.

Sufficient WiFi Infrastructure:
- Assume that Macquarie University has sufficient WIFI access points indoors for triangulation

Use of Real-Time Kinematic:
-	Assume the university infrastructure uses RTK for GPS positioning

Use of Geographic Information System:
-	Assume GIS infrastructure is used by Macquarie University and is synchronised with the Directions MQ service server

Restful APIs
-	Assume that restful APIs are not being used before implementation of this app

Authentication
-	All authentication is done by OAuth2.0

Server Scalability: 
-	Macquarie’s servers can be scaled and handle sufficient server requests and API requests

### Section 4: Overall Description:

4.1 Product Perspective: 

“Directions MQ” is a software based mobile application that will be integrated with the Macquarie University technology infrastructure and aims to provide a real time and tailored navigational on campus service. Our applications will be integrated with the global GPS system alongside an RTK system on campus which enables our application to achieve a 14mm positional accuracy. The application will also utilise WPS which will leverage WIFI access points for accurate location triangulation inside buildings where GPS signals are sometimes non-existent. 

Further integration of the app can be achieved through syncing with Macquarie’s GIS system. As this software is primarily responsible for managing building layouts, this allows the application to dynamically update routes based on real time changes to the university campus such as areas being closed for renovation or new areas under construction.  

Local caching will also play a key role in this application to allow for offline navigation on the local device as a layout can be stored. This can display preloaded routes as well as saved destinations in the case of a WIFI connection being disrupted.

During the final implementation phase, restful APIs will also be integrated into university servers. Through this, the Directions MQ server will handle API requests such as route data or process user-submitted routes for approval by an admin. This connection will be done via the HTTP protocol and use OAuth2.0 for authorisation to prevent server overload.  

4.2 Product Functions:

Selecting Destination Waypoints:
o	Users can select specific university locations as waypoints, such as campus buildings, campus facilities, or classroom numbers.
o	A dropdown menu will appear on the app, showing possible matching locations and ensuring that the location is correct.
o	Directions MQ will communicate with the server once the destination waypoint is selected, and on-screen information will be displayed.

Type of Route:
o	Users can choose routes based on their preferences, e.g., the shortest route or a route that avoids rain.
o	There will be an icon on the app's UI showing the weather conditions, along with a toggle option for weather-specific routes.
o	Route options will appear after a waypoint is selected.

Adding Intermediate Waypoints or Points of Interest:
o	Intermediate waypoints or points of interest can be added using an option on the UI. For example, a route to 25 Wally’s Walk can have Macquarie Library added as an intermediate location if the user wants to stop by the café to get food.
o	Waypoints can be favourited and added.
o	Directions MQ will find the shortest way to each waypoint by default.

Saving Routes and Points of Interest (POI):
o	Routes and points of interest can be saved and favourited.
o	Certain destinations can be renamed, for example, 11 Wally’s Walk can be renamed to “Class 2”.
o	Routes can be saved and named by the user.

Real-Time ETA:
o	The Estimated Time of Arrival (ETA) will be calculated in real-time through interaction with a backend system that uses a GNN machine learning model. Nodes and edges will match real-life locations and paths.
o	The average speed of the user will be reported back to the server, which will calculate the ETA.

User-Submitted Routes:
o	Directions MQ will allow students and staff to share routes, which can be approved by an administrator on the MQ Directions service server.
o	After these routes are approved, they can be liked and rated in a dropdown menu.
o	The dropdown menu for user-submitted routes will be sorted based on their ratings.

Route Complaints:
o	There will be a side menu in the app with the option to report routes that display inconsistencies with real-life situations. For example, a route may show that there is no construction, even though there is construction.

Finding Empty Study Spaces:
o	There will be a feature for students to find the nearest study space that has not been booked.
o	For teaching staff, there will be an option to show meeting locations and available time slots.
o	Multiple locations will be listed, and users can set a waypoint to the study or meeting location.

Accessibility Features:
o	The app will include an option to avoid routes that are difficult for people with disabilities to access.

4.3 User Characteristics:

The intended users of Directions MQ and their respective roles are as follows:

Students:

Students are expected to be the largest user base, as most will use the app to navigate their way to classes, locate facilities on campus, and find available study spaces.
Students can set preferred routes and customise routes according to their needs.
Students can also propose new routes and report issues with existing routes.

Teaching Staff:

Faculty and administrative staff can use the app for campus navigation and to find available meeting rooms.
They can set preferred routes and customise routes as required.
Teaching staff can propose new routes and report problems with existing routes.

Visitors:

Visitors are expected to be another significant user base. They can use the app for navigation but will not have access to features such as study space or meeting room availability.
Visitors can set preferred routes and customise them according to their preferences.
Visitors can also propose new routes and report any problems they encounter.

4.4 Constraints:

Due to the assumptions we have made, there are several key constraints that may challenge the functional excellence of Directions MQ:

RTK Signal Obstruction:

To achieve maximum real-time precision with RTK, it is essential to ensure that there are no obstructions near the RTK stations that could interfere with the signal.

Reliability of WPS:

As indoor GPS signals are often non-existent, the app depends on Wi-Fi Positioning System (WPS) for accurate indoor navigation. To maintain this accuracy, Wi-Fi access points must be widely available and reliable.
If the Wi-Fi signal is unreliable, indoor triangulation will not function correctly, negatively impacting the app’s performance.

Synchronisation with GIS:

Continuous synchronisation with Macquarie University’s GIS is required to ensure that building layouts and potential hazards (e.g., ongoing construction) are up-to-date.
Any issues with synchronisation could lead to outdated information being used in route calculations, resulting in suboptimal routes and reduced app performance.

Server Scalability:

The app’s servers must be highly scalable to handle a large volume of requests, particularly during peak times. Any server request overload could cause the app to become unresponsive or cease functioning entirely.

Operating Systems:

The app is designed to be compatible with multiple operating systems (e.g., Android, iOS), which can introduce complexities and delays during the development phase due to differences in system requirements and performance optimisations.

### Section 5: Specific Requirements

5.1 User Requirements:

•	FR-1: Buildings on campus can be chosen as a destination, and the user can select a room in the chosen building as the specific destination.
o	The app displays a searchable list of all buildings on campus. Upon selecting a building, the app shows a list or a map of all rooms within that building. Users can successfully select both a building and a room as their final destination, with the system providing accurate directions to that specific room.

•	FR-2: Waypoints can be added whilst on a route, which does not override the original destination and merely redirects the route to include the waypoint.
o	Users can add multiple waypoints at any time during the route. The app recalculates the route to include the waypoints and displays the updated path. The original destination remains unchanged, and the waypoints are integrated seamlessly into the overall route.

System Requirements:

•	FR-3: Routes can be saved and labelled such that we can choose from preloaded routes for a destination. Meaning a single destination can have multiple routes (e.g., best for scenic routes, best for wet weather).
o	Users can save any route with a custom label. The app allows at least two different routes to be saved for the same destination. Saved routes are accessible from a "Saved Routes" menu, and users can select a previously saved route with a single click.

5.2 Non-Functional Requirements:

•	NFR-1: Adding waypoints requires less than 3 seconds to load the route to the new sub-destination in order for navigation to be efficient for the users of ‘DirectionsMQ’.

•	NFR-2: The updated route to the waypoint displays appropriate directions on the map and shows an updated ETA until the waypoint.

•	NFR-3: Saved/preloaded routes and destinations can be accessed while the application is not connected to the internet.

•	NFR-4: Users have the option to save the map, route, and waypoint data locally on the device, which will update routinely when the device is connected to the internet.

•	NFR-5: Users can upload routes that are scrubbed of any identifying information, including metadata, in order to protect the privacy and security of the application's users.

•	NFR-6: When routes are uploaded to the public forum/listing, user data is not attached to the upload (anonymous uploading).

### Section 6: Use cases

"DirectionsMQ" app planning and route management

- Name:
  Route Planning and Management

- Goal:Allow users to plan, manage, and update their routes by selecting destinations, adding waypoints, uploading routes, and managing these routes with an external direction service (MQ-Directions-Service).

- Actors:

    User: The primary actor who interacts with the system to plan, save, and manage routes.

    MQ-Directions-Service: An external service providing directions and estimated time of arrival based on user input.

    Admin: Responsible for managing routes and updating the system.

- Preconditions:
The user must be logged into the system.
MQ-Directions-Service should be available and functional for route updates and ETA calculation.
Admin must have access to manage the routes.

- Success End State:
The user successfully plans, uploads, and manages their route, receiving estimated time of arrival (ETA) via the external service.

- Failure End State:
Routes are not uploaded or saved.
Directions or ETA information is not retrieved from MQ-Directions-Service.
The system cannot update or manage routes.

- Main Scenario:
The user selects a destination.
The user adds waypoints (optional).
The user saves the route.
The user uploads the route to MQ-Directions-Service for processing.
The user receives an estimated time of arrival (ETA).
The user can update the route, if necessary.
The admin manages and oversees route arrangement and updates within the system.

We have also provided a picture of a use case diagram for better understanding of our stakeholders.

  ![Screenshot 2024-09-02 175443](https://github.com/user-attachments/assets/7e386a53-8f6b-4227-91d8-dd008831f41b)


Below are the three most important use cases based on our use case diagram "DirectionsMQ" app planning and route management. Each story outlines the initial situation, standard sequence of events, possible problems, simultaneous activities, and the final outcome.
### User Story 1:As a user, I want to select a destination and add waypoints to my route, so that I can customize my journey and receive more accurate directions .

- Starting Situation:
The user has logged into the system and wants to create a route by selecting a destination and adding waypoints.

- Normal Flow of Events:
The user selects the "Select Destination" option from the interface.
The system prompts the user to enter a destination such as via a search bar or map interface.
After selecting the destination, the user is given the option to add waypoints.
The user adds one or more waypoints, refining the route to pass through specific locations.
The route is displayed visually, showing the destination and waypoints.

- What Can Go Wrong:
The system cannot find the destination.
Invalid waypoints or an error in waypoint input could occur.
The system crashes or is unable to display the route visually.

- Concurrent Activities:
The system checks the availability of waypoints and verifies the destination given by the user.
The system ensures that all waypoints are on a valid route and connects to the MQ-Directions-Service to validate the entered destinations and waypoints.

- End State:
The user has successfully created a route with a destination and waypoints, which is displayed on the map interface.

### User Story 2: As a user, I want to upload my route to the directions service  and retrieve the estimated time of arrival (ETA) , so that I can plan my journey effectively and know when I will reach my destination.

- Starting Situation:
The user opens the DirectionsMQ application and initiates the sign-in process. After successful authentication via the MQAuthService, the user is presented with the main menu and is ready to create a route by selecting a destination and potentially adding waypoints.

- Normal Flow of Events:
The user selects the "Choose Destination" option from the main menu.
The system displays a searchable list of buildings within Macquarie University or external destinations, depending on the user's input.
The user searches for and selects a specific destination (either a building or a room within a building).
If the destination is within the university, the DirectionsMQ system requests route data from the MQ-Directions-Service and displays the calculated route.
If the destination is external, the system sends a request to an external directions service for route information and displays the external route.
The user may choose to add waypoints to the route by selecting "Add Waypoint."
The system provides options for selecting waypoint locations. After the user selects a waypoint, the route is updated and recalculated, showing the revised route and the estimated time of arrival (ETA).

- What Can Go Wrong:
The system fails to connect to the MQ-Directions-Service, possibly due to connectivity issues or an unresponsive service.
The external directions service may be down or may respond with an error if the route data is not formatted correctly or if there is a server issue.
Waypoints or destination selections may be invalid or improperly formatted, causing the route to fail or not be displayed correctly.

- Concurrent Activities:
While the student is selecting a destination or adding waypoints, the MQ-Directions-Service continues processing route data for other users.
The system periodically checks connectivity and ensures that any route or waypoint data can be uploaded or updated in real-time.

- End State:
The user successfully uploads the route, including waypoints if added, and receives the ETA displayed on their interface. The route is visually shown, reflecting the destination and any waypoints along the path.

### User Story 3: As a user, I want to manage and update my saved routes, so that I can make adjustments to my journey, add or remove waypoints, and ensure I have the most up-to-date directions and ETA.

- Starting Situation:
The user or admin wants to manage and update an already created route due to changes in travel plans or new information.

- Normal Flow of Events:
The user selects the "Manage Routes" option from their dashboard.
A list of saved routes is displayed.
The user selects a route to update.
The system allows the user to change the destination or add/remove waypoints.
The user saves the updated route.
The system synchronizes the changes and sends them to MQ-Directions-Service for reprocessing, if necessary.
The updated route, along with a new ETA, is displayed to the user.

- What Can Go Wrong:
The user selects an invalid route to update.
The system fails to save the updated route.
The MQ-Directions-Service is unavailable for recalculating the ETA.

- Concurrent Activities:
Admins monitor all route changes and updates by users.
The system may have other users updating routes simultaneously.

- End State:
The selected route is updated, and the user or admin has successfully made the required changes. A new ETA is available if needed.

The Interaction diagram visually represents the process described in User Story 2, which involves a student using "DirectionsMQ" app to select a destination, calculate a route, and potentially upload the route to internal services such as MQ-Directions-Service  to retrieve an estimated time of arrival (ETA).

 ![Screenshot 2024-09-07 075705](https://github.com/user-attachments/assets/fa8534be-3098-47bc-917d-8c377ce97df0)

The  Interaction diagram captures the flow of interactions between the student, the DirectionsMQ system, the MQ authentication service, and an external routing services if the designated destination or the alternative route is outside of Macquarie . It highlights both typical routing processes within the university and external route handling, along with the possibility of adding waypoints and recalculating routes based on user preferences.

### Section 7: Discussion

 #### Elicitation Methods

We have used various elicitation techniques to capture the requirements of the "DirectionsMQ" mobile application. Each technique has been chosen with purpose so that we could understand their needs, expectations, and constraints with respect to the project. Below are the techniques followed, along with the details of their implementation:

- Interviews:
  - Methods Applied: Structured interviews with key stakeholders such as students, university staff, and visitors were conducted. These interviews captured the 
    expectation, pain points, and desires for a campus navigation solution.

  - Details: We held in-person interviews, as well as video calls to make this more accessible to all. We devised open-ended questions that would result in very 
    focused answers. For example, asking users to describe how they get around campus today and pain points would help us understand the need for features such as 
    real-time updates and personal route optimization.

- Workshops:
  - Techniques Used: Several workshops were conducted involving all levels of stakeholders, including representatives of the university facilities management, IT 
    department, and student bodies to brainstorm ideas, align on project objectives, and identify potential challenges.
  - Details: We conducted brainstorming sessions in these workshops and used mind mapping to bring out ideas. Identification of integration with the current 
    university services was one of the essential conclusions arrived at, like Wi-Fi networks for location tracking.

- Online Surveys and Questionnaires:
  - Approaches Used: To get feedback from an even larger group, we asked for campus input through survey handouts to students and faculty. The questionnaires 
    consisted of quantitative data, such as how often one uses campus maps, along with qualitative feedback, like suggestions for improvements.
   - Details: Most of the questions in these questionnaires were multiple-choice to ease data analysis, while some were open-ended for more descriptive feedback. 
    This really helped us put an approximate quantity on how many people wanted features like being able to select scenic routes or avoid highly crowded 
    areas.

- Observation:
   - The Techniques Applied: We have witnessed students and visitors in transit across campus to identify the problem that may not be reported through 
     interviewsor questionnaires. This technique was especially useful in uncovering unexpressed needs.
   - Details: Observation during peak times, such as between classes, was done to see the end-user interaction with existing signage and maps. The problems 
     identified from this included a lack of directions in certain areas and the need for a mobile solution to help provide step-by-step guidance.

- Document Analysis:
  - Techniques Used: A review was done of existing documentation, including campus maps, university infrastructure plans, and any prior feedback given by users on 
    current campus navigation tools.
   - Details: This focus group helped us understand the current limitations of existing systems and identified a potential place for improvement. Examples include 
     old and unfriendly campus maps. The majority of users claimed that this was a problem and provided grounds to include real-time updating within the app.

#### Section 8: Outlook
If we were  to continue the project, we would have taken  a number of steps to develop  the system architecture and refine the requirements further.Few of the steps and our proposed system architecture for our "DirectionsMQ" navigating  app  are given below:

![Screenshot 2024-09-04 203742 (2)](https://github.com/user-attachments/assets/12e31646-1636-41b7-a814-05927f01bfb6)


- Continuous Feedback Loop:
  - Approach: We would, therefore, be creating a continuous feedback loop with stakeholders through frequent check-ins, user testing sessions, and prototype 
    reviews. This will make sure that during the project, requirements remain aligned with user needs.
  - Details: One way this can be achieved is to conduct periodic surveys and interviews about prototypes and beta versions of the app. Such feedback can be 
    compiled and used to further refine the requirements and subsequently prioritize new features.

- Prototyping and User Testing:
  - Approach: Interactive prototype development and, consequently, user testing will serve to validate requirements that may otherwise show gaps or problems in 
    our system much too late in the course of development.
  - Details: First, we will create low-fidelity wireframes followed by high-fidelity prototypes to test particular features such as personalized routing and real- 
    time updates. We will conduct user testing sessions with a diverse stakeholder group to receive feedback on usability and functionality.

- Prioritization and Scope Management:
  - Approach: Extra requirements gathering would be done in order of prioritization on the basis of user impact, technical feasibility, and alignment to the 
    vision of the project.
  -  Details: A systematic approach will be used to evaluate and rank requirements. This might involve creating a scoring system or a prioritization matrix that 
    considers factors such as the potential benefits to users, the level of technical difficulty, and how well the requirement fits with the project’s strategic 
    objectives. Engaging stakeholders through surveys or focus groups could also provide insights into the relative importance of different requirements. Regular 
    review meetings will be scheduled to reassess priorities as the project progresses and new information becomes available.

- Advanced Feature Exploration:
  - Approach: The solution would then be further explored with more advanced features, such as integration with other smart campus initiatives-like IoT sensors 
    for occupancy detection-to keep "DirectionsMQ" current.
  - Details: Workshops with the university's IT and facilities management teams could help identify potential integrations with other campus technologies. This 
    might lead to new features including dynamic routing based on real-time foot traffic data.

- Ensuring Correctness and Completeness of Requirements:
  - Approach: We would ensure that the requirements are accurate and complete by implementing vigorous techniques for validation, including peer reviews, 
    requirement traceability, and regular stakeholder validation sessions.
  - Details: RTMs would be developed that connect each requirement to its source and specific test cases. This will give confidence that the requirements are 
    necessary and tested during the development process.

- Risk Management
   - Approach: Risk identification and management would be vital for the success of the project.
   - Details: Continuous risk assessment would reveal technical limitation, changes in priorities of stakeholders, among other challenges. A mitigation strategy 
     would be developed for high-impact risks.

Hence, through such a process,  "DirectionsMQ" mobile app could be developed and further enhanced to suit the needs of the users and fulfill the vision of making Macquarie University's campus much easier to navigate for one and all.

### Section 9: Appendices

| **Log of Interactions with Stakeholders**                   | **References**                                                | **Third-party Resource**                                                                                       |
|-------------------------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| 2024-08-15: Initial project  meeting with Stakeholder Team A.   | Project Brief Document from Stakeholders                           | UML 2 Use Case Diagrams: An Agile Introduction – The Agile Modeling (AM) Method                        |
|                                                             |                                                               | URL: https://agilemodeling.com/artifacts/usecasediagram.htm                                                     |
|                                                             |                                                               | Description: Used as a reference for the use case diagram creation in this SRS.                                 |
| 2024-08-22: Functional Requirement clarification with stakeholders.     | Instagram group communication with stakeholders.                        | Lucidchart – Ben Dilts and Karl Sun                                                                             |
|                                                             |                                                               | URL https://www.lucidchart.com/pages/ |
|                                                             |                                                               | Description: Used as a tool for designing diagrams in the SRS.                                                  |
| 2024-08-29: Discussion on deliverables and Non-Functional Requiremnts.    | Internal Design Specifications Document such as Functional and Non-Functional Requirements.                      | Markdown Preview Mermaid Support (v1.23.1) – Matt Bierner                                                       |
|                                                             |                                                               | URL: https://bierner.gallerycdn.vsassets.io/extensions/bierner/markdown-mermaid/1.23.1/1718743113268/Microsoft.VisualStudio.Services.Content.License |
|                                                             |                                                               | Description: Used to create Mermaid diagrams in the SRS documentation.                                          |
| 2024-09-05: Final approval for testing phase from Team A.       | Meeting notes from weekly project stand-up.                   | IEEE 830-1998: Software Requirements Specification (SRS) Standard                                               |
|                                                             |                                                               | URL: https://standards.ieee.org/ieee/830/1222/                                                                  |
|                                                             |                                                               | Description: Industry Standard that provides best practices.                                                    |
| 2024-09-12 : Project Handover to our Stakeholder            | Stakeholders feedback on Test Plan Document.                      | Positioning Australia: GPS Information – Geoscience Australia                                                   |
|                                                             |                                                               | URL: https://www.ga.gov.au/scientific-topics/positioning-navigation/positioning-australia/about-the-program      |
|                                                             |                                                               | Description: Information about GPS technology in Australia and used to explain the GPS functionality within the Directions MQ system. |
|                                                             |                                                               | Wi-Fi Positioning System vs. GPS – Eelink                                                                       |
|                                                             |                                                               | URL: https://www.eelinktech.com/blog/wps-vs-gps-5-reasons-to-use-wifi-positioning-system-devices-in-your-business/ |
|                                                             |                                                               | Description: Explains differences between WPS and GPS, used to advocate for WPS.                                |
|                                                             |                                                               | RTK System Overview – National Center for Biotechnology Information (NCBI)                                       |
|                                                             |                                                               | URL: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9611497/                                                      |
|                                                             |                                                               | Description: Referenced to understand RTK technology application in Directions MQ to achieve centimetre-level accuracy. |
|                                                             |                                                               | RTK Accuracy in Measurement Systems                                                                             |
|                                                             |                                                               | URL: https://doi.org/10.1016/j.measurement.2022.111647                                                          |
|                                                             |                                                               | Description: Provides detailed insights into RTK accuracy and its benefits to MQ Directions.                    |
|                                                             |                                                               | Geographic Information Systems (GIS) – SAGE Publications                                                        |
|                                                             |                                                               | URL: https://doi.org/10.1177/1473325016655203                                                                   |
|                                                             |                                                               | Description: Explores GIS application and its integration with Directions MQ for dynamic routing.                |
|                                                             |                                                               | RESTful API Design – MDPI                                                                                       |
|                                                             |                                                               | URL: https://www.mdpi.com/2076-3417/12/9/4369                                                                   |
|                                                             |                                                               | Description: Provides insights into RESTful APIs, used to guide API implementation for server communication.     |
|                                                             |                                                               | OAuth 2.0 Authentication and Authorization – National Center for Biotechnology Information (NCBI)               |
|                                                             |                                                               | URL: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4838526/                                                      |
|                                                             |                                                               | Description: Industry-standard protocol for secure user access within the Directions MQ app.                    |
|                                                             |                                                               | Estimated Time of Arrival (ETA) Calculation – ACM Digital Library                                               |
|                                                             |                                                               | URL: https://dl.acm.org/doi/abs/10.1145/3459637.3481916                                                         |
|                                                             |                                                               | Description: Methods for real-time ETA calculations, used in the ETA functionality section.                     |
|                                                             |                                                               | Logo Creation: Canva                                                                                            |
|                                                             |                                                               | URL: https://www.canva.com/design/DAGP3xZ3uQI/N-bYTBAhXhWmLopVCjN1eA/view?utm_content=DAGP3xZ3uQI&utm_campaign=designshare&utm_medium=link&utm_source=editor |
|                                                             |                                                               | Description: Canva used to create the project logo for Directions MQ.                                           |

