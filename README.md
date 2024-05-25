# 📚 Week 6B

## 🤖 Advanced SQL Queries for Robot Data

### Creating the Robot Database
```sql
CREATE DATABASE robot_db;
USE robot_db;

CREATE TABLE robots (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  model VARCHAR(50),
  category VARCHAR(50),
  price DECIMAL(10, 2),
  weight DECIMAL(6, 2),
  battery_capacity INT
);

CREATE TABLE components (
  id INT PRIMARY KEY,
  robot_id INT,
  component_name VARCHAR(50),
  component_type VARCHAR(50),
  FOREIGN KEY (robot_id) REFERENCES robots(id)
);

CREATE TABLE maintenance_logs (
  id INT PRIMARY KEY,
  robot_id INT,
  maintenance_date DATE,
  description VARCHAR(200),
  FOREIGN KEY (robot_id) REFERENCES robots(id)
);

INSERT INTO robots (id, name, model, category, price, weight, battery_capacity)
VALUES
  (1, 'RoboMaid', 'RM-100', 'Household', 999.99, 5.5, 5000),
  (2, 'RoboChef', 'RC-200', 'Culinary', 1499.99, 8.2, 7500),
  (3, 'RoboGuard', 'RG-300', 'Security', 2999.99, 12.8, 10000),
  (4, 'RoboMedic', 'RM-400', 'Medical', 4999.99, 6.3, 6000),
  (5, 'RoboBuilder', 'RB-500', 'Construction', 3499.99, 15.6, 12000);

INSERT INTO components (id, robot_id, component_name, component_type)
VALUES
  (1, 1, 'Vacuum Pump', 'Cleaning'),
  (2, 1, 'Brushes', 'Cleaning'),
  (3, 2, 'Knife Attachment', 'Culinary'),
  (4, 2, 'Induction Cooktop', 'Culinary'),
  (5, 3, 'Surveillance Camera', 'Security'),
  (6, 3, 'Motion Sensors', 'Security'),
  (7, 4, 'Surgical Laser', 'Medical'),
  (8, 4, 'Vital Signs Monitor', 'Medical'),
  (9, 5, 'Welding Torch', 'Construction'),
  (10, 5, 'Hydraulic Arm', 'Construction');

INSERT INTO maintenance_logs (id, robot_id, maintenance_date, description)
VALUES
  (1, 1, '2023-01-15', 'Replaced vacuum pump'),
  (2, 2, '2023-02-10', 'Recalibrated knife attachment'),
  (3, 3, '2023-03-05', 'Upgraded motion sensors'),
  (4, 4, '2023-04-20', 'Performed laser alignment'),
  (5, 5, '2023-05-12', 'Replaced welding torch nozzle'),
  (6, 1, '2023-06-01', 'Cleaned brush assembly'),
  (7, 2, '2023-07-18', 'Replaced induction cooktop'),
  (8, 3, '2023-08-22', 'Updated surveillance camera firmware'),
  (9, 4, '2023-09-08', 'Recalibrated vital signs monitor'),
  (10, 5, '2023-10-30', 'Serviced hydraulic arm');
```



### Aggregation Functions in SQL
- **What are Aggregation Functions?**
  - Aggregation functions perform calculations on a set of values and return a single result.
  - Common aggregation functions include COUNT, SUM, AVG, MIN, and MAX.

### Using Aggregation Functions with Robot Data
- **Example:** Counting the number of robots in the inventory
  ```sql
  SELECT COUNT(*) FROM robots;
  ```

- **Example:** Calculating the average price of robots
  ```sql
  SELECT AVG(price) FROM robots;
  ```

- **MIN/MAX:**
  - The `MIN()`/`MAX()` aggregate function returns the lowest value (minimum)/highest value (maximum) in a set of non-NULL values.
  - Example: `SELECT MIN(price), MAX(price) FROM robots;`

- **GROUP BY:**
  - The `GROUP BY` clause allows you to arrange the rows of a query in groups. The groups are determined by the columns that you specify in the `GROUP BY` clause.
  - Example: `SELECT category, COUNT(*) FROM robots GROUP BY category;`

- **HAVING:**
  - The `HAVING` clause is often used with the `GROUP BY` clause to filter groups based on a specified list of conditions.
  - Example: `SELECT category, AVG(price) FROM robots GROUP BY category HAVING AVG(price) > 2000;`

- **LIKE:**
  - `LIKE` determines if a string matches a pattern.
  - `LIKE` supports two wildcard options: `%` and `_`.
  - `LIKE` is used when only a fragment of a text value is known.
  - Example: `SELECT * FROM robots WHERE name LIKE 'Robo%';`

- **BETWEEN:**
  - `BETWEEN` returns values within a given range.
  - `BETWEEN` is a shorthand for `>=` and `<=`.
  - `BETWEEN` is inclusive, i.e., begin and end values are included.
  - Example: `SELECT * FROM robots WHERE price BETWEEN 1000 AND 3000;`

- **AND/OR:**
  - `AND` requires that two conditions are true.
  - `OR` requires that one of two conditions is true.
  - Example: `SELECT * FROM robots WHERE category = 'Household' AND price < 1500;`

- **WHERE:**
  - The `WHERE` clause is used to filter records based on specified conditions.
  - Example: `SELECT * FROM robots WHERE weight > 10;`

- **ORDER BY:**
  - The `ORDER BY` clause returns the rows in the given sort order.
  - Rows can be returned in ascending or descending sort order. (ASC, DESC)
  - Example: `SELECT * FROM robots ORDER BY price DESC;`

- **DISTINCT:**
  - `DISTINCT` returns unique values (without duplicates).
  - `DISTINCT` operates on a single column.
  - Example: `SELECT DISTINCT category FROM robots;`


### 💡 Discussion
- Discuss the benefits of using SQL functions and clauses for data analysis in the context of superhero mission management.
- Explore how these functions and clauses can help in resource allocation, performance evaluation, and pattern identification for superheroes.

## 🌟 Hands-on Practice: Building the Superhero Database

In this section, you will have the opportunity to practice your SQL skills by creating and populating the superhero database. Follow the requirements below to build the database and tables.

### Database Requirements

1. Create a database named `superhero_db`.

2. Create a table named `superheroes` with the following columns:
   - `id` (INT): Primary key to uniquely identify each superhero.
   - `name` (VARCHAR(50)): Name of the superhero.
   - `superpower` (VARCHAR(100)): The main superpower of the superhero.
   - `city` (VARCHAR(50)): The city where the superhero primarily operates.

3. Create a table named `missions` with the following columns:
   - `id` (INT): Primary key to uniquely identify each mission.
   - `superhero_id` (INT): Foreign key referencing the `id` column in the `superheroes` table.
   - `mission_name` (VARCHAR(100)): Name or title of the mission.
   - `start_date` (DATE): Start date of the mission.
   - `end_date` (DATE): End date of the mission.

4. Insert sample data into the `superheroes` table with at least 5 superheroes.

5. Insert sample data into the `missions` table with at least 10 missions, ensuring that each superhero has at least one mission assigned.

### 🎨 Practical Exercise: Analyzing Superhero Missions with SQL Functions and Clauses
- **Task:** Use SQL functions and clauses to gain insights into superhero mission data.
- **Instructions:**
  - Write a query to find the superhero with the maximum number of missions.
  - Calculate the average duration of missions for each superhero using the `AVG` function and `GROUP BY` clause.
  - Determine the longest and shortest missions using the `MIN` and `MAX` functions.
  - Find the total number of missions per city using the `COUNT` function and `GROUP BY` clause.
  - Retrieve the names of superheroes whose names start with 'Super' using the `LIKE` operator.
  - Find the missions that occurred between two specific dates using the `BETWEEN` operator.
  - Retrieve the details of superheroes who operate in 'New York' and have a superpower related to 'strength' using the `AND` operator.
  - Filter the missions to include only those where the duration is greater than 5 days using the `WHERE` clause.
  - Sort the superheroes based on their total number of missions in descending order using the `ORDER BY` clause.
  - Retrieve the distinct cities where superheroes operate using the `DISTINCT` keyword.

### 💡 Discussion
- Discuss the benefits of using SQL functions and clauses for data analysis in the context of superhero mission management.
- Explore how these functions and clauses can help in resource allocation, performance evaluation, and pattern identification for superheroes.
## 🔗 Joining Tables for Comprehensive Robot Information

### Understanding Joins in SQL
- **What are Joins?**
  - Joins are used to combine rows from two or more tables based on a related column between them.
  - They allow you to retrieve data from multiple tables in a single query.

### Types of Joins
- **INNER JOIN:**
  - Returns only the rows where there is a match in both tables.
  - Example: `SELECT * FROM robots INNER JOIN components ON robots.id = components.robot_id;`

- **LEFT JOIN:**
  - Returns all rows from the left table and the matching rows from the right table.
  - Example: `SELECT * FROM robots LEFT JOIN components ON robots.id = components.robot_id;`

- **RIGHT JOIN:**
  - Returns all rows from the right table and the matching rows from the left table.
  - Example: `SELECT * FROM robots RIGHT JOIN components ON robots.id = components.robot_id;`

### 🌍 Practical Exercise: Joining Superhero Tables for Comprehensive Information
- **Task:** Use joins to combine data from multiple tables and retrieve comprehensive information about superheroes and their missions.
- **Instructions:**
  - Write a query to join the superheroes and missions tables to display the superhero names along with their corresponding mission details.
  - Perform a left join between the superheroes and missions tables to include all superheroes, even if they don't have assigned missions.
  - Join the superheroes and cities tables to show the city each superhero operates in.

### 💡 Discussion
- Discuss the importance of using joins in retrieving data from multiple tables.
- Explore scenarios where different types of joins (inner, left, right) are appropriate in the context of superhero data analysis.

## 🔍 Subqueries and Complex Queries

### Understanding Subqueries
- **What are Subqueries?**
  - Subqueries are queries nested within another query.
  - They allow you to use the result of one query as input for another query.

### Using Subqueries with Robot Data
- **Example:** Finding robots that have a price higher than the average price
  ```sql
  SELECT * FROM robots
  WHERE price > (SELECT AVG(price) FROM robots);
  ```

### Complex Queries
- **Example:** Retrieving robots with their latest maintenance record
  ```sql
  SELECT r.name, m.maintenance_date, m.description
  FROM robots r
  INNER JOIN (
    SELECT robot_id, MAX(maintenance_date) AS latest_date
    FROM maintenance_logs
    GROUP BY robot_id
  ) latest_logs ON r.id = latest_logs.robot_id
  INNER JOIN maintenance_logs m ON r.id = m.robot_id AND latest_logs.latest_date = m.maintenance_date;
  ```

### 🧩 Practical Project: Superhero Performance Analysis

### Project Description
- Develop a set of SQL queries to analyze the performance and mission records of superheroes.
- The queries should provide insights into superhero efficiency, mission patterns, and city coverage.

### Project Requirements
- Use aggregation functions to calculate metrics such as average mission duration, total missions per superhero, and mission success rates.
- Join multiple tables to retrieve comprehensive information about superheroes, their missions, and the cities they operate in.
- Utilize subqueries and complex queries to generate reports on superhero performance and identify areas for improvement.

### 🚀 Implementation Steps
- Step 1: Write queries using aggregation functions to calculate key performance metrics for superheroes and missions.
- Step 2: Join the superheroes, missions, and cities tables to retrieve detailed information about each superhero's mission history and city coverage.
- Step 3: Use subqueries to filter superheroes based on performance criteria, such as mission success rate above a certain threshold or mission frequency within a specific timeframe.
- Step 4: Construct complex queries to generate reports on superhero performance, mission patterns, and city coverage.
- Step 5: Analyze the query results to identify trends, strengths, and areas for improvement in superhero mission management.

### 💡 Discussion
- Discuss how advanced SQL queries, including aggregation functions, joins, subqueries, and complex queries, can be leveraged to gain valuable insights from superhero mission data.
- Explore the potential impact of data-driven decision-making on superhero performance evaluation, mission planning, and resource allocation in the context of the practical project.