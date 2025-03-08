SELECT 
    c.CustomerID AS "Customer ID", 
    CONCAT(c.FirstName, ' ', c.LastName) AS "Full Name", 
    COALESCE(COUNT(o.OrderID), 0) AS "Total Orders"
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.FirstName, c.LastName
ORDER BY "Total Orders" DESC, "Full Name";
SELECT 
    c.Country AS "Country", 
    COALESCE(SUM(o.TotalAmount), 0) AS "Total Order Value ($)"
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.Country
HAVING "Total Order Value ($)" > 0
ORDER BY "Total Order Value ($)" DESC, "Country";
SELECT 
    c.CustomerID AS "Customer ID", 
    CONCAT(c.FirstName, ' ', c.LastName) AS "Full Name", 
    ROUND(AVG(o.TotalAmount), 2) AS "Average Order Value ($)"
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.FirstName, c.LastName
HAVING "Average Order Value ($)" IS NOT NULL
ORDER BY "Average Order Value ($)" DESC, "Full Name";
