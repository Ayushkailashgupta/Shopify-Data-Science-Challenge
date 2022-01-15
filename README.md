# Shopify-Data-Science-Challenge

# Question 1:
Given some sample data, write a program to answer the following: click here to access the required data set
On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

a. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

Answer:

On Analyzing data I found out that there are outliers present in our data set.
user id 607 and shop id 78 are the outliers present in our data-set : These 2 are the main things that are going wrong in our calculation. Therefore, a better metric would be Median Order Value. Though if we remove outlier values from our data-set we can also use Mean Order Value metric.

b. What metric would you report for this dataset?

Answer:

The metric that I would report for this dataset is median order value as there are outliers present in our data-set.
But if we remove outliers from data-set then we can use mean order value.


c. What is its value?

Answer:

284.0 (Median Order Value)
(302.58 - Mean Order Value if we remove outliers from our data-set)

# Question 2:
For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

a. How many orders were shipped by Speedy Express in total?

Answer:

SELECT COUNT(OrderID) FROM Orders 
WHERE ShipperID = (SELECT ShipperID FROM Shippers 
WHERE ShipperName = 'Speedy Express');

Output: 54

b. What is the last name of the employee with the most orders?

Answer:

SELECT e.LastName, COUNT(DISTINCT o.OrderID) as total_order 
FROM Orders o
Inner Join Employees e ON o.EmployeeID = e.EmployeeID 
GROUP BY e.EmployeeID 
ORDER BY COUNT(DISTINCT OrderID) DESC LIMIT 1;

Output: Peacock (No of orders is 40)

c. What product was ordered the most by customers in Germany?

Answer:

SELECT Products.ProductName FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID 
INNER JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
INNER JOIN Products ON OrderDetails.ProductID = Products.ProductID
WHERE Customers.Country = 'Germany' 
GROUP BY Products.ProductName 
ORDER BY COUNT(Products.ProductName) DESC LIMIT 1;

Output: Gorgonzola Telino

