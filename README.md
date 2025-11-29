# Hospital Data SQL Project

This project contains SQL queries and documentation for analyzing the `hospital_data_history` database. The project is completed by a team of 5 members.

---

## 📌 Project Overview

This SQL project focuses on analyzing hospital patient information using four main tables:

- **patients**
- **doctors**
- **admissions**
- **province_names**

The team performed 34 SQL problem queries involving filters, joins, group-by operations, aggregations, updates, and derived columns (BMI, weight groups, etc.). All queries have been tested and are stored in the `queries/` folder.

---

## 👥 Team Members & Responsibilities

| Member | Role | Responsibilities |
|--------|------|------------------|
| **Y.Lokesh** | Database Analyst | Created database schema diagram, data dictionary, analyzed relationships between tables |
| **Kushal Kumar D S** | SQL Developer 1 | Completed SQL queries **Q1–Q12**, tested results |
| **Joseph Allen N.S** | SQL Developer 2 | Completed SQL queries **Q13–Q24**, handled group-by and join logic |
| **SidhendraKp** | SQL Developer 3 | Completed SQL queries **Q25–Q34**, advanced joins and CASE logic |
| **Ahtasham Anjum** | GitHub & Documentation Manager | Managed repo, merged branches, wrote README, maintained folder structure |

---

## 📂 Folder Structure

```
hospital_sql_project/
│
├── data/              # database dump or sample data
├── queries/           # all SQL answers
├── docs/              # schema, data dictionary
├── screenshots/       # output images for verification
└── README.md          # documentation
```

---

## 🗂️ SQL Queries Summary

Queries are grouped into 3 files:

```
queries/
├── Q01_to_Q12.sql
├── Q13_to_Q24.sql
└── Q25_to_Q34.sql
```

Each file contains:
- Clean, formatted SQL
- Comments explaining queries
- Verified output (screenshots in `/screenshots`)

---

## 🧠 Database Documentation

See the `/docs/` folder:

- `data_dictionary.md` — Description of all tables and columns
- `schema_diagram.png` — ER diagram showing relationships
- `project_plan.md` — Team workflow and task distribution

---

## 📊 Data Dictionary – hospital_data_history

### patients

| Column | Type | Description |
|---------------|-----------|-------------|
| patient_id | INT (PK) | Unique patient ID |
| first_name | VARCHAR(150) | Patient's first name |
| last_name | VARCHAR(150) | Patient's last name |
| gender | CHAR(1) | M/F |
| birth_date | DATE | Date of birth |
| city | VARCHAR(150) | City name |
| province_id | CHAR(2) |
| allergies | VARCHAR(150) | Allergy information | 
| height | DECIMAL(3,0) | Height in cm |
| weight | DECIMAL(4,0) | Weight in kg |


### doctors

| Column | Type | Description |
|---------------|-----------|-------------|
| doctor_id | INT (PK) | Unique doctor ID |
| first_name | VARCHAR(130) | Doctor's first name |
| last_name | VARCHAR(130) | Doctor's last name |
| specialty | VARCHAR(125) | Doctor's specialization |

### admissions

| Column | Type | Description |
|---------------------|-----------|-------------|
| patient_id | INT (PK) | Reference to patients |
| admission_date | DATE(PK)| Admission date |
| discharge_date | DATE | Discharge date |
| diagnosis | VARCHAR(50) | Primary diagnosis |
| attending_doctor_id | INT(11)


### province_names

| Column | Type | Description |
|---------------|-----------|-------------|
| province_id | CHAR(2) (PK) | Province identifier |
| province_name | VARCHAR(30) | Full name of province |

---

## 🛠️ Tools Used

- MySQL / PostgreSQL / SQLite (depending on your environment)
- GitHub for version control and collaboration
- DB Browser / Workbench for query testing

---

## 🚀 How to Run the Project

1. Import `hospital_data_history.sql` into MySQL/PostgreSQL.
2. Open the `queries/` folder.
3. Run each `.sql` file in order.
4. Check output screenshots for validation.

---

## ✔️ Project Completed Successfully

All requirements have been met, including:

- ✅ Data exploration
- ✅ 34 SQL problem queries
- ✅ Data dictionary
- ✅ Schema diagram
- ✅ Proper folder structure
- ✅ Team collaboration using Git branches
- ✅ Professional GitHub documentation



