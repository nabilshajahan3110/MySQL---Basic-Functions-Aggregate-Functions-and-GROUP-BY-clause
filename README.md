# DAY 18 and DAY 19 - Challenge 16 and 18

# BASIC SQL QUERIES, AGGREGATE FUNCTIONS AND GROUP BY CLAUSE

Created by NABIL SHAJAHAN

As part of a 75-day data analysis challenge, this work on MySQL covers basic functions, aggregate functions, and GROUP BY clause


USE Challenge;

SELECT * FROM Country;
SELECT * FROM Persons;

# 1. Write an SQL query to print the first three characters of Country_name from the Country table.

SELECT CountryID, 
SUBSTRING(Country_Name,1,3) 
AS CountryCode 
FROM Country;

# 2. Write an SQL query to concatenate first name and last name from Persons table.

SELECT ID, 
CONCAT(Fname,' ',Lname) AS Full_Name 
FROM Persons;

# 3. Write an SQL query to count the number of unique country names from Persons table.

SELECT Country_Name, 
COUNT(DISTINCT Country_Name) 
AS UniqueCountry
FROM Persons
GROUP BY Country_Name;

# 4. Write a query to print the maximum population from the Country table.

SELECT Country_ID, 
Country_Name, Population
FROM Country WHERE
Population = 
(SELECT MAX(Population) FROM Country);

# 5. Write a query to print the minimum population from Persons table.

SELECT DISTINCT CountryID, 
Country_Name, Population
FROM Persons WHERE
Population = 
(SELECT MIN(Population) FROM Persons);

# 6. Insert 2 new rows to the Persons table making the Lname NULL. Then write another query to count Lname from Persons table.

INSERT INTO Persons (ID,Fname,Lname,Population,Rating,CountryID,Country_Name) VALUES
(461, 'Rudra', NULL , 1435579517, 4.7, 101, 'India'),
(462, 'Alan', NULL , 340962176, 4.9, 103, 'USA');


SELECT COUNT(LName) 
AS NameCount
FROM Persons;

# 7. Write a query to find the number of rows in the Persons table.

SELECT COUNT(*)
AS RowCount 
FROM Persons;

# 8. Write an SQL query to show the population of the Country table for the first 3 rows. (Hint: Use LIMIT)

SELECT Country_Name, 
Population FROM Country 
LIMIT 3;

# 9. Write a query to print 3 random rows of countries. (Hint: Use rand() function and LIMIT)

SELECT * FROM Country
ORDER BY RAND() LIMIT 3;

# 10. List all persons ordered by their rating in descending order.

SELECT CONCAT(Fname,' ',Lname) 
AS Full_Name,
Rating FROM Persons
ORDER BY Rating DESC;


![Day 18 and Day 19 II](https://github.com/user-attachments/assets/adc1c671-0c99-4d54-aee9-d9de28ed68a5)


# 11. Find the total population for each country in the Persons table.

SELECT DISTINCT Country_Name,Population 
FROM Persons WHERE 
Country_Name IS NOT NULL;

# 12. Find countries in the Persons table with a total population greater than 50M.

SELECT DISTINCT Country_Name,Population
FROM Persons
WHERE Country_Name IS NOT NULL 
AND Population > 50000000;


![Day 18 and Day 19](https://github.com/user-attachments/assets/f505ff74-60ce-4b3c-acc1-95856b81e894)



/* 13. List the total number of persons and average rating for each country, 
but only for countries with more than 2 persons, 
ordered by the average rating in ascending order. */

SELECT Country_Name,
COUNT(ID) AS NoOfPersons,
ROUND(AVG(Rating),1) AS AvgRating
FROM Persons GROUP BY Country_Name
HAVING COUNT(ID) > 2
ORDER BY ROUND(AVG(Rating),1) ASC;
