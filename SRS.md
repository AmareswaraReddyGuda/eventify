# Software Requirements Specification (SRS)
### Project: Eventify
### Version: 1.0
### Date: November 2025
### Prepared by: Team Eventify

---

## 1. Introduction

### 1.1 Purpose
This document defines the functional and non-functional requirements for **Eventify**, a minimal event management portal designed for college campuses.  
The portal allows students to discover and register for events, receive QR-based tickets, and enables organizers to manage event attendance digitally.

### 1.2 Scope
Eventify will:
- Provide event discovery and one-click registration for students.  
- Generate unique QR tickets for each registration.  
- Enable organizers to scan and mark attendance through a browser-based scanner.  
- Offer a dashboard for organizers to view registration and attendance metrics.

The system will be lightweight, web-based, and accessible from desktops and mobile browsers.

### 1.3 Intended Audience
- **Students** – for browsing and registering for events.  
- **Organizers / Faculty** – for creating and managing events and tracking attendance.  
- **Mentors / Reviewers** – for evaluating project progress and outcomes.

---

## 2. Overall Description

### 2.1 Product Perspective
Eventify is an independent web application built with Flask and MySQL, using server-side rendering (Jinja2 + Bootstrap).  
It follows a simple client-server architecture:
- Frontend: HTML/CSS/Bootstrap templates.
- Backend: Flask (Python).
- Database: MySQL for persistent storage.

### 2.2 Product Functions
1. **User Authentication**
   - Signup/Login for students and organizers.
   - Password hashing and validation.
2. **Event Management**
   - Organizer can create, edit, and delete events.
   - Each event has a name, date, capacity, and description.
3. **Registration & Ticketing**
   - Students can register for available events.
   - System generates a unique QR ticket.
4. **QR Code Scanning**
   - Organizer scans QR using `html5-qrcode` to mark attendance.
5. **Dashboard**
   - Organizers can view registration count, attendance %, and event details.

### 2.3 User Classes and Characteristics
| User Type | Role | Description |
|------------|------|-------------|
| Student | End User | Browse and register for events. |
| Organizer | Admin | Create events, scan tickets, view dashboard. |
| Reviewer | Viewer | Mentor or evaluator to review progress. |

### 2.4 Operating Environment
- **Frontend:** HTML5, CSS3, Bootstrap 5  
- **Backend:** Python 3.10+, Flask  
- **Database:** MySQL 8.x  
- **Browser Support:** Chrome, Edge, Firefox  
- **Deployment:** Localhost (development), Render/Railway (production)

### 2.5 Design and Implementation Constraints
- Use Flask (Python) with MySQL.  
- Use `qrcode` for QR generation and `html5-qrcode` for scanning.  
- Minimal use of JavaScript frameworks.  
- Project duration: 8 weeks (college + office workload considered).

---

## 3. Functional Requirements

### FR1. User Authentication
- Users can create an account (Student/Organizer).
- Passwords are stored securely (hashed).
- Login and logout functionality provided.

### FR2. Event Management
- Organizer can add, update, and delete events.
- Each event has:
  - Event ID
  - Name
  - Description
  - Date & Time
  - Capacity
  - Organizer ID

### FR3. Registration
- Students can register for events.
- Capacity check before registration.
- Confirmation email (optional).

### FR4. QR Ticket Generation
- Each successful registration generates a QR PNG.
- QR code encodes event ID + user ID + registration ID.

### FR5. Attendance Scanning
- Organizer uses browser camera to scan QR tickets.
- Attendance marked as “present” in the database.

### FR6. Dashboard
- Organizer dashboard shows:
  - Total registrations
  - Attended count
  - Attendance percentage

---

## 4. Non-Functional Requirements

### 4.1 Performance
- QR scan and response < 2 seconds on stable connection.  
- Support 100+ concurrent registrations per event.

### 4.2 Security
- Use hashed passwords (`werkzeug.security`).  
- Validate user sessions via Flask-Login.  
- Prevent duplicate registrations.

### 4.3 Usability
- Clean and responsive UI (Bootstrap).  
- Compatible on mobile and desktop browsers.

### 4.4 Reliability
- MySQL ensures persistence.  
- Flask error handlers to manage invalid operations.

### 4.5 Scalability
- Future enhancement: deploy to cloud (Render/Railway).  
- Optional features like email reminders and event analytics.

---

## 5. Database Design (Summary)
| Table | Description |
|--------|--------------|
| users | Stores user info (id, name, email, role, password_hash) |
| events | Stores event details (id, name, description, capacity, date) |
| registrations | Stores registration info (id, user_id, event_id, qr_code, attendance_status) |

*(Detailed ERD diagram in `docs/ERD.png`)*

---

## 6. External Interfaces
- **Email API** – SMTP (proof-of-concept email confirmation).  
- **QR Scanning** – `html5-qrcode` JavaScript library.  
- **Database** – MySQL via SQLAlchemy ORM.

---

## 7. Future Enhancements
- Email reminders before 24 hours of event.  
- Event feedback and ratings.  
- Student leaderboard for most event participation.  
- Admin panel for overall statistics.

---

## 8. References
- Flask Documentation: https://flask.palletsprojects.com/  
- SQLAlchemy: https://docs.sqlalchemy.org/  
- html5-qrcode: https://github.com/mebjas/html5-qrcode  
- Bootstrap: https://getbootstrap.com/  
- Python qrcode library: https://pypi.org/project/qrcode/

---

