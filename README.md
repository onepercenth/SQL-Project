# AxiaStores SQL Database Project
## Project Overview
This project demonstrates a complete SQL based solution for an Electronics & Accessories retail business, **AxiaStores**. It involves designing and implementing a relational database with three core tables, Customer, Product, and Orders. While performing various analytical queries to extract insights.
## Objectives
The primary goal of this project is to
- Create a sample relational database
- Creation of multiple tables within the database with appropriate data types and constraints:
- Insertion of sample records into all tables
- Query functions like:
  - Retriever of customer details
  - Sorting alphabetically
  - The use of Join funtion for multiple tables
  - Use of aggregate functions like average and sum
## Tools and Methodologies 
**Tool Used:** **SQL SERVER MANAGEMENT STUDIO 21** [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
## Key Analytical Questions
The queries in this project aim to answer the following key questions based on the AxiaStores dataset:
1. Return the FirstName and Email of every customer who has ever purchased the product “Wireless Mouse”
2. List all customers’ full names in ascending alphabetical order (LastName, then FirstName)
3. Show every order together with the customer’s full name, the product name, quantity, unit price, total price (quantity × unit price), and order date
4. Show average sales per product category and sort in descending order
5. Which city generated the highest revenue for AxiaStores
1. **CREATING DATABASE**
<pre>
CREATE DATABASE [AxiaStores]; --SQL Server
</pre>
2. **CREATING CustomerTB**
<pre>
CREATE TABLE CustomerTB
(CustomerID INT PRIMARY KEY,
FirstName VARCHAR (255),
LastName VARCHAR (255),
Email VARCHAR (255),
Phone VARCHAR (50),
City VARCHAR (100));
INSERT INTO CustomerTB (CustomerID, FirstName, LastName, Email, Phone, City)
VALUES
(1, 'Musa', 'Ahmed', 'musa.ahmed@hotmail.com', '0803‑123‑0001', 'Lagos'),
('2', 'Ray', 'Samson', 'ray.samson@yahoo.com', '0803‑123‑0002', 'Ibadan'),
('3', 'Chinedu', 'Okafor', 'chinedu.ok@yahoo.com', '0803‑123‑0003', 'Enugu'),
('4', 'Dare', 'Adewale', 'dare.ad@hotmail.com', '0803‑123‑0004', 'Abuja'),
('5', 'Efe', 'Ojo', 'efe.oj@gmail.com', '0803‑123‑0005', 'Port Harcourt'),
('6', 'Aisha', 'Bello', 'aisha.bello@hotmail.com', '0803‑123‑0006', 'Kano'),
('7', 'Tunde', 'Salami', 'tunde.salami@yahoo.c
('8', 'Nneka', 'Umeh', 'nneka.umeh@gmail.com', '0803‑123‑0008', 'Owerri'),
('9', 'Kelvin', 'Peters', 'kelvin.peters@hotmail.com', '0803‑123‑0009', 'Asaba'),
('10', 'Blessing', 'Mark', 'Blessing.mark@gmail.com', '0803‑123‑0010', 'Uyo');
</pre>
## Answers to Analytical Questions and Results

1. **Return the FirstName and Email of every customer who has ever purchased the product “Wireless Mouse”**
<pre>
--Return the FirstName and Email of every customer who has ever purchased the product “Wireless Mouse”
select c.firstname, c.email from customertb c
join OrdersTB o on c.CustomerID = o.CustomerID
join ProductTB p on o.ProductID = p.ProductID
where p.ProductID=1
</pre>
2. **List all customers’ full names in ascending alphabetical order (LastName, then
FirstName)**
<pre>
SELECT 
    CONCAT(FirstName, ' ', LastName) AS FullName
FROM 
    CustomerTB
ORDER BY 
    LastName ASC, FirstName ASC;
</pre>
3. **Show every order together with the customer’s full name, the product name, quantity,
unit price, total price (quantity × unit price), and order date**
<pre>
SELECT 
    o.OrderID,
    CONCAT(c.FirstName, ' ', c.LastName) AS CustomerName,
    p.ProductName,
    o.Quantity,
    p.UnitPrice,
    (o.Quantity * p.UnitPrice) AS TotalPrice,
    o.OrderDate
FROM OrdersTB o
JOIN CustomerTB c ON o.CustomerID = c.CustomerID
JOIN ProductTB p ON o.ProductID = p.ProductID;
</pre>
4. **Show average sales per product category and sort in descending order**
<pre>
SELECT 
    p.Category,
    ROUND(AVG(o.Quantity * p.UnitPrice), 2) AS AvgSales
FROM OrdersTB o
JOIN ProductTB p ON o.ProductID = p.ProductID
GROUP BY p.Category
ORDER BY AvgSales DESC;
</pre>
5. **Which city generated the highest revenue for AxiaStores?**
<pre>
SELECT TOP 1
    c.City,
    SUM(o.Quantity * p.UnitPrice) AS TotalRevenue
FROM OrdersTB o
JOIN CustomerTB c ON o.CustomerID = c.CustomerID
JOIN ProductTB p ON o.ProductID = p.ProductID
GROUP BY c.City
ORDER BY TotalRevenue DESC;
</pre>
### References
- [Axia Africa SQL Exam](https://drive.google.com/file/d/13chnDFUr7NqbyPSRqy65d9pgeVCM86Ix/view)
- [Axia Africa](https://student.axia.africa)
## Table of Content
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Tools and Methodologies](#tools-and-methodologies)
- [Key Analytical Questions](#key-analytical-questions)
- [Samples of SQL Queries and Results](#samples-of-sql-queries-and-results)
- [Answers to Analytical Questions and Results](#answers-to-analytical-questions-and-results)
- [References](#references)
