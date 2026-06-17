# Student Enrollment Form — JsonPowerDB Micro Project

[![JsonPowerDB](https://img.shields.io/badge/Database-JsonPowerDB-orange)](http://login2explore.com/jpdb)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()
[![License](https://img.shields.io/badge/License-MIT-blue)]()

---

## Table of Contents

1. [Description](#description)
2. [Benefits of Using JsonPowerDB](#benefits-of-using-jsonpowerdb)
3. [Illustrations](#illustrations)
4. [Scope of Functionalities](#scope-of-functionalities)
5. [Examples of Use](#examples-of-use)
6. [Project Status](#project-status)
7. [Release History](#release-history)
8. [Technologies Used](#technologies-used)
9. [Database Design](#database-design)
10. [Form Behaviour](#form-behaviour)
11. [How to Run](#how-to-run)
12. [Sources](#sources)

---

## Description

A web-based **Student Enrollment Form** micro project built using **HTML, CSS, JavaScript**, and **JsonPowerDB (JPDB)** as the backend database. The form allows school administrators to enroll new students and update existing student records stored in the `STUDENT-TABLE` relation of the `SCHOOL-DB` database.

The form follows a strict state-driven behaviour:
- On page load, only the primary key field (Roll No.) is active.
- Entering a Roll No. automatically detects whether the student exists and switches between **Insert mode** and **Update mode**.
- All data is validated before any database operation is performed.
- Three control buttons — `[Save]`, `[Update]`, and `[Reset]` — manage the entire workflow.

**Input Fields:** Roll No. · Full Name · Class · Birth Date · Address · Enrollment Date

**Primary Key:** Roll No.

---

## Benefits of Using JsonPowerDB

JsonPowerDB is a real-time, high-performance, lightweight, and easy-to-use database that provides a simple REST API for all database operations. Below are the key benefits that make it ideal for this project:

| Benefit | Details |
|---|---|
| **Simple REST API** | All CRUD operations (GET, PUT, UPDATE, REMOVE) are performed via simple HTTP requests — no complex SQL queries or ORM setup needed. |
| **Schema-free** | JsonPowerDB stores data as JSON documents, so no rigid schema definition is required. Fields can be added without altering a table structure. |
| **Multi-mode database** | Supports Key-Value store, Document store, Time-series, GeoSpatial, and RDBMS modes in a single product. |
| **Serverless ready** | Works directly from the browser or any client using REST calls — no dedicated backend server is needed. |
| **Real-time data** | Changes are reflected immediately without requiring page reloads or complex polling mechanisms. |
| **Built-in token authentication** | Secure connection token (`connection-token`) ensures only authorised clients can access the database. |
| **Minimal configuration** | Zero setup overhead — no installation, no driver, no ORM. Just a connection token and a base URL. |
| **High performance** | JsonPowerDB is built on PowerIndeX (PIX), an in-memory data processing engine, delivering very fast read/write speeds. |
| **Free to use** | JsonPowerDB provides a free tier via [Login2Explore](http://login2explore.com) for student and micro projects. |
| **Ideal for micro projects** | Lightweight nature and REST-based interface make it perfect for college and school-level micro projects without infrastructure complexity. |

---

## Illustrations

### Form State — Initial (Page Load)

```
┌─────────────────────────────────────────────────┐
│  🎓  Student Enrollment  │  STUDENT-TABLE·SCHOOL-DB │
├─────────────────────────────────────────────────┤
│  Roll No.*  [ __________________ ]  ← cursor    │
│                                                  │
│  Full Name  [ ░░░░░░░░░░░░░░░░░░ ] (disabled)   │
│  Class      [ ░░░░░ ]  Birth Date [ ░░░░░░░░ ]  │
│  Address    [ ░░░░░░░░░░░░░░░░░░ ] (disabled)   │
│  Enroll Date[ ░░░░░░░░ ]          (disabled)    │
│                                                  │
│         [Reset░] [Save░] [Update░]  ← disabled  │
└─────────────────────────────────────────────────┘
```

### Form State — New Student (Roll No. not found)

```
┌─────────────────────────────────────────────────┐
│  🟢 New Student                                  │
├─────────────────────────────────────────────────┤
│  Roll No.*  [ 2024001            ]  (locked)    │
│                                                  │
│  Full Name  [ __________________ ]  ← cursor    │
│  Class      [ ______ ]  Birth Date [ ________ ] │
│  Address    [ ____________________]             │
│  Enroll Date[ ________ ]                        │
│                                                  │
│         [Reset✓] [Save✓] [Update░]              │
└─────────────────────────────────────────────────┘
```

### Form State — Existing Student (Roll No. found)

```
┌─────────────────────────────────────────────────┐
│  🟣 Existing Record                              │
├─────────────────────────────────────────────────┤
│  Roll No.*  [ 2024001            ]  (disabled)  │
│                                                  │
│  Full Name  [ Rohit Sharma       ]  ← cursor    │
│  Class      [ 10-A   ]  Birth Date [ 2008-05-12]│
│  Address    [ 45, MG Road, Pune  ]              │
│  Enroll Date[ 2024-06-01 ]                      │
│                                                  │
│         [Reset✓] [Save░] [Update✓]              │
└─────────────────────────────────────────────────┘
```

---

## Scope of Functionalities

| Functionality | Supported |
|---|---|
| Enroll a new student (Insert) | ✅ |
| Retrieve existing student by Roll No. | ✅ |
| Update existing student record | ✅ |
| Field-level empty validation | ✅ |
| Auto-switch between Save / Update mode | ✅ |
| Disable primary key after record is loaded | ✅ |
| Reset form to initial state | ✅ |
| Live table preview of all records | ✅ |
| Persistent data storage via JsonPowerDB | ✅ |
| Delete a student record | ❌ (out of scope for this micro project) |
| Search / filter records | ❌ (out of scope) |
| Bulk import | ❌ (out of scope) |

---

## Examples of Use

### Enrolling a New Student

1. Open the form in a browser.
2. Enter Roll No. `2024005` and press **Enter**.
3. The system checks STUDENT-TABLE — Roll No. not found.
4. `[Save]` and `[Reset]` buttons are enabled. Cursor moves to **Full Name**.
5. Fill in: Full Name = `Priya Desai`, Class = `9-B`, Birth Date = `2009-03-22`, Address = `12, Shivaji Nagar, Pune`, Enrollment Date = `2024-06-15`.
6. Click `[Save]` — record is saved to JsonPowerDB. Form resets.

### Updating an Existing Student

1. Enter Roll No. `2024005` and press **Enter**.
2. The system finds the record and loads it into the form.
3. `[Update]` and `[Reset]` are enabled. Roll No. field is locked.
4. Change **Class** from `9-B` to `9-C`.
5. Click `[Update]` — record is updated in JsonPowerDB. Form resets.

### JsonPowerDB API Call — Save Record (PUT)

```javascript
function saveStudent(rollNo, data) {
  const request = {
    token: "<your-connection-token>",
    cmd: "PUT",
    dbName: "SCHOOL-DB",
    rel: "STUDENT-TABLE",
    jsonStr: {
      "Roll-No": rollNo,
      "Full-Name": data.fullName,
      "Class": data.cls,
      "Birth-Date": data.birthDate,
      "Address": data.address,
      "Enrollment-Date": data.enrollDate
    }
  };

  fetch("http://api.login2explore.com:5577/api/irl", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(request)
  }).then(res => res.json()).then(console.log);
}
```

### JsonPowerDB API Call — Get Record (GET by Key)

```javascript
function getStudent(rollNo) {
  const request = {
    token: "<your-connection-token>",
    cmd: "GET_BY_KEY",
    dbName: "SCHOOL-DB",
    rel: "STUDENT-TABLE",
    jsonStr: { "Roll-No": rollNo }
  };

  return fetch("http://api.login2explore.com:5577/api/irl", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(request)
  }).then(res => res.json());
}
```

---

## Project Status

**Status: Active — v1.0 Complete**

The core micro project is fully implemented and functional. All required features from the project specification are working:

- [x] Student enrollment form with 6 input fields
- [x] Primary key lookup (Roll No.)
- [x] Insert mode for new students
- [x] Update mode for existing students
- [x] Field validation (no empty fields allowed)
- [x] Save, Update, Reset button logic
- [x] JsonPowerDB integration for persistent storage
- [x] Live record table preview

---

## Release History

| Version | Date | Description |
|---|---|---|
| **v1.0** | June 2025 | Initial release — Student Enrollment Form with JsonPowerDB integration. Full Save/Update/Reset flow, field validation, and live record preview. |
| **v0.2** | May 2025 | Beta — Form UI complete with state-driven enable/disable logic. Storage wired to browser localStorage for testing. |
| **v0.1** | May 2025 | Alpha — Static HTML form scaffold. No database integration. |

> **GitHub Repository:** [https://github.com/your-username/student-enrollment-jsonpowerdb](https://github.com/your-username/student-enrollment-jsonpowerdb)
>
> *(Replace `your-username` with your actual GitHub username before publishing.)*

---

## Technologies Used

| Technology | Version | Purpose |
|---|---|---|
| HTML5 | 5 | Page structure and form layout |
| CSS3 | 3 | Styling and responsive design |
| JavaScript | ES6+ | Form logic, validation, state management |
| JsonPowerDB (JPDB) | 2.0 | Backend NoSQL database via REST API |
| Login2Explore API | v5577 | JsonPowerDB cloud endpoint |
| Bootstrap *(optional)* | 5.x | Responsive UI framework |

---

## Database Design

**Database:** `SCHOOL-DB`  
**Relation / Table:** `STUDENT-TABLE`  
**Primary Key:** `Roll-No`

```json
{
  "Roll-No": "2024001",
  "Full-Name": "Rohit Sharma",
  "Class": "10-A",
  "Birth-Date": "2008-05-12",
  "Address": "45, MG Road, Pune",
  "Enrollment-Date": "2024-06-01"
}
```

JsonPowerDB stores each student as a JSON document, indexed by `Roll-No` as the primary key.

---

## Form Behaviour

### State Machine

```
[Page Load]
     │
     ▼
[Initial State]
 Roll No. active | All other fields disabled | All buttons disabled
     │
     ▼ (User types Roll No. + presses Enter)
     │
     ├── Not in DB ──► [Insert Mode]
     │                  Save + Reset enabled
     │                  Fill all fields → click [Save] → PUT to JPDB → Initial State
     │
     └── Found in DB ─► [Update Mode]
                         Update + Reset enabled | Roll No. locked
                         Edit fields → click [Update] → UPDATE in JPDB → Initial State
                         OR click [Reset] → Initial State
```

---

## How to Run

1. Clone or download this repository.
2. Sign up at [Login2Explore](http://login2explore.com) and obtain your **connection token**.
3. Replace `<your-connection-token>` in `index.html` with your actual token.
4. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari).
5. No server setup needed — all API calls go directly to the JsonPowerDB cloud endpoint.

---

## Sources

- [JsonPowerDB Official Documentation](http://login2explore.com/jpdb/docs.html)
- [Login2Explore — JsonPowerDB Portal](http://login2explore.com)
- [JsonPowerDB REST API Reference](http://api.login2explore.com:5577)
- [README Template by dbader](https://github.com/dbader/readme-template)
- [Shields.io — Badge Generator](https://shields.io)

---

## Other Information

- This project was developed as a **micro project** for a Database Management / Web Technology course.
- JsonPowerDB is used as the primary backend because it requires no server-side programming and is directly accessible from the browser via REST.
- The form design follows the exact specification provided in the micro project guidelines — three buttons, primary key lookup, and state-driven field enabling.

---

*Micro Project · Database Forms · Engineering / Diploma Program*
