# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="732" height="805" alt="image" src="https://github.com/user-attachments/assets/98b29e0d-6b1b-4865-af95-21916d80bb14" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Member    |        MemberID ,Membership          |  Store member details     |
|      Trainer  |      TrainerID,Name,Email,PhoneNumber              |     Store Trainer details  |
|  Program      |      ProgramID,Cost              |  Programs like Zumbz/yoga     |
|    Session    |       SessionID,SessionDate             |    Tracks attendance   |
|    Payment    |          PaymentID,Amount          |   Tracks payments by members    |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|       Member-Program       |     M:N       |      Optional(Member),Mandatory(Enrollment)         | Member may or may not join programs      |
|          Trainer-Program    |      M:N      |            Optional(Trainer),Mandatory(Assignment)   |  Trainer may or may not run Programs     |
|       Member–Trainer       |     1:N       |        Mandatory (Session), Optional (Member/Trainer)       |    Session must have a member & trainer   |

### Assumptions
- Program = recurring class; Session = specific instance.
- Payments cover both memberships and sessions.
- A Session links one Member and one Trainer.
 

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="647" height="763" alt="Screenshot 2025-11-14 142501" src="https://github.com/user-attachments/assets/51955ef7-587e-4d1e-9801-c25fedc88be8" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Member    |      MemberID (PK), Name, Address, Phone, Email              |   Library members    |
|      Book  |      BookID (PK), Title, Author, Category, ISBN, PubYear              |    Books in collection   |
|    Loan    |        LoanID (PK), LoanDate, DueDate, ReturnDate, FineAmount, MemberID (FK), BookID (FK)            |     Tracks book borrowing  |
|     Event   |         EventID (PK), Name, Description, EventDate, StartTime, EndTime, RoomID (FK)           |    Library cultural events   |
|    Speaker    |         SpeakerID (PK), Name, Bio, ContactInfo           |    Event speakers/authors   |
|      Booking  |             BookingID (PK), BookingDate, StartTime, EndTime, RoomID (FK), MemberID (FK)       |    Study room reservations   |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|      Member–Book        |       M:N     |        Mandatory for Loan, Optional for Member/Book       |   Members borrow books    |
|    Member–Event          |      M:N      |     Mandatory for Registration, Optional for Member/Event          |   Members register for events    |
|   Event–Speaker  |      M:N      |    Mandatory for EventSpeaker, Optional for Event/Speaker |    Events may have multiple speakers   |
|   Event–Room           |      1:N      |    Mandatory for Event, Optional for Room           |  Each event in one room     |
|  Room–Booking            |      1:N   |      Mandatory for Booking, Optional for Room         |   Rooms booked for study by members    |

### Assumptions
- Overdue fines are stored per Loan record.
- BookCopy not modeled
- Rooms serve both events and study bookings.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="598" height="744" alt="image" src="https://github.com/user-attachments/assets/995c215b-e577-4a7d-bedd-095dc6cef1e9" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Customer    | CustomerID (PK), Name, Email, Phone |  Stores customer info     |
|   Waiter     | WaiterID (PK), Name, Shift, ContactInfo|   Waiter details    |
|    Table    | TableID (PK), TableNumber, Capacity, Location  |Restaurant tables |
|  Reservation   | ReservationID (PK), ReservationDate, ReservationTime, NoOfGuests, Status, CustomerID (FK), TableID (FK) | Table bookings|
| Order       |  OrderID (PK), OrderDate, OrderTime, Status, ReservationID (FK)| Orders linked to reservations|
| Dish       |  DishID (PK), DishName, Description, Price, CategoryID (FK)| Menu items|
|  Bill      | BillID (PK), BillDate, TotalAmount, ServiceCharge, Tax, Status, ReservationID (FK)|Final bill per reservation|
| Assignment       | AssignmentID (PK), WaiterID (FK), ReservationID (FK)|Resolves Waiter–Reservation|

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|  Customer–Reservation            |   1:N         |  Mandatory for Reservation, Optional for Customer             |   One customer can have many reservations    |
|  Reservation–Table            |    1:N        |  Mandatory for Reservation, Optional for Table             |  Each reservation is for one table     |
|   Order–Dish           |      M:N      |    Mandatory for Order_Item, Optional for Order/Dish   |  An order can include many dishes     |
|   Reservation–Bill           |  1:1          | Mandatory for Bill, Optional for Reservation              | One bill per reservation      |
|   Waiter–Reservation           |   M:N         | Mandatory for Assignment, Optional for Waiter/Reservation              | Multiple waiters can serve a reservation      |


### Assumptions
- Walk-in customers are still recorded
- One bill per reservation
- Split payments not modeled; could extend with a Payment entity.


---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
