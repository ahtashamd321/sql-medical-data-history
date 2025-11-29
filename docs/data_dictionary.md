# Hospital SQL Project - Data Dictionary

This document describes all tables, columns, data types, constraints, and meanings used in the Hospital SQL Project.

---

## 1. Table: `patients`

Stores personal and demographic information about patients.

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| `patient_id` | INT | PRIMARY KEY | Unique identifier for each patient |
| `first_name` | VARCHAR(150) | NOT NULL | Patient's first name |
| `last_name` | VARCHAR(150) | NOT NULL | Patient's last name |
| `gender` | CHAR(1) | CHECK (M/F) | Gender: 'M' = Male, 'F' = Female |
| `birth_date` | DATE | | Date of birth |
| `city` | VARCHAR(150) | | City of residence |
| `province_id` | CHAR(2) | FOREIGN KEY → `province_names.province_id` | Province or state code |
| `allergies` | VARCHAR(150) | | Patient's known allergies |
| `height` | DECIMAL(3,0) | | Patient's height in centimeters |
| `weight` | DECIMAL(4,0) | | Patient's weight in kilograms |

---

## 2. Table: `doctors`

Stores information about doctors in the hospital.

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| `doctor_id` | INT | PRIMARY KEY | Unique identifier for each doctor |
| `first_name` | VARCHAR(130) | NOT NULL | Doctor's first name |
| `last_name` | VARCHAR(130) | NOT NULL | Doctor's last name |
| `specialty` | VARCHAR(125) | | Medical specialty of the doctor |

---

## 3. Table: `admissions`

Tracks the admission history of patients.

⚠️ **This table has a composite primary key:** `(patient_id, admission_date)`

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| `patient_id` | INT | PRIMARY KEY, FOREIGN KEY → `patients.patient_id` | Patient who was admitted |
| `admission_date` | DATE | PRIMARY KEY | Date of admission |
| `discharge_date` | DATE | | Date of discharge |
| `diagnosis` | VARCHAR(50) | | Reason for admission |
| `attending_doctor_id` | INT | FOREIGN KEY → `doctors.doctor_id` | Doctor responsible during stay |

---

## 4. Table: `province_names`

Stores standard provincial/state codes linked to patients.

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| `province_id` | CHAR(2) | PRIMARY KEY | Province/state code |
| `province_name` | VARCHAR(30) | NOT NULL | Full name of the province |

---

## Entity Relationship Summary

- **patients** ↔ **province_names**: Many-to-One (via `province_id`)
- **admissions** ↔ **patients**: Many-to-One (via `patient_id`)
- **doctors** ↔ **admissions**: One-to-Many (via `attending_doctor_id`)

---

*This data dictionary serves as the complete reference for the Hospital SQL Project database schema.*