# Student Information System (SIS)

**Greenfield University Student Information System** is an enterprise-grade, full-stack academic management web application built with **Node.js**, **Express.js**, **SQLite**, and vanilla **HTML5 / CSS3 / JavaScript (ES6+)**.

---

## 1. System Overview

- **Architecture:** Modular Object-Oriented Architecture (Models, Controllers, Services, Middleware, Routes, SQLite storage).
- **Authentication:** Secure session-based auth via SQLite session store, bcrypt password hashing (cost factor 12), and role-based access control (RBAC).
- **Database:** Normalized SQLite database with 23 tables, foreign key constraints, indexes, triggers, and automated schema migrations.
- **Frontend:** Responsive Single-Page Application (SPA) with Light and Dark themes, Lucide icons, Chart.js analytics, modal dialogs, and mobile-responsive sidebar.
- **Roles:**
  1. **Administrator:** Complete institutional management (students, faculty, departments, courses, fees, exams, announcements, settings).
  2. **Faculty:** Authorized course lists, daily attendance entry, assignment creation & grading, study material uploads, marks entry.
  3. **Student:** Profile view, real-time attendance percentage & alerts, timetable, published examination results, assignment submissions, digital study materials, fee balances & printable receipts.

---

## 2. Technology Stack

- **Runtime:** Node.js (v20+ or v22+ / v24+ supported)
- **Backend Framework:** Express.js 4.x
- **Database:** SQLite (using built-in `node:sqlite` DatabaseSync — **no XAMPP, MySQL, or native C++ compiler needed**)
- **Session Store:** SQLite-backed session store with automatic session expiration
- **Security:** Helmet CSP headers, Express rate limiting, bcryptjs hashing, audit logging
- **File Uploads:** Multer with file-type whitelisting and UUID-based secure storage
- **Frontend:** Vanilla HTML5, CSS3 Custom Properties (Design System), Modular ES6 JavaScript
- **Visualization:** Chart.js 4.x for enrollment and attendance trend analytics
- **Icons:** Lucide Icons

---

## 3. Quick Start & Setup Guide (Windows & VS Code)

### Prerequisites

- [Node.js](https://nodejs.org/) installed (v20.x, v22.x, or v24.x recommended).
- [Visual Studio Code](https://code.visualstudio.com/) or any text editor.
- **No external database server (XAMPP / MySQL) required!** The entire database is self-contained in a single SQLite file.

### Step-by-Step Installation

1. **Open the project folder in VS Code:**
   ```powershell
   cd C:\Users\Asokan\.gemini\antigravity\scratch\sis
   code .
   ```

2. **Configure Environment:**
   A default `.env` file is pre-configured. If needed, copy `.env.example` to `.env`:
   ```powershell
   cp .env.example .env
   ```

3. **Install Dependencies:**
   ```powershell
   npm install
   ```

4. **Seed the Database with Demo Data:**
   Initialize all 23 database tables, academic years, departments, courses, faculty, students, fees, exams, and attendance records:
   ```powershell
   npm run seed
   ```

5. **Start the Application:**
   ```powershell
   npm start
   ```
   For development with auto-reload:
   ```powershell
   npm run dev
   ```

6. **Access in Browser:**
   Open [http://localhost:3000](http://localhost:3000)

---

## 4. Default Demo Credentials

| Role | Username | Password | Notes |
| :--- | :--- | :--- | :--- |
| **Administrator** | `admin` | `Admin@1234` | Full institutional access |
| **Faculty** | `anikasharma` | `Faculty@1234` | Head of CSE / Professor |
| **Student** | `aaravsingh` | `Student@1234` | B.Tech CSE Student (Sem 5) |

*(Additional faculty logins: `rahulverma`, `priyanair`, `arjunpatel`, `meerakrishnan` with `Faculty@1234`)*

---

## 5. Running Automated Tests

Run the comprehensive Jest & Supertest test suite (covering authentication, session cookies, RBAC authorization, and API modules):
```powershell
npm test
```

All 22 test cases will run against the SQLite database and verify:
- Invalid credentials rejection
- Successful login & HttpOnly session cookie assignment
- RBAC permissions (e.g., student forbidden from creating students or entering marks)
- Academic and administrative endpoint data delivery

---

## 6. Directory Structure

```
sis/
├── docs/
│   └── OOAD_DOCUMENTATION.md      # Full OOAD report (UML diagrams, SOLID, ERD)
├── public/
│   ├── css/
│   │   └── main.css               # Complete responsive design system & dark theme
│   ├── js/
│   │   ├── api.js                 # Central fetch wrapper for all API endpoints
│   │   ├── utils.js               # Toast, confirm modal, dates, badges, helpers
│   │   ├── auth.js                # Login, logout, session state management
│   │   ├── app.js                 # SPA client-side router & navigation
│   │   ├── dashboard.js           # Charts & role-specific metric cards
│   │   ├── students.js            # Student directory, CRUD, profile view
│   │   ├── faculty.js             # Faculty directory, subject assignments
│   │   ├── departments.js         # Departments, degree courses, syllabus subjects
│   │   ├── attendance.js          # Daily attendance marking, session records
│   │   ├── examinations.js        # Exam scheduler, hall allocation, mark entry
│   │   ├── results.js             # Result sheets, grade calculations, print view
│   │   ├── fees.js                # Fee ledger, payments, printable receipts
│   │   ├── timetable.js           # Weekly timetable grid with conflict detection
│   │   ├── assignments.js         # Assignment creation, submission & grading
│   │   ├── materials.js           # Digital learning repository (PDFs, slides)
│   │   ├── announcements.js       # Campus notice board & circulars
│   │   ├── notifications.js       # Notification panel & real-time polling
│   │   ├── profile.js             # User account profile, settings, academic years
│   │   └── reports.js             # Institutional analytics & CSV/print reports
│   ├── uploads/                   # Uploaded photos, assignments & materials
│   └── index.html                 # Main Single-Page Application shell
├── server/
│   ├── app.js                     # Express app setup, security, route mounting
│   ├── config/
│   │   ├── database.js            # SQLite database initialization & transaction wrapper
│   │   ├── dbHelpers.js           # Query result normalizers
│   │   └── sessionStore.js        # Pure SQLite session store for express-session
│   ├── controllers/               # API route controllers
│   ├── db/
│   │   ├── schema.sql             # Complete 23-table SQLite schema & triggers
│   │   └── seed.js                # Realistic demo data generation script
│   ├── middleware/                # Auth, RBAC, Rate Limiting, Multer, Audit Log
│   ├── models/                    # Object-Oriented domain entities
│   ├── routes/                    # Express route definitions
│   └── services/                  # Business logic services (Auth, Attendance, Reports)
├── tests/
│   └── api.test.js                # Automated Jest API test suite
├── .env.example
├── package.json
└── README.md
```

---

## 7. Key Features Implemented

1. **Academic Management:** Department, degree course, and subject curriculum configuration with credit allocation and faculty assignments.
2. **Attendance Management:** Daily attendance entry with Present, Absent, and Late markers; percentage calculations; low attendance alerts (<75%).
3. **Examinations & Results:** Exam scheduling, maximum and passing marks, automatic percentage and letter grade calculation (A+, A, B, C, D, F), publish control, and printable mark sheets.
4. **Fee Management:** Tuition and exam fee structures, student ledger tracking, partial payments, and printable payment receipts.
5. **Timetable:** Weekly visual schedule with conflict detection preventing double-booking of faculty and classrooms.
6. **Assignments & Materials:** Faculty assignment postings, student submissions, grading with feedback, and digital study material repository.
7. **Announcements & Notifications:** Targeted broadcasts (all, student, faculty), pinned notices, unread badges, and polling notification center.
8. **Institutional Reports:** Interactive Chart.js graphs for enrollment, attendance trends, examination pass/fail rates, fee recovery, and assignments.
9. **UI/UX Design:** High-contrast accessible color palette, fluid mobile navigation, theme switcher (Light / Dark mode), loading spinners, and empty states.

---

## 8. Troubleshooting

- **Database file locked or read-only:** Ensure the server is not running in multiple terminal windows simultaneously. The SQLite database is located at `./server/db/sis.db`.
- **Port 3000 already in use:** Edit `.env` and change `PORT=3000` to `PORT=3001` or another available port.
- **Node version warnings:** Node.js v20+ or v22+ has full built-in SQLite support (`node:sqlite`). If using older Node versions (<20), please upgrade to the current LTS release.
#   S t u d e n t - I n f o r m a t i o n - S y s t e m  
 