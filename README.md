# Smart Elevator Control System ER Diagram

Author: Shikhar

## Overview
This ER diagram represents a smart elevator control system designed for large buildings such as offices, malls, hospitals and residential complexes. The system manages multiple buildings, elevators, floors, ride requests, assignments, ride logs, maintenance and status tracking.

The design separates static configuration data from dynamic operational data to ensure scalability and clarity.

## Workflow
The system follows this flow:

Building contains floors and elevators  
Users generate floor requests  
Requests are assigned to elevators  
Elevators execute rides  
Ride logs are stored for history and analysis  
Maintenance and status are tracked separately  

## Entities

### Building
Stores building level information.

Attributes:
- building_id (PK)
- name
- location
- type

### Floor
Represents floors within a building.

Attributes:
- floor_id (PK)
- building_id (FK)
- floor_number
- label

### Elevator_Shaft
Represents shafts inside a building.

Attributes:
- shaft_id (PK)
- building_id (FK)
- shaft_number

### Elevator
Represents elevators operating inside a building.

Attributes:
- elevator_id (PK)
- shaft_id (FK)
- building_id (FK)
- capacity
- current_floor_id (FK)
- status

### Elevator_Floor
Junction table mapping elevators to floors.

Attributes:
- elevator_floor_id (PK)
- elevator_id (FK)
- floor_id (FK)

### Floor_Request
Represents requests generated from floors.

Attributes:
- request_id (PK)
- floor_id (FK)
- direction
- requested_at
- status

### Ride_Assignment
Represents allocation of requests to elevators.

Attributes:
- assignment_id (PK)
- request_id (FK)
- elevator_id (FK)
- assigned_at

### Ride_Log
Stores completed ride information.

Attributes:
- ride_id (PK)
- elevator_id (FK)
- request_id (FK)
- start_floor_id (FK)
- end_floor_id (FK)
- start_time
- end_time

### Maintenance
Tracks maintenance records of elevators.

Attributes:
- maintenance_id (PK)
- elevator_id (FK)
- issue
- start_time
- end_time
- status

### Status_Log
Tracks historical status changes of elevators.

Attributes:
- status_log_id (PK)
- elevator_id (FK)
- status
- recorded_at

## Relationships

- One building has many floors
- One building has many elevators
- One building has many shafts
- One shaft contains one elevator
- One elevator serves many floors and one floor can be served by many elevators through Elevator_Floor
- One floor generates many requests
- One request is assigned to one elevator
- One elevator can handle many assignments
- One request results in one ride log
- One elevator completes many rides
- One elevator can have many maintenance records
- One elevator can have many status logs

## Design Decisions

- Elevator configuration is separated from operational data such as requests and ride logs
- Elevator_Floor is used to model many to many relationships between elevators and floors
- Ride_Assignment separates request generation from elevator allocation logic
- Ride_Log stores historical trip data for analytics
- Maintenance is stored separately to preserve history
- Status_Log tracks dynamic state changes instead of storing them directly in elevator

## Assumptions

- Each building contains multiple elevators and floors
- Each request is handled by one elevator
- Each ride log represents a completed trip
- Maintenance events do not remove historical data
- Status changes are tracked over time

## ER Diagram 

<img width="942" height="826" alt="er diagram " src="https://github.com/user-attachments/assets/1047f9e4-23e1-42e9-a9d7-ad675b37e5a0" />


## Conclusion

This design models a scalable elevator control system with clear separation between configuration, request handling, ride execution and maintenance tracking. It supports real world infrastructure needs and efficient monitoring.
