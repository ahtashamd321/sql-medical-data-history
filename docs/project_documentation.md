# Hospital Management Database System – Project Documentation

## 1. Cover Page

**Project Title:** Hospital Management Database System – SQL Analysis Project  
**Course/Department:** —  Certified Data Analyst
**Prepared By:** Team Members (Ahtasham Anjum, Y.Lokesh, Joseph Allen N.S, Kushal Kumar D S, Sidhendra KP)   
**Date:** — 28-11-2025

---

## 2. Table of Contents

1. Project Overview
2. Database Overview
3. ER Diagram (Structure Explanation)
4. Data Dictionary
5. SQL Queries (Q1–Q34)
6. Team Roles & Workflow
7. Conclusion
8. References

---

## 3. Project Overview

This project is based on the **hospital_data_history** database which contains medical records, patient details, doctor information, and admission history. The goal is to perform **34 SQL tasks** involving data filtering, aggregation, joins, grouping, and data cleaning.

The project is designed to help understand database relationships and perform analytical queries in SQL.

---

## 4. Database Overview

The database contains four main tables:

- **patients** – Stores personal, physical, and medical details of each patient.
- **doctors** – Contains information about hospital doctors.
- **admissions** – Tracks hospital admissions, diagnosis, and associated doctor.
- **province_names** – Contains province IDs and their full province names.

---

## 5. Database Schema / ER Diagram (Explanation)

### Relationships:

- **patients (1) → admissions (many)** using `patient_id`
- **doctors (1) → admissions (many)** using `doctor_id`
- **province_names (1) → patients (many)** using `province_id`

**This means:**
- A patient can have multiple admissions.
- A doctor may treat multiple patients.
- A province can have multiple patients.

---

## 6. Data Dictionary

### `patients` table

| Column       | Type    | Description                    |
|--------------|---------|--------------------------------|
| patient_id   | INT     | Unique patient identifier      |
| first_name   | VARCHAR | Patient's first name           |
| last_name    | VARCHAR | Patient's last name            |
| gender       | CHAR    | M or F                         |
| birth_date   | DATE    | Date of birth                  |
| city         | VARCHAR | Patient's city                 |
| province_id  | CHAR    | FK → province_names            |
| allergies    | VARCHAR | Allergies or NULL              |
| height       | INT     | Height in cm                   |
| weight       | INT     | Weight in kg                   |

### `doctors` table

| Column       | Type    | Description                    |
|--------------|---------|--------------------------------|
| doctor_id    | INT     | Unique doctor identifier       |
| first_name   | VARCHAR | Doctor first name              |
| last_name    | VARCHAR | Doctor last name               |
| specialty    | VARCHAR | Medical specialty              |

### `admissions` table

| Column               | Type    | Description                    |
|----------------------|---------|--------------------------------|
| patient_id           | INT     | FK → patients                  |
| admission_date       | DATE    | Date admitted                  |
| discharge_date       | DATE    | Date discharged                |
| diagnosis            | VARCHAR | Diagnosis information          |
| attending_doctor_id  | INT     | FK → doctors                   |

### `province_names` table

| Column         | Type    | Description                    |
|----------------|---------|--------------------------------|
| province_id    | CHAR    | Province abbreviation          |
| province_name  | VARCHAR | Full name of province          |

---

## 7. SQL Queries (All 34 Requirements)

Below is the list placeholder for the SQL queries. You will paste the final tested SQL queries here.

### Q1–Q33 SQL Queries:

```sql
-- 1. Show first name, last name, and gender of patients who's gender is 'M' 
SELECT first_name, last_name, gender 
FROM patients 
WHERE gender = 'M';

-- 2. Show first name and last name of patients who does not have allergies. 
SELECT first_name, last_name, allergies
FROM patients
WHERE allergies IS NULL;

-- 3. Show first name of patients that start with the letter 'C' 
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';

-- 4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive) 
SELECT first_name, last_name, weight
FROM patients
WHERE weight BETWEEN 100 AND 120;

-- 5. Update the patients table for the allergies column. If the patient's allergies is 
-- null then replace it with 'NKA' 
UPDATE patients
SET allergies ='NKA'
WHERE allergies IS NULL;

-- 6. Show first name and last name concatenated into one column to show their full name.
SELECT CONCAT(first_name, last_name) AS full_name
FROM patients;


-- 7. Show first name, last name, and the full province name of each patient
SELECT p.first_name, 
	   p.last_name,
       pn.province_name
FROM patients AS p
INNER JOIN province_names AS pn
	ON p.province_id = pn.province_id;

-- 8. Show how many patients have a birth_date with 2010 as the birth year. 
SELECT COUNT(patient_id) AS total_patient
FROM patients
WHERE YEAR(birth_date) = 2010; 

-- 9. Show the first_name, last_name, and height of the patient with the greatest height. 
SELECT first_name, last_name, height
FROM patients
ORDER BY height DESC LIMIT 1;

-- 10. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000 
SELECT * FROM patients
WHERE patient_id IN(1,45,534,879,1000);

-- 11. Show the total number of admissions 
SELECT COUNT(*) AS total_admission
FROM admissions;

-- 12. Show all the columns from admissions where the patient was admitted and 
-- discharged on the same day. 
SELECT * 
FROM admissions
WHERE admission_date = discharge_date;

-- 13. Show the total number of admissions for patient_id 579. 
SELECT COUNT(*) 
FROM admissions
WHERE patient_id = 579;

-- 14. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?
SELECT DISTINCT(city)
FROM patients
WHERE province_id = 'NS';

-- 15. Write a query to find the first_name, last name and birth date of patients 
-- who have height more than 160 and weight more than 70
SELECT first_name, last_name, birth_date
FROM patients
WHERE height > 160 
	AND weight > 70;

-- 16. Show unique birth years from patients and order them by ascending. 
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year ASC;

-- 17. Show unique first names from the patients table which only occurs once in the list.
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) =1;

-- 18. Show patient_id and first_name from patients where their first_name start 
-- and ends with 's' and is at least 6 characters long.
SELECT patient_id, first_name
FROM patients
WHERE first_name LIKE 'S%'
	AND first_name LIKE '%S'
AND LENGTH(first_name) >= 6;

-- 19. Show patient_id, first_name, last_name from patients whos diagnosis is 
-- 'Dementia'.   Primary diagnosis is stored in the admissions table.
SELECT p.patient_id,
	   p.first_name,
       p.last_name,
       a.diagnosis
FROM patients AS p
INNER JOIN admissions AS a
	ON p.patient_id = a.patient_id
WHERE a.diagnosis ="Dementia";

-- 20. Display every patient's first_name. Order the list by the length of each name 
-- and then by alphbetically.
SELECT first_name
FROM patients
ORDER BY LENGTH(first_name) ASC,
		first_name ASC;

-- 21. Show the total amount of male patients and the total amount of female 
-- patients in the patients table. Display the two results in the same row.
SELECT
	SUM(gender = "M") AS male_count,
    SUM(gender = "F") AS female_count
FROM patients;

-- 22. Show patient_id, diagnosis from admissions. Find patients admitted 
-- multiple times for the same diagnosis.
SELECT patient_id,
	   diagnosis
FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(*) > 1;

-- 23. Show patient_id, diagnosis from admissions. Find patients admitted 
-- multiple times for the same diagnosis.
SELECT patient_id,
	   diagnosis
FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(*) > 1;

-- 24. Show the city and the total number of patients in the city. Order from most 
-- to least patients and then by city name ascending.
SELECT city, COUNT(patient_id) total_patient
FROM patients
GROUP BY city
ORDER BY total_patient DESC,
		city ASC;

-- 25. Show first name, last name and role of every person that is either patient or 
-- doctor. The roles are either "Patient" or "Doctor" 
SELECT first_name, last_name, 'patient' AS role
FROM patients

UNION ALL

SELECT first_name, last_name, 'doctor' AS role
FROM doctors;

--- 26. Show all allergies ordered by popularity. Remove NULL values from query. 
SELECT allergies, COUNT(*) AS total_patients
FROM patients
WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY total_patients DESC;

-- 27. Show all patient's first_name, last_name, and birth_date who were born in 
-- the 1970s decade. Sort the list starting from the earliest birth_date.
SELECT first_name, last_name, birth_date
FROM patients
WHERE birth_date BETWEEN '1970-01-01' AND '1979-12-31'
ORDER BY birth_date ASC;

-- 28. We want to display each patient's full name in a single column. Their 
-- last_name in all upper letters must appear first, then first_name in all lower case 
-- letters. Separate the last_name and first_name with a comma. Order the list by 
-- the first_name in decending order    
SELECT CONCAT(UCASE(last_name), ',', LCASE(first_name)) AS full_name
FROM patients
ORDER BY first_name DESC;

-- 29. Show the province_id(s), sum of height; where the total sum of its patient's 
-- height is greater than or equal to 7,000.
SELECT province_id, SUM(height) AS total_height
FROM patients
GROUP BY province_id
HAVING SUM(height) >= 7000;

-- 30. Show the difference between the largest weight and smallest weight for 
-- patients with the last name 'Maroni' 
SELECT
	  (SELECT MAX(weight) FROM patients WHERE last_name = 'Maroni') -
      (SELECT MIN(weight) FROM patients WHERE last_name = 'Maroni')
AS weight_difference;

-- 31 Show all of the days of the month (1-31) and how many admission_dates 
-- occurred on that day. Sort by the day with most admissions to least admissions. 
SELECT 
    DAY(admission_date) AS day_of_month, 
    COUNT(*) AS total_admissions
FROM admissions
GROUP BY DAY(admission_date)
ORDER BY day_of_month;

-- 32. Show all of the patients grouped into weight groups. Show the total amount 
-- of patients in each weight group. Order the list by the weight group decending. 
SELECT 
    FLOOR(weight / 10) * 10 AS weight_group,
    COUNT(*) AS total_patients
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;

--  33. Show patient_id, weight, height, isObese from the patients table. Display 
-- isObese as a boolean 0 or 1. Obese is defined as weight(kg)/(height(m). Weight 
-- is in units kg. Height is in units cm.
SELECT 
    patient_id,
    weight,
    height,
    (weight / ((height / 100) * (height / 100)) >= 30) AS isObese
FROM patients;

-- 34. Show patient_id, first_name, last_name, and attending doctor's specialty. 
-- Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first 
-- name is 'Lisa'. 
SELECT p.patient_id,
	   p.first_name,
       p.last_name,
       a.diagnosis,
       d.specialty,
       d.first_name
FROM patients AS p
JOIN admissions AS a
	ON p.patient_id = a.patient_id
JOIN doctors AS d
	On a.doctor_id = d.doctor_id
WHERE diagnosis = 'Epilepsy'
	AND d.first_name = 'Lisa';

---

## 8. Team Roles & Workflow

### **Member A – Database Analyst**
- Created ER diagram
- Understood relationships
- Built data dictionary

### **Member B – SQL Developer (Queries 1–12)**
- Basic select, filtering queries

### **Member C – SQL Developer (Queries 13–24)**
- Grouping, HAVING, counting, joins

### **Member D – SQL Developer (Queries 25–34)**
- Advanced logic, CASE, analytics

### **Member E – GitHub & Documentation Manager (You)**
- Created GitHub repository structure
- Added queries folder & documentation
- Merged all team SQL results
- Maintained clean version control
- Wrote README and full documentation (this file)

---

## 9. Conclusion

This SQL project improved understanding of:

- Relational databases
- SQL joins, filters, aggregations
- Data cleaning and transformation
- Query optimization
- Collaborative work with GitHub

The queries provide insights into patient demographics, doctor specialties, diagnoses, city distribution, and admission behaviors.

---
