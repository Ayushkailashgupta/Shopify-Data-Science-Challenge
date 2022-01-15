# Shopify-Data-Science-Challenge

Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

a) How many orders were shipped by Speedy Express in total?
Answer:
SELECT COUNT(OrderID) FROM Orders 
WHERE ShipperID = (SELECT ShipperID FROM Shippers 
WHERE ShipperName = 'Speedy Express');

Output: 54

b) What is the last name of the employee with the most orders?
Answer:
SELECT e.LastName, COUNT(DISTINCT o.OrderID) as total_order 
FROM Orders o
Inner Join Employees e ON o.EmployeeID = e.EmployeeID 
GROUP BY e.EmployeeID 
ORDER BY COUNT(DISTINCT OrderID) DESC LIMIT 1;

Output: Peacock (No of orders is 40)

What product was ordered the most by customers in Germany?
Answer:
SELECT Products.ProductName FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID 
INNER JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
INNER JOIN Products ON OrderDetails.ProductID = Products.ProductID
WHERE Customers.Country = 'Germany' 
GROUP BY Products.ProductName 
ORDER BY COUNT(Products.ProductName) DESC LIMIT 1;

Output: Gorgonzola Telino

