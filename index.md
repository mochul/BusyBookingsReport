# Busy Bookings!!
## Introduction/Background (10 points):

Busy Bookings is a booking application that enables customers to interact with businesses and allows businesses to manage their schedules, services, and customer appointments. The primary objective is to create a platform where customers can log in, explore various businesses and their availability, and make appointments through an interactive calendar. Furthemore, business administrators can register their businesses, maintain their profiles, manage availability, and oversee all booking activities from a centralized dashboard

## Software Technologies (15 points):

Technologies, Frameworks, and AI Tools:

  Frontend: React.

  Backend: Node.js. 

  Database: mySQL, Google Cloud Platform

  Version Control: GitHub.

AI Tools Used: GitHub Copilot, Claude/GPT

Rationale for AI Tools and Design Patterns: Copilot was useful because it was integrated into the coding environment and allowed to see various options for potential refactors and this helped us work faster. Claude/GPT o-1 preview helped us with code generation and reasoning when adding features. GPT was also useful for parsing error messages that were difficult to parse as a human. The ability to quickly sumarize problems was a great help in debugging. The combined usage of these two tools reduced development time and improved code readability.


## Requirements (20 Points):

Functional Requirements:

User Registration and Authentication:

  Users can create accounts with unique usernames and passwords.
  Users can log in based on their role (customer/business).
  The system must reject invalid credentials and maintain session security.
  
Business Onboarding:
  Business admins can register their businesses with a name, address, and availability.
  Businesses can specify operational hours and services offered.

Booking Creation and Management:
  Customers can search available slots and create bookings via an interactive calendar.
  Customers can view, edit, or cancel their bookings.
  Business admins can view, modify, and delete bookings.
  
Role-Specific Access Control:

  Customers and businesses see different dashboards.
  Business admins can access additional functionalities like availability settings and booking management.
  
Non-Functional Requirements: 
 - BusyBookings hould be able to process multiple requests at the same time without causing noticeable delays for users.

 - BusyBookings should allow the platform to accommodate more businesses and customers in the future without requiring major structural changes.

 - BusyBookings should allow customers and business owners to locate businesses, create bookings, and manage their profiles.

  
MMF 1: Business Onboarding and Profile Management
	•	Description: Enable business admins to register their businesses, create profiles, and specify services and availability. Allow  businesses to onboard themselves and populate the platform with offerings and make it functional for customers.	

MMF 2: Interactive Booking Calendar for Customers
	•	Description: Provide customers with an interactive calendar to view availability and book services with selected businesses. This is the core functionality for customers. 

MMF 3: Booking Management Dashboard for Business Admins
	•	Description: Offer business admins a dashboard to view, manage, and organize bookings, including customer details and booking statuses. Businesses need tools to manage their bookings efficiently. This feature empowers them to handle bookings.

MMF 4: Customer Dashboard
•	Description: Page where customers can view and manage all bookings they have made. Customers need tools to track and manage their bookings as it would be irresponsible for them to have to navigate to each business page individually. This would allow them to interact with the application in an easy and intuitive manner. 

   

## Design (30 Points)
The architectural designs that we implemented were the singleton design pattern, the observer design pattern, the factory design pattern, and the strategy design pattern. However, we will only discuss the first three in this document.

![alt text](./images/ObserverDesignDiagram.PNG)

First, we will take a look at the observer design pattern. As the diagram shows, it was specifically used for updating our calendars for when the bookings list was updated. This bookings list is instantiated upon a user logging in depending on whether they are a customer or business. Then, as bookings are created, the list is updated as well as pushed to the database. This also calls the notify() function which tells the calendars to update. This was extremely useful in keeping real time updates of the bookings for both types of users as well as that react can handle these updates instantly. 

![alt text](./images/SingletonDesignDiagram.PNG)

Next, we will take a look at the singleton design pattern. As the diagram shows, it was only used for the dbConnector class, which was only accessed by our App class (the main logic unit of our application). The connector was accessed many different functions all which needed to update or get entries from the database. It greatly helped with keeping our connection stable and manageable as without the singleton class, multiple could have been created which may have broken a connection or would have been very hard to manage properly. It also helps when multiple users are using the application at once as all information goes through the single connection.

![alt text](./images/FactoryDesignDiagram.PNG)

Finally, we will take a look at the factory design pattern. As the diagram shows, this was used for creating users at their instantiation. When a new user is made, we can call their respective factory to create a new user object with their information and then push that to the database. It was very useful with its intended purpose. Since we didn’t know what type of users we will be creating when the application is opened, it allowed us to have an easy way to do so. It allowed us to remove ambiguity from creating user logic. 


## Design Patterns Implementation (30 points):

Design Patterns:

  Singleton Pattern: Makes sure there is only one single instance of each class.  This prevents resource wastage and complexity, which greatly helped during development, and will help when multiple users are using the application. As we add more to the code base, it will keep the connector consistent throughout all of our updates. For our singleton object, we had db_connector.js implementing a single instance of the database connection, ensuring consistent and efficient management throughout the application.

  Observer Pattern: Notify multiple objects about any events that happen to the object they are observing. This enables a one-to-many dependency, where it is possible
  and even encouraged for multiple objects to base their behavior on an object while preventing tight coupling of any of the objects.  For example, when a booking changes, observers (like business calendar and customer calendar) are automatically updated. React states are used here, enabling components like CreateBookingsPage.jsx and Calendar.js to automatically update in response to state changes.

  Factory Pattern: Allows for a superclass object and factory object where subclass objects of each can be created with new fields, inherienting the super class for ease of creation of new objects. Was used specifically for the user types, business and customer. When the App class creates a new user, it calls the respective factory class to create a new user, and then pushes that to the database. When users are pulled from the database, the respective factory class is called to create that user for usage throughout the application. This allowed for extremely easy creation of new users and will greatly help when expanding the application as we could expand this to bookings where new bookings go through a factory. This would also allow for new types of bookings to be made easily. Overall, the pattern allows for much better scalability as we expand the application.


## Testing Strategy, Execution, AI tool analysis (60 points):

Overall, we took a two-pronged approach towards testing, splitting the testing across white-box and black-box both in methods and in purpose.
We mainly employed blackbox testing for system testing, ensuring that every key functionality was still up and running after every merge. We specifically
used decison table testing, a black-box testing method that uses a table to organize input combinations and their corresponding outcomes.
It's a technique used to identify the correct test cases for systems with complex business rules. This was perfect for our project as there were
very complex rules governing our logins, calendar, and booking system where both security and efficiency had to be balanced. After every merge 
we tested the application once again to ensure nothing broke and the new changes were implemented smoothly. When this was not the case, we would roll 
back the change and start over. 

On the other hand, we mainly utilized unit testing for our whitebox testing. This allowed for our integration testing to focus on integration as much as possible without being dragged down by easily foresseable bugs. This meant almost all of this testing for new code was done pre-merge. The database would be thouroughly tested in isolation, before being connected to the backend API. This was mostly done using ChatGPT and Claude to write out test querys, as well as make edge-case suggestions based on the already written code. Similarly, the backend Node.js API and frontend React interface were all tested in isolation through whitebox testing before being merged into the main project.

Of our AI tools, some were better used for whitebox testing and some for blackbox. Claude was most useful in White-Box testing, as it was the best tool at writing new code and specific test cases. ChatGPT had a higher tendency to hallucinate when dealing directly with syntax. In contrast, ChatGPT was the better AI tool for blackbox testing, as it was better then Claude at understanding descriptions of functionality without code examples. It was consistantly better at identifying theoretical edge cases, then Claude.

In terms of impact, AI streamlined the testing process a significant amount. Traditionally, it took us around a day or two to develop comprehensive tests, for 
both black and white box. With AI, this was reduced to under a day, sometimes only an hour or two of prompting the agent and removing tests we deemed irrelevant.
However, AI did have a blind spot in terms of spotting defects in the code, reducing the overall quality of each test. However, due to the fact that it was able to
generate at least 4-5x more raw tests than we could manually, this was a shortcoming we eagerly worked around. Furthermore, the test robustness from the AI was not up
to our standard, as it generally only understood the test case in reference to the code we provided, meaning than any changes we made to the code, no matter how small,
could potentially cause most if not all of their pre generated tests to stop working. We found that the best practice was to use AI to create ideas for tests, perhaps provide
some started code, then take over the rest ourselves. 




## Challenges and Innovations (15 points):

Challenges:

  Role-Based Control: Ensuring that users with different roles see different features was challenging. It was also difficult to integrate and work with the calender. The solution involved designing clear logic in the backend.
  
  Integrating AI Tools Effectively: Striking a balance between relying on Copilot’s suggestions and maintaining code quality required discipline. Initially, we had code bloat and less-than-ideal suggestions, but we refined prompts and learned when to trust AI recommendations.
  
  Decision Table Testing: Mapping various,complex booking scenarios into decision tables took time, but once done, it streamlined test case generation.

Innovations:

  Use of Claude for Complex Testing and Debugging: Claude’s ability to reason about code and offer structured solutions was leveraged, going beyond simple code generation.
  Observer Pattern in Calendar UI: The calendar’s automatic updates with booking changes gave a seamless user experience, distinguishing this project’s approach from simpler static booking pages.


Project Outcomes and Evaluation (10 points):

Summarize the final outputs, emphasizing the effectiveness/non-effectiveness of AI tools in achieving project goals.
Critically assess the project outcomes relative to the initial objectives and provide a quantitative and qualitative evaluation.

## Future Directions (10 points):


Integrate load balancing and caching strategies as user base grows.
Utilize AI-driven anomaly detection for booking. For example, suspicious patterns or double-booking attempts.
Implement a recommendation engine to suggest businesses based on user preferences.
Implement reminders and notifications through SMS or email, further automating the booking experience.
Integrate automated load testing tools and performance profiling guided by AI suggestions.

## Contributions

| Team Member  | Contribution                                                                 |
|--------------|------------------------------------------------------------------------------|
| Michael      | Testing, Introduction, Design Patterns, Google Pages Setup                                   |
| Ishaan       | Introduction, Software Technologies, Requirements, Future Directions, Challenges and Innovations |
| Vivien       | Software Technologies, Testing, Future Directions                          |
| Mattias      | Design, Design Patterns Implementation, Challenges and Innovations     |

