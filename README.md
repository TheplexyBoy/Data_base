# PostgreSQL & pgAdmin 4 Basic Guide

## Introduction

This project is a basic guide to learn how to use PostgreSQL and pgAdmin 4 on Ubuntu Linux. It explains how to install PostgreSQL and pgAdmin 4, start the local server, create a database, clean an Excel file before importing it, import CSV files, create tables, manage data, and write simple SQL queries.

The purpose of this guide is to understand the basic workflow when working with databases. The explanations are simple because this guide is intended for beginners.

---

# Table of Contents

1. Installing PostgreSQL and pgAdmin 4
2. Starting the PostgreSQL Local Server
3. Creating a Database in pgAdmin 4
4. Cleaning an Excel File
5. Importing a CSV File into pgAdmin 4
6. Creating and Modifying Tables
7. SQL Commands (CRUD)
8. INNER JOIN
9. Basic SQL Queries
10. Final Notes

---

# 1. Installing PostgreSQL and pgAdmin 4

## Step 1 - Update Ubuntu

Open the Terminal and update your system.

```bash
sudo apt update
sudo apt upgrade
```

---

## Step 2 - Install PostgreSQL

Run the following command:

```bash
sudo apt install postgresql postgresql-contrib
```

Press **Y** if Ubuntu asks for confirmation.

---

## Step 3 - Install pgAdmin 4

Go to the official pgAdmin website and download the version for Ubuntu.

https://www.pgadmin.org/download/

Follow the installation instructions shown on the website.

---

## Step 4 - Open pgAdmin 4

After installing it, open pgAdmin 4 from the Applications menu.

The first time you open it, it will ask you to create a **Master Password**.

This password is only used to access pgAdmin.

---

# 2. Starting the PostgreSQL Local Server

Normally PostgreSQL starts automatically after installation.

To check if it is running:

```bash
sudo systemctl status postgresql
```

If the service is stopped:

```bash
sudo systemctl start postgresql
```

To enable PostgreSQL every time Ubuntu starts:

```bash
sudo systemctl enable postgresql
```

Now open pgAdmin 4.

You should see your local server on the left panel.

If it does not appear, you can register a new server using your PostgreSQL username and password.

---

# 3. Creating a Database in pgAdmin 4

1. Open pgAdmin 4.
2. Connect to the local server.
3. Expand **Servers**.
4. Expand **Databases**.
5. Right-click **Databases**.
6. Select **Create → Database**.
7. Enter the database name.

Example:

```
sales_database
```

8. Click **Save**.

Your database is now ready to use.

---

# 4. Cleaning an Excel File

Before importing any data, it is a good practice to clean the Excel file.

## Remove Duplicates

1. Select all the data.
2. Go to **Data**.
3. Click **Remove Duplicates**.
4. Click **OK**.

---

## Use Filters

1. Select the entire table.
2. Go to **Data**.
3. Click **Filter**.

Use the filters to check if there are incorrect values.

---

## Remove Blank Rows

Use the filters to find empty cells.

If an entire row has missing information, delete it.

If only one value is missing and you know the correct value, complete it.

---

## Check the Data

Verify that:

* Numbers are numeric.
* Dates have the same format.
* Names do not contain extra spaces.
* There are no typing mistakes.
* There are no special characters that should not be there.

---

## Rename the Columns

Column names should be simple.

Example:

Good:

```
customer_name
```

Bad:

```
Customer Name!!!
```

---

## Save as CSV

When everything is ready:

**File → Save As**

Choose:

```
CSV UTF-8
```

UTF-8 is recommended because it supports special characters correctly.

---

# 5. Importing a CSV File into pgAdmin 4

Before importing the CSV, make sure that your table already exists.

## Import Steps

1. Right-click the table.
2. Select **Import/Export Data**.

Configure the following options.

### Import

```
Import
```

### Filename

Select your CSV file.

### Format

```
CSV
```

### Encoding

```
UTF8
```

### Header

Enable the **Header** option.

This tells PostgreSQL that the first row contains the column names.

### Delimiter

Usually:

```
,
```

or

```
;
```

depending on how the CSV was created.

Finally, click **OK**.

---

# 6. Creating and Modifying Tables

## Create a Table

Right-click **Tables**.

Select:

```
Create → Table
```

Enter the table name.

Next, go to the **Columns** tab.

Create each column by specifying:

* Column Name
* Data Type
* Length (if needed)
* Primary Key (if needed)
* Not Null (optional)

Example:

| Column     | Data Type    |
| ---------- | ------------ |
| id         | SERIAL       |
| first_name | VARCHAR(100) |
| last_name  | VARCHAR(100) |
| age        | INTEGER      |
| city       | VARCHAR(100) |

Click **Save**.

---

## Add a New Column

```sql
ALTER TABLE students
ADD COLUMN email VARCHAR(100);
```

---

## Modify a Column

```sql
ALTER TABLE students
ALTER COLUMN age TYPE SMALLINT;
```

---

## Delete a Column

```sql
ALTER TABLE students
DROP COLUMN email;
```

---

# 7. SQL Commands (CRUD)

## Create Data (INSERT)

```sql
INSERT INTO students(first_name, last_name, age, city)
VALUES
('Andres','Quintero',19,'Barranquilla');
```

---

## Read Data (SELECT)

```sql
SELECT *
FROM students;
```

---

## Update Data (UPDATE)

```sql
UPDATE students
SET city='Cartagena'
WHERE id=1;
```

---

## Delete Data (DELETE)

```sql
DELETE FROM students
WHERE id=1;
```

---

# 8. INNER JOIN

Suppose we have these two tables.

### Students

| id | first_name |
| -- | ---------- |

### Courses

| student_id | course_name |
| ---------- | ----------- |

We can combine both tables using an INNER JOIN.

```sql
SELECT
students.first_name,
courses.course_name
FROM students
INNER JOIN courses
ON students.id = courses.student_id;
```

This query only returns the rows that exist in both tables.

---

# 9. Basic SQL Queries

## Show All Records

```sql
SELECT *
FROM students;
```

---

## Show Only One Column

```sql
SELECT first_name
FROM students;
```

---

## Search by a Condition

```sql
SELECT *
FROM students
WHERE city='Barranquilla';
```

---

## Sort the Results

```sql
SELECT *
FROM students
ORDER BY age;
```

---

## Count Records

```sql
SELECT COUNT(*)
FROM students;
```

---

## Average Value

```sql
SELECT AVG(age)
FROM students;
```

---

## Maximum Value

```sql
SELECT MAX(age)
FROM students;
```

---

## Minimum Value

```sql
SELECT MIN(age)
FROM students;
```

---

## Filter Using LIKE

```sql
SELECT *
FROM students
WHERE first_name LIKE 'A%';
```

This query returns every student whose name starts with the letter **A**.

---

# 10. Final Notes

This guide explains the basic steps to work with PostgreSQL and pgAdmin 4 using Ubuntu Linux.

Before importing any CSV file, it is always a good idea to clean the data in Excel to avoid import errors. Using filters, removing duplicates, checking blank cells, and saving the file as UTF-8 can make the process much easier.

Learning SQL takes practice. The best way to improve is by creating tables, inserting data, updating records, deleting information, and writing different queries until the syntax becomes familiar.
