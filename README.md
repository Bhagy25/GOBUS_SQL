# 🚌 GoBus — Bus Ticket Booking & Management System

> A unified, database-driven platform that manages the end-to-end bus travel experience — from route planning and seat booking to passenger management and ticket generation.


---

## 📖 About the Project

GoBus is a relational database-backed bus booking system designed to digitize and streamline the entire lifecycle of bus travel in India. It serves three types of stakeholders:

- **Passengers** — search routes, select seats, book tickets, and get a PNR
- **Operators** — manage their fleet, schedule trips, and assign drivers/conductors
- **Administrators** — manage routes, stations, and system-wide data

> *"Every day, crores of Indians travel by bus. But most still buy tickets at a counter, on paper, with no digital record of who they are or which seat they're sitting in. GoBus exists to change that."*

---

## 🔴 Problem Statement

Traditional bus travel in India remains largely manual and fragmented:

- Passengers visit physical counters, stand in long queues, and carry paper tickets that can be lost or forged
- Operators have no centralized system to manage their fleet, drivers, or seat occupancy
- There is no unified platform linking route data, bus schedules, passenger records, and payment in one place

**GoBus solves this by providing a complete, normalized relational database system that connects every part of the bus travel ecosystem.**

---

## ✅ Features

### For Passengers
- Search available trips by route and date
- View seat availability with seat type (AC / sleeper / general)
- Book tickets for multiple passengers in a single booking
- Get a unique PNR for every ticket
- Referral system — refer friends and earn rewards

### For Operators
- Register buses with type, registration number, and seat configuration
- Schedule trips on specific routes with departure date and time
- Assign drivers and conductors to each trip
- Track journey status (scheduled / in-progress / completed / cancelled)

### For the System
- Route and station management with stop-wise duration tracking
- Multi-passenger booking with individual seat assignment
- Passenger profiles with type (adult / child / senior), DOB, and gender
- Payment and booking status tracking

---

## 🏗️ System Architecture

```
Operator
   └── owns → Bus
                └── has → Seats
                └── assigned to → Trip
                                    └── travels on → Route
                                    └── passes through → Stations

User
   └── makes → Booking
                  └── for → Trip
                  └── issues → Ticket (PNR)
                                  └── linked to → Passengers
                                                      └── assigned → Seats
```

---

## 🗄️ Database Schema

### Tables Overview

| Table | Primary Key | Description |
|---|---|---|
| `Station` | Station_ID | Bus stations with address and city |
| `Route` | Route_ID | Named routes |
| `Route_Station` | Route_ID + Station_ID | Stops on each route with duration |
| `Operator` | Operator_ID | Bus operators / companies |
| `Bus` | Bus_ID | Buses owned by operators |
| `Seat` | Seat_ID | Individual seats per bus |
| `Trip` | Bus_ID + Departure_Date_Time | Scheduled trips |
| `User` | User_ID | Registered users with referral |
| `Booking` | Booking_ID | Booking transactions |
| `Ticket` | PNR | Travel tickets linked to bookings |
| `Passenger` | Passenger_ID | Individual travellers |
| `Passenger_Ticket` | Passenger_ID + PNR | Links passengers to tickets |
| `Passenger_Seat` | Seat_ID + Passenger_ID | Links passengers to seats |

---

### Key Relationships

- One **Operator** can own many **Buses**
- One **Bus** can have many **Seats** and run many **Trips**
- One **Route** passes through many **Stations** (via Route_Station)
- One **Trip** = one Bus + one Route + one Departure Date/Time
- One **Booking** is made by one **User** for one **Trip**
- One **Booking** issues one **Ticket** (PNR)
- One **Ticket** can be shared by many **Passengers** (group booking)
- Each **Passenger** is assigned a specific **Seat**

---

## 📊 ER Diagram

> See `/docs/ER_Diagram.png` for the full Entity-Relationship diagram.

Key entities and their cardinalities:

- Station **N** ←→ **M** Route (many-to-many via Route_Station)
- Bus **1** ←→ **N** Seat
- Bus **1** ←→ **N** Trip
- Operator **1** ←→ **N** Bus
- User **1** ←→ **N** Booking
- Booking **1** ←→ **1** Ticket
- Passenger **M** ←→ **N** Seat (via Passenger_Seat)
- Passenger **M** ←→ **N** Ticket (via Passenger_Ticket)
- User **1** ←→ **N** User (self-referential referral)

---

## 📦 Modules

### 1. Route & Station Module
Manages all physical stations and the routes that connect them. Stores stop number and duration from source for each station on a route, enabling arrival time calculation at intermediate stops.

### 2. Operator & Bus Module
Operators register their details and add their buses to the system. Each bus is configured with its total seats, bus type, and registration number. Individual seat records are created per bus.

### 3. Trip Scheduling Module
Admins or operators schedule trips by assigning a bus to a route on a specific date and time. Each trip records the assigned driver, conductor, and current journey status.

### 4. User & Referral Module
Users register with basic details. The referral system tracks who referred each user via a self-referential foreign key (`Referral_User_ID`), enabling reward and discount logic.

### 5. Booking & Payment Module
Users make bookings for a specific trip. Each booking records the date, amount paid, booking status, and payment status.

### 6. Ticket & PNR Module
Every confirmed booking generates a unique PNR-based ticket. The ticket stores total seats and is linked to the booking. Individual passengers and their seat assignments are stored separately.

### 7. Passenger Module
Each traveller on a booking is recorded as a passenger with their own profile — name, type, gender, DOB, and email. Passengers are linked to their ticket (Passenger_Ticket) and their seat (Passenger_Seat).

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Database | MySQL / PostgreSQL |
| Schema Design | Normalized Relational Model (3NF) |
| Diagramming | ER Diagram + Relational Schema |
| Documentation | Markdown |

> *This project is currently a database design and schema project. Application layer (frontend/backend) is planned for future development.*

---

## 🚀 Future Enhancements

- [ ] Driver and Conductor tables with license and rating records
- [ ] Dynamic pricing based on demand and seat type
- [ ] Real-time seat locking to prevent double-booking
- [ ] GPS-based live trip tracking and journey status updates
- [ ] Route demand analytics and revenue reporting
- [ ] Mobile app with PNR tracking and delay notifications
- [ ] Third-party API layer for aggregator integration
- [ ] Corporate bulk booking accounts

---

## 👥 Team

**Project:** GoBus — Bus Ticket Booking & Management System  
**Course:** Database Management Systems (DBMS)  
**Institution:** <!-- Add your college name -->  

| Name | Role |
|---|---|
| <!-- Name 1 --> | ER Diagram & Schema Design |
| <!-- Name 2 --> | Relational Model & Normalization |
| <!-- Name 3 --> | Documentation & Presentation |

---

## 📄 License

This project was developed for academic purposes as part of a DBMS course project.

---

<p align="center">Made with ❤️ for DBMS | GoBus Project</p>
