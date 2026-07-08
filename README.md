# Hospital Management App

A beginner-friendly full-stack **Hospital Management System** built with **Node.js, Express, MongoDB Atlas, and Mongoose**.
This project allows users to **register patients, view patient records, search/filter records, update patient details, discharge patients, and delete patient records**.

---

## Features

* Add/register new patients
* View all patients
* View a single patient by ID
* Search patients by **name** or **disease**
* Filter patients by **status** (`Admitted` / `Discharged`)
* Pagination support for patient listing
* Update patient details
* Discharge patients with automatic **discharge date**
* Delete patient records
* MongoDB Atlas integration using **Mongoose**

---

## Tech Stack

### Backend

* **Node.js**
* **Express.js**
* **MongoDB Atlas**
* **Mongoose**
* **CORS**

### Frontend

* React.js (if connected separately)
* Vite (if frontend is built using Vite)

---

## Project Structure

```bash
project-folder/
│
├── backend/
│   └── index.js
│
├── frontend/
│   ├── src/
│   └── ...
│
└── README.md
```

---

## Backend Overview

The backend is built using **Express** and connects to **MongoDB Atlas** using **Mongoose**.

### Main API File

* `backend/index.js`

### Database

* MongoDB Atlas
* Collection stores hospital patient records

---

## Patient Schema

Each patient record contains the following fields:

| Field            | Type        | Description                                      |
| ---------------- | ----------- | ------------------------------------------------ |
| `name`           | String      | Patient name                                     |
| `age`            | Number      | Patient age                                      |
| `gender`         | String      | Male / Female / Other                            |
| `disease`        | String      | Disease or health issue                          |
| `doctorAssigned` | String      | Doctor assigned to patient                       |
| `roomNumber`     | String      | Room number of patient                           |
| `status`         | String      | `Admitted` or `Discharged`                       |
| `admissionDate`  | Date        | Automatically stores admission date              |
| `dischargeDate`  | Date / null | Stores discharge date when patient is discharged |

---

# API Endpoints

## 1. Register a New Patient

**POST** `/patients`

### Request Body

```json
{
  "name": "Rahul Patil",
  "age": 25,
  "gender": "Male",
  "disease": "Fever",
  "doctorAssigned": "Dr. Sharma",
  "roomNumber": "A-101"
}
```

### Response

```json
{
  "_id": "64f1234567890abc12345678",
  "name": "Rahul Patil",
  "age": 25,
  "gender": "Male",
  "disease": "Fever",
  "doctorAssigned": "Dr. Sharma",
  "roomNumber": "A-101",
  "status": "Admitted",
  "admissionDate": "2026-07-08T10:00:00.000Z",
  "dischargeDate": null
}
```

---

## 2. Get All Patients

**GET** `/patients`

Supports:

* pagination
* search
* status filter

### Example

```bash
GET /patients?page=1&limit=5&search=fever&status=Admitted
```

### Query Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| `page`    | Page number                          |
| `limit`   | Number of records per page           |
| `search`  | Search by patient name or disease    |
| `status`  | Filter by `Admitted` or `Discharged` |

### Response

```json
{
  "data": [],
  "page": 1,
  "limit": 5,
  "total": 0,
  "totalPages": 1
}
```

---

## 3. Get Single Patient by ID

**GET** `/patients/:id`

### Example

```bash
GET /patients/64f1234567890abc12345678
```

---

## 4. Update Patient Details

**PUT** `/patients/:id`

Used to:

* edit patient details
* change room number
* change doctor assigned
* discharge patient
* re-admit patient

### Example Request Body

```json
{
  "status": "Discharged"
}
```

### Important Logic

* If patient status becomes **Discharged**, `dischargeDate` is automatically set.
* If patient status becomes **Admitted** again, `dischargeDate` is cleared.

---

## 5. Delete Patient

**DELETE** `/patients/:id`

### Example

```bash
DELETE /patients/64f1234567890abc12345678
```

---

# Validation Rules

The following fields are required while creating a patient:

* `name`
* `age`
* `gender`
* `disease`
* `doctorAssigned`

Additional rules:

* `age` must be greater than `0`
* `gender` must be one of:

  * `Male`
  * `Female`
  * `Other`
* `status` must be either:

  * `Admitted`
  * `Discharged`

---

# Installation and Setup

## 1. Clone the Project

```bash
git clone <your-repository-link>
cd hospital-management-app
```

## 2. Install Backend Dependencies

Go to the backend folder and install packages:

```bash
cd backend
npm install express cors mongoose
```

## 3. Run the Backend Server

```bash
node index.js
```

If everything works correctly, you should see:

```bash
Connected to MongoDB Atlas
Server running on http://localhost:5000
```

---

# MongoDB Connection

This project uses **MongoDB Atlas** with a hardcoded connection string inside `index.js`.

Example:

```js
const MONGODB_URI =
  'mongodb+srv://username:password@cluster.mongodb.net/';
```

> Note: In real projects, it is better to store database credentials in a `.env` file for security.

---

# Example Testing Using Postman

You can test all endpoints using **Postman**.

## Sample Patient JSON

```json
{
  "name": "Anjali Desai",
  "age": 32,
  "gender": "Female",
  "disease": "Typhoid",
  "doctorAssigned": "Dr. Kulkarni",
  "roomNumber": "B-203"
}
```

### Test Cases

* Add a patient using **POST**
* Fetch all patients using **GET**
* Search for a patient using `search=Typhoid`
* Filter admitted patients using `status=Admitted`
* Update a patient using **PUT**
* Discharge a patient using `status: "Discharged"`
* Delete a patient using **DELETE**

---

# Sample Workflow

1. Start the server
2. Add a new patient
3. Open `/patients` to see all records
4. Search for a patient by name or disease
5. Update room number or doctor
6. Discharge the patient
7. Delete the patient if needed

---

# Future Improvements

You can extend this project by adding:

* Frontend UI for patient management
* Authentication for admin/staff login
* Doctor management module
* Appointment booking system
* Billing system
* Dashboard with charts
* Export patient reports
* File upload for medical documents

---

# Learning Outcomes

By building this project, you can learn:

* How to create REST APIs using Express
* How to connect Node.js with MongoDB Atlas
* How to use Mongoose schemas and models
* How to perform CRUD operations
* How to implement search, filter, and pagination
* How to handle request validation
* How to structure a beginner-friendly backend project

---

# Author

**Hospital Management App**
Built for learning full-stack development with **Express + MongoDB Atlas + React**.
