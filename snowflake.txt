-- Create database and schema
CREATE DATABASE IF NOT EXISTS salary;
USE DATABASE salary;

USE SCHEMA analysis;

CREATE TABLE employee_data (
    Positions VARCHAR,
    Location VARCHAR,
    Gender VARCHAR,
    Education VARCHAR,
    Experience INT,
    Salary INT
);


-- Step 2: Create a File Format
CREATE OR REPLACE FILE FORMAT CSV_FORMAT 
TYPE = 'CSV' 
FIELD_OPTIONALLY_ENCLOSED_BY = '"' 
SKIP_HEADER = 1;

-- Step 3: Create Stages for Files
CREATE OR REPLACE STAGE highestpaidjobs
URL = 's3://highestpaidjobs/output_file.csv'
CREDENTIALS = (AWS_KEY_ID = ' ');


LIST @highestpaidjobs;

-- Step 5: Copy Data into Tables
COPY INTO employee_data
FROM @highestpaidjobs
FILE_FORMAT = (FORMAT_NAME = CSV_FORMAT);



SELECT * FROM employee_data LIMIT 10;

SELECT * FROM employee_data;
-- 1
SELECT 
    AVG(Salary) AS Average_Salary
FROM 
    employee_data
WHERE 
    Education = 'DIPLOMA';
    
-- 2 
SELECT 
    AVG(Salary) AS Average_Salary
FROM 
    employee_data
WHERE 
    Education IN ('B.Tech/B.E.', 'BCA','B.COM', 'B.SC');  

-- 3
SELECT 
    Positions, 
    MAX(Salary) AS Highest_Salary
FROM 
    employee_data
GROUP BY 
    Positions
ORDER BY 
    Highest_Salary DESC;

-- 4 
SELECT 
    Positions, 
    Salary
FROM 
    employee_data
WHERE 
    Salary = (SELECT MIN(Salary) FROM employee_data);

--5 
WITH HighestPaid AS (
    SELECT 
        Positions, 
        MAX(Salary) AS Highest_Salary
    FROM 
        employee_data
    GROUP BY 
        Positions
    ORDER BY 
        Highest_Salary DESC
)
SELECT 
    LP.Positions AS Current_Position,
    LP.Salary AS Current_Salary,
    HP.Positions AS Suggested_Position,
    HP.Highest_Salary AS Potential_Salary
FROM 
    (SELECT Positions, Salary FROM employee_data WHERE Salary = (SELECT MIN(Salary) FROM employee_data)) LP
CROSS JOIN 
    (SELECT Positions, Highest_Salary FROM HighestPaid LIMIT 3) HP;

--
WITH HighestPaid AS (
    SELECT 
        Positions, 
        Education,
        MAX(Salary) AS Highest_Salary
    FROM 
        employee_data
    GROUP BY 
        Positions, Education
    ORDER BY 
        Highest_Salary DESC
)
SELECT 
    LP.Positions AS Current_Position,
    LP.Education AS Current_Education,
    LP.Salary AS Current_Salary,
    HP.Positions AS Suggested_Position,
    HP.Education AS Suggested_Education,
    HP.Highest_Salary AS Potential_Salary
FROM 
    (SELECT Positions, Education, Salary 
     FROM employee_data
     WHERE Salary = (SELECT MIN(Salary) FROM employee_data)) LP
CROSS JOIN 
    (SELECT Positions, Education, Highest_Salary 
     FROM HighestPaid 
     LIMIT 3) HP;


     



