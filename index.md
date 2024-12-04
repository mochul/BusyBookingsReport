# Busy Bookings!!


## Introduction/Background (10 points):

Busy Bookings is a booking application that enables customers to interact with businesses and allows businesses to manage their schedules, services, and customer appointments. The primary objective is to create a platform where customers can log in, explore various businesses and their availability, and make appointments through an interactive calendar. Furthemore, business administrators can register their businesses, maintain their profiles, manage availability, and oversee all booking activities from a centralized dashboard

Software Technologies (15 points):

Technologies, Frameworks, and AI Tools:

Frontend: React
Backend: Node.js
Database: MongoDB (NoSQL document database)
Version Control: GitHub

AI Tools Used:
GitHub Copilot: Automated code suggestions and completions directly in the IDE.
Claude/GPT: Code generation, debugging advice, and architectural suggestions.

Rationale for AI Tools and Design Patterns:
Copilot is integrated into the coding environment, giving real-time suggestions and reducing trivial coding tasks. Claude/GPT, conversely, excels at reasoning about complex code blocks, helping to restructure code, improve performance, or debug tricky issues. Their combined usage significantly reduced development time and improved code readability.

Design Patterns:

Singleton Pattern: Makes sure there is a single instance of critical resources.  Thisprevents resource wastage and complexity.
Observer Pattern: Maintains a clear one-to-many relationship between components. For example, when a booking changes, observers (like the calendar UI and business dashboards) are automatically updated.
Single Responsibility Principle: Ensures each module or class has one well-defined purpose, making code easier to test and refactor. This enhances scalability. 

## Requirements (20 Points):

Functional Requirements:

User Registration and Authentication:

Users can create accounts with unique usernames and passwords.
  Users can log in based on their role (customer/business admin).
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

  Performance:
  The system should handle multiple concurrent requests without significant latency.
  Scalability:
  The architecture should support adding more businesses and customers without major restructuring.
  Usability:
  Intuitive UI/UX to ensure users can easily find businesses, create bookings, and manage their profiles.
  Reliability:
  System should maintain consistent uptime and gracefully handle errors.

Design (30 Points):

Present architectural design diagrams.
Explain your design decisions and their impact.
Design Patterns Implementation (30 points):

Document the design patterns used, their justification, visual evidence of their usage, and their impact on the project’s structure and maintainability.

## Testing Strategy, Execution, AI tool analysis (60 points):

Overall, we took a two-pronged approach towards testing, splitting the testing across white-box and black-box both in methods and in purpose.
We mainly employed blackbox testing for system testing, ensuring that every key functionality was still up and running after every merge. We specifically
used decison table testing, a black-box testing method that uses a table to organize input combinations and their corresponding outcomes.
It's a technique used to identify the correct test cases for systems with complex business rules. This was perfect for our project as there were
very complex rules governing our logins, calendar, and booking system where both security and efficiency had to be balanced. After every merge 
we tested the application once again to ensure nothing broke and the new changes were implemented smoothly. When this was not the case, we would roll 
back the change and start over. 

On the other hand, we mainly utilized unit testing for our whitebox testing. 

Elaborate on the Test Strategy, including whitebox and blackbox testing methods. List various tools used for testing and explain their purpose.
Provide detailed test cases and their outcomes.
Discuss the AI tools used in blackbox and whitebox testing.
Offer a comparative analysis on the performance, usability, and impact of these tools on productivity and quality, including metrics and statistical evidence. (30 points)

## Challenges and Innovations (15 points):

Challenges:

  Role-Based Control: Ensuring that users with different roles see different features was tricky. The solution involved designing clear user flow logic and robust middleware checks on the backend.
  
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
Utilize AI-driven anomaly detection for booking. For example, suspicious patterns or double-booking attempts).
Implement a recommendation engine to suggest businesses based on user preferences.
Implement reminders and notifications through SMS or email, further automating the booking experience.
Integrate automated load testing tools and performance profiling guided by AI suggestions.

## Contributions
| Team Member  | Contribution |
| ------------- | ------------- |
| Michael       | Testing   |
| Ishaan       | Introduction, Software Technologies, Requirements, Future Directions, Challenges and Innovations   |
