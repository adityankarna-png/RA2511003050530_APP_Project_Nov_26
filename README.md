# Smart Disaster Evacuation & Resource Allocation System

A Java-based disaster management application designed to manage disaster information, register victims, monitor shelters and resources, and prioritize evacuation operations through a rule-based priority calculation system.

## Project Overview

The **Smart Disaster Evacuation & Resource Allocation System** is a desktop application developed to support disaster response operations. During emergencies, coordinating victims, shelters, rescue resources, and evacuation activities can become difficult when information is managed manually.

This system provides a centralized platform where administrators and response teams can manage disaster-related information, monitor available resources, and process evacuation requests efficiently.

The application uses Java Swing for its graphical user interface and MySQL for database management. It also incorporates multithreading for background monitoring and notification operations.

## Objectives

- Centralize disaster-related information.
- Maintain victim records and identify evacuation requirements.
- Manage shelters and their available capacity.
- Monitor resources and their stock levels.
- Calculate victim evacuation priorities using a rule-based scoring system.
- Assign victims to suitable shelters and available resources.
- Process evacuation requests and monitor their status.
- Provide reports and system notifications.

## Key Features

### 1. Dashboard
- Displays an overview of system activities.
- Provides access to different application modules.
- Presents disaster, victim, shelter, resource, and evacuation information.

### 2. Disaster Management
- Add and manage disaster records.
- Maintain disaster-related information.
- Monitor active disaster records.

### 3. Victim Management
- Register victims affected by disasters.
- Maintain victim information.
- Record vulnerability and medical details.
- Support evacuation prioritization.

### 4. Shelter Management
- Maintain shelter information.
- Monitor shelter occupancy and capacity.
- Identify shelters with available capacity.

### 5. Resource Management
- Manage available relief resources.
- Track resource quantities.
- Update stock after resource allocation.
- Identify resources that are out of stock.

### 6. Evacuation Management
- Generate evacuation requests for registered victims.
- Calculate evacuation priority scores.
- Assign suitable shelters and available resources.
- Maintain evacuation status.

### 7. Reports
- Display system summary information.
- Retrieve reporting data from the database.
- Perform background report loading using SwingWorker.

### 8. Background Monitoring
The application uses Java multithreading to perform background activities, including:

- Disaster monitoring.
- Resource monitoring.
- Evacuation processing.
- Notification services.
- Weather monitoring.

### 9. Role-Based Access
The application includes role-based GUI permissions for:

- ADMIN
- RESCUE_TEAM
- MEDICAL_TEAM

Access to application modules is controlled through the user interface.

## Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Java |
| GUI | Java Swing |
| Database | MySQL |
| Database Connectivity | JDBC |
| Architecture | Layered Architecture |
| Multithreading | Java Threads |
| Background GUI Tasks | SwingWorker |
| IDE | IntelliJ IDEA / NetBeans |
| Build and Dependency Management | Maven |

## System Architecture

The application follows a layered architecture to separate user interface operations, business logic, database operations, and data models.

```text
              USER
                |
                v
       JAVA SWING GUI
                |
                v
        SERVICE LAYER
       (Business Logic)
                |
                v
          DAO LAYER
       (Database Access)
                |
                v
          MYSQL DATABASE
```

### Main Layers

**1. Presentation Layer**

Contains Swing-based graphical components such as:

- MainFrame
- DashboardPanel
- DisasterPanel
- VictimPanel
- ShelterPanel
- ResourcePanel
- EvacuationPanel
- ReportsPanel

**2. Service Layer**

Contains the business logic of the application.

Examples:
- EvacuationService
- EvacuationServiceImpl

**3. DAO Layer**

Handles database operations through JDBC.

Examples:
- DisasterDAO
- VictimDAO
- ShelterDAO
- ResourceDAO
- EvacuationDAO
- ReportDAO

**4. Model Layer**

Contains Java classes representing the application's entities.

Examples:
- Disaster
- Victim
- Shelter
- Resource
- Evacuation

**5. Exception Handling**

Custom exceptions are used to handle application-specific situations.

Examples:
- NoResourceAvailableException
- NoShelterAvailableException
- VictimNotFoundException

## Evacuation Priority Algorithm

The system uses a rule-based scoring mechanism to determine the urgency of evacuation for each victim.

The priority score is calculated using:

**P = V + Z + W + M**

Where:

| Parameter | Description |
|---|---|
| P | Total priority score |
| V | Victim vulnerability score |
| Z | Disaster zone risk score |
| W | Waiting-time score |
| M | Medical condition score |

Medical condition score:

- 5 points if the victim has a medical condition.
- 0 points if the medical condition is recorded as `None`.

A higher priority score indicates a more urgent evacuation requirement.

This is a rule-based algorithm, not a machine learning model.

## Evacuation Workflow

1. Register disaster information.
2. Register victims associated with the disaster.
3. Calculate each victim's priority score.
4. Identify a suitable shelter with available capacity.
5. Check the availability of required resources.
6. Create an evacuation record.
7. Assign the shelter and resource.
8. Update shelter occupancy and resource stock.
9. Maintain the evacuation status.

If a victim, suitable shelter, or required resource is unavailable, the system handles the situation through its exception-handling mechanisms.

## Multithreading Implementation

The system uses background threads to monitor and process application activities.

| Thread / Component | Responsibility |
|---|---|
| DisasterMonitoringThread | Monitors disaster information |
| ResourceMonitoringThread | Monitors resource availability |
| EvacuationProcessingThread | Checks pending evacuation requests |
| NotificationServiceThread | Checks conditions requiring notifications |
| WeatherMonitor | Handles weather-monitoring functionality |

The evacuation processing thread checks pending evacuation records periodically, while the notification service monitors relevant system conditions.

## Database

The project uses **MySQL** as its relational database and JDBC for communication between Java and the database.

The database stores information related to:

- Disasters
- Victims
- Shelters
- Resources
- Evacuations
- Reports and related records

Database connection configuration is handled through the `DBConnection` class.

## Project Structure

The following is the logical organization of the application. Actual package names and folder locations may differ depending on the project configuration.

```text
SmartDisasterEvacuationSystem/
│
├── src/
│   └── main/
│       └── java/
│           ├── model/
│           │   ├── Disaster.java
│           │   ├── Victim.java
│           │   ├── Shelter.java
│           │   ├── Resource.java
│           │   └── Evacuation.java
│           │
│           ├── dao/
│           │   ├── DisasterDAO.java
│           │   ├── VictimDAO.java
│           │   ├── ShelterDAO.java
│           │   ├── ResourceDAO.java
│           │   ├── EvacuationDAO.java
│           │   └── ReportDAO.java
│           │
│           ├── service/
│           │   ├── EvacuationService.java
│           │   └── EvacuationServiceImpl.java
│           │
│           ├── exception/
│           │   ├── NoResourceAvailableException.java
│           │   ├── NoShelterAvailableException.java
│           │   └── VictimNotFoundException.java
│           │
│           ├── monitor/
│           │   ├── SystemMonitor.java
│           │   ├── EvacuationProcessingThread.java
│           │   ├── NotificationServiceThread.java
│           │   └── WeatherMonitor.java
│           │
│           └── gui/
│               ├── MainFrame.java
│               ├── DashboardPanel.java
│               ├── DisasterPanel.java
│               ├── VictimPanel.java
│               ├── ShelterPanel.java
│               ├── ResourcePanel.java
│               ├── EvacuationPanel.java
│               └── ReportsPanel.java
│
├── pom.xml
└── README.md
```

## Installation and Setup

### Prerequisites

Install the following software:

- Java Development Kit (JDK)
- MySQL Server
- MySQL Workbench (optional)
- IntelliJ IDEA or NetBeans
- Maven

### Step 1: Clone the Repository

```bash
git clone https://github.com/adityakarna-png/Smart-Disaster-Evacuation-System.git
```

### Step 2: Open the Project

Open the cloned project folder in IntelliJ IDEA or NetBeans.

If the project uses Maven, allow the IDE to download and resolve the required dependencies.

### Step 3: Configure MySQL

1. Start the MySQL server.
2. Create the project database.
3. Import or execute the SQL database schema provided with the project.
4. Update the database connection details in `DBConnection.java`.

Example configuration:

```java
private static final String URL =
    "jdbc:mysql://localhost:3306/your_database";

private static final String USER = "your_username";

private static final String PASSWORD = "your_password";
```

Replace the example values with your local MySQL configuration.

### Step 4: Configure JDBC

Ensure that MySQL Connector/J is included in the project's Maven dependencies.

### Step 5: Run the Application

Run the project's main Java class from your IDE.

The Swing application should open with the main application window.

## Testing

The project was tested using multiple functional and validation scenarios.

The recorded testing included:

- Disaster record creation.
- Victim registration.
- Priority score calculation.
- Evacuation record creation.
- Shelter and resource allocation.
- Database constraint validation.

The recorded test cases passed.

An invalid disaster ID was also tested to verify that database foreign-key constraints prevent invalid references.

## Current Limitations

- The earthquake/disaster testing workflow uses simulated data rather than a live seismic data feed.
- The priority scoring weights are rule-based and have not been validated by disaster-management experts.
- The application has not undergone large-scale concurrent allocation stress testing.
- Evacuation, shelter, and resource database updates are not yet implemented as one atomic transaction.
- Role-based permissions are enforced at the GUI level and are not a complete server-side security system.
- The application has not yet been validated in real-world disaster-response operations.

## Future Enhancements

- Integrate live disaster and earthquake data APIs.
- Integrate real-time weather information services.
- Introduce GPS-based victim and shelter location tracking.
- Implement map-based evacuation route visualization.
- Add automated route optimization.
- Improve resource allocation using optimization algorithms.
- Implement database transactions for safer allocation operations.
- Strengthen authentication and authorization.
- Perform performance and concurrency testing.
- Develop a mobile application for field rescue teams.

## Course Details

| Detail | Information |
|---|---|
| Course ID | 21CSC203P |
| Course Name | Advanced Programming Practice (APP) |
| Department | Computer Science and Engineering (CSE) |
| Section | F |
| Academic Year | Second Year (2026–2027) |
| Institution | SRM Institute of Science and Technology, Tiruchirappalli |

## Team Members

| S.No. | Full Name | Register Number | Department | Section | Academic Year |
|---|---|---|---|---|---|
| 1 | Aditya Nishant Karna | RA2511003050530 | CSE | F | Second Year |
| 2 | Yugandhar Yadav | RA2511003050528 | CSE | F | Second Year |
| 3 | Rahul Yadav | RA2511003050532 | CSE | F | Second Year |
| 4 | Dharmik Sai | RA2511003050347 | CSE | F | Second Year |

## Mentor Details

| Detail | Information |
|---|---|
| Mentor Name | Dr. S. Shargunam |
| Designation | Assistant Professor (AP) |
| Course | Advanced Programming Practice (APP) |

## Project Information

**Project Title:** Smart Disaster Evacuation & Resource Allocation System

**Project Type:** Academic Java Application

**Institution:** SRM Institute of Science and Technology, Tiruchirappalli
