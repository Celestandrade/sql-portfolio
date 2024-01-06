-- Tools used: Mac OS, Docker Desktop, Azure Data Studio, Microsoft SQL Server
-- Database: AdventureWorks2019 via https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms 
-- I uploaded the database to MSSQL Server via Azure Data Studio and queried the database.

-- Q1: Retrieve all rows and columns from the table and sort the results by job title ascending.
-- Table: HumanResources.Employee
SELECT * FROM HumanResources.Employee
ORDER BY JobTitle ASC;

-- Q2: Retrieve all rows and columns from the table using table aliasing and sort the results by last name ascending.
-- Table: Person.Person
SELECT e.* FROM Person.Person AS e 
ORDER BY LastName ASC;

-- Q3: Retrieve first name, last name, and business entity ID from the table.
-- Rename the business entity ID column as 'Employee_ID' and sort the results by last name ascending. 
-- Table: Person.Person
SELECT FirstName, LastName, BusinessEntityID AS Employee_ID
FROM Person.Person 
ORDER BY Lastname ASC;

-- Q4: Return product ID, product number, and name for products that have a sell start date that is not null and a product line of 'T'.
-- Sort the results by name ascending. 
-- Table: Production.Product
SELECT ProductID, ProductNumber, Name AS ProductName
FROM Production.Product
WHERE SellStartDate IS NOT NULL 
AND ProductLine = 'T'
ORDER BY Name ASC;

-- Q5: Return sales order ID, customer ID, order date, subtotal and calculate the percentage of tax on the subtotal as a column.
-- Sort the results by subtotal descending. 
-- Table: Sales.SalesOrderHeader
SELECT SalesOrderID, CustomerID, OrderDate, SubTotal, ((TaxAmt / SubTotal) * 100) AS PercentageOfTax
FROM Sales.SalesOrderHeader
ORDER BY SubTotal DESC;

-- Q6: Return a result of unique job titles.
-- Table: HumanResources.Employee
SELECT DISTINCT(JobTitle) FROM HumanResources.Employee;

-- Q7: Calculate the total freight paid by each customer.
-- Sort the results to see which customer has paid the highest amount in freight.
-- Table: Sales.SalesOrderHeader
SELECT CustomerID, SUM(Freight) AS TotalFreightPaid
FROM Sales.SalesOrderHeader
GROUP BY CustomerID
ORDER BY SUM(Freight) DESC;

-- Q8: Find the average and the sum of the subtotal for every customer. 
-- Group the result by customer ID and sales person ID to see how much each customer spent with each sales person.
-- Table: Sales.SalesOrderHeader
SELECT CustomerID, SalesPersonID, AVG(SubTotal) AS AverageSpent, SUM(SubTotal) AS TotalSpent
FROM Sales.SalesOrderHeader
GROUP BY CustomerID, SalesPersonID
ORDER BY CustomerID DESC;

-- Q9: Retrieve the total quantity of each product ID which are in shelf A, C or H.
-- Filter the results by quantity of more than 500. 
-- Table: Production.ProductInventory
SELECT ProductID, SUM(Quantity) AS TotalQuantity
FROM Production.ProductInventory 
WHERE Shelf IN ('A', 'C', 'H') 
GROUP BY ProductID
HAVING SUM(Quantity) > 500
ORDER BY ProductID ASC;

-- Q10: Find persons whose last name starts with the letter L. 
-- Tables: Person.Person and Person.PersonPhone
SELECT Person.Person.BusinessEntityID, FirstName, LastName, PhoneNumber
FROM Person.Person
JOIN Person.PersonPhone 
ON Person.Person.BusinessEntityID = Person.PersonPhone.BusinessEntityID
WHERE LastName LIKE 'L%'
ORDER BY LastName, FirstName;

-- Q11: Find the number of employees for each city.
-- Sort the results by the cities with the most employees.
-- Tables: Person.BusinessEntityAddress and Person.Address
SELECT a.City, COUNT(b.AddressID) AS NumberOfEmployees
FROM Person.BusinessEntityAddress AS b
JOIN Person.Address AS a 
ON b.AddressID = a.AddressID 
GROUP BY a.City
ORDER BY NumberOfEmployees DESC;

-- Q12: Find the contacts who are designated as a manager in various departments.
-- Table: Person.ContactType
SELECT ContactTypeID, Name 
FROM Person.ContactType
WHERE NAME LIKE '%Manager%';

-- Q13: Make a list of contacts who are designated as 'Purchasing Manager'.
-- Return business entity ID, first name, and last name.
-- Tables: Person.ContactType and Person.BusinessEntityContact and Person.Person
SELECT p.BusinessEntityID, FirstName, LastName
FROM Person.BusinessEntityContact AS c
INNER JOIN Person.ContactType AS t 
ON t.ContactTypeID = c.ContactTypeID
INNER JOIN Person.Person AS p
ON p.BusinessEntityID = c.PersonID 
WHERE t.Name = 'Purchasing Manager'
ORDER BY LastName;

-- Q14: Retrieve the total cost of each sales order ID that exceeds 100000.
-- Tables: Sales.SalesOrderDetail
SELECT SalesOrderID, SUM(OrderQty * UnitPrice) AS SalesOrderIDCost 
FROM Sales.SalesOrderDetail 
GROUP BY SalesOrderID
HAVING SUM(OrderQty * UnitPrice) > 100000;

-- Q15: Retrieve products whose names start with 'Lock Washer'. 
-- Table: Production.Product
SELECT ProductID, Name 
FROM Production.Product
WHERE Name LIKE 'Lock Washer%'
ORDER BY ProductID ASC;

-- Q16: Retrieve records of employees. 
-- Order the results on hire date.
-- Table: HumanResources.Employee
SELECT BusinessEntityID, JobTitle, HireDate 
FROM HumanResources.Employee
ORDER BY HireDate ASC;

-- Q17: Retrieve persons whose last name begins with the letter R. 
-- Return the first name and last name. 
-- Table: Person.Person
SELECT FirstName, LastName 
FROM Person.Person
WHERE LastName LIKE 'R%'
ORDER BY FirstName ASC;

-- Q18: Use a CASE statement to identify which employees are salaried or hourly. 
-- Table: HumanResources.Employee
SELECT BusinessEntityID, JobTitle, 
CASE 
WHEN (SalariedFlag = 'true') THEN 'Salaried Employee'
ELSE 'Hourly Employee' END AS EmployeeClassification
FROM HumanResources.Employee;

-- Q19: Retrieve results from a table and skip the first 10 rows from the sorted result set. 
-- Table: HumanResources.Department
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID OFFSET 10 ROWS;

-- Q20: List all products that are red or blue in color. 
-- Table: Production.Product
SELECT Name, Color, ListPrice 
FROM Production.Product
WHERE Color IN ('Red', 'Blue')
ORDER BY ListPrice DESC; 

-- Q21: Retrieve individuals with a business entity ID within 1500.
-- And a last name starting with 'Al', and a first name starting with 'M'.
-- Table: Person.Person
SELECT BusinessEntityID, FirstName, LastName 
FROM Person.Person
WHERE BusinessEntityID < 1500
AND FirstName LIKE 'M%'
AND LastName LIKE 'Al%';

-- Q22: Retrieve the mailing address for any company that is outside of the U.S.
-- Also in a city which name starts with 'Pa'. 
-- Tables: Person.Address and Person.StateProvince
SELECT a.AddressLine1, a.AddressLine2, a.City, a.PostalCode, s.CountryRegionCode
FROM Person.Address AS a 
JOIN Person.StateProvince AS s
ON a.StateProvinceID = s.StateProvinceID
WHERE s.CountryRegionCode NOT IN ('US')
AND a.City LIKE 'Pa%'
ORDER BY s.CountryRegionCode;

-- Q23: Retrieve orders with order quantities greater than 5 or unit price discount less than 1000.
-- Also the total due must be greater than 100. 
-- Tables: Sales.SalesOrderHeader and Sales.SalesOrderDetail
SELECT * 
FROM Sales.SalesOrderHeader AS h
JOIN Sales.SalesOrderDetail AS d 
ON h.SalesOrderID = d.SalesOrderID
WHERE h.TotalDue > 100
AND (d.OrderQty > 5 OR d.UnitPriceDiscount < 1000);
