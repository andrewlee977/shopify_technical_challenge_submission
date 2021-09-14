# Question 2: SQL Questions
a. How many orders were shipped by Speedy Express in total?

SELECT ShipperName, COUNT(*) 
FROM Orders o 
JOIN Shippers s 
ON o.ShipperID = s.ShipperID 
WHERE ShipperName = 'Speedy Express' 
GROUP BY ShipperName;

Answer: 54

b. What is the last name of the employee with the most orders?

SELECT LastName, COUNT(*) AS Count_Orders 
FROM Orders o 
JOIN Employees e 
ON o.EmployeeID = e.EmployeeID 
GROUP BY LastName 
ORDER BY Count_Orders DESC 
LIMIT 1;

Answer: 40

c. What product was ordered the most by customers in Germany?

WITH table1 AS ( 
      SELECT * 
      FROM Orders 
      WHERE CustomerID IN ( SELECT CustomerID FROM Customers WHERE Country = 'Germany') )

SELECT ProductName, SUM(Quantity) as Count_Orders
FROM table1 a JOIN OrderDetails b ON a.OrderID = b.OrderID JOIN Products c ON b.ProductID = c.ProductID GROUP BY ProductName
ORDER BY Count_Orders DESC
LIMIT 1;

Answer: Boston Crab Meat (160 orders)
