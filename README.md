# CaseStudy
CREATE TABLE Products (
ProductID INT PRIMARY KEY,
ProductName NVARCHAR(100),
Price DECIMAL(10, 2)
);

INSERT INTO Products (ProductID, ProductName, Price) VALUES
(1, 'Laptop', 1500.00),
(2, 'Mouse', 25.00),
(3, 'Keyboard', 45.00);

CREATE TABLE Sales (
SaleID INT PRIMARY KEY,
ProductID INT,
Quantity INT,
SaleDate DATETIME,
FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

INSERT INTO Sales (SaleID, ProductID, Quantity, SaleDate) VALUES
(1, 1, 2, '2024-01-10'),
(2, 2, 5, '2024-01-15'),
(3, 1, 1, '2024-02-20'),
(4, 3, 3, '2024-03-05'),
(5, 2, 7, '2024-03-25'),
(6, 3, 2, '2024-04-12');

SELECT 
    Products.ProductID, 
	Products.ProductName,
	YEAR(Sales.SaleDate) AS Year_,
    SUM(Sales.Quantity) AS NumberofSales, 
    SUM(Sales.Quantity * Products.Price) AS SalesAmount
FROM 
    Products
LEFT JOIN 
    Sales ON Sales.ProductID = Products.ProductID
GROUP BY 
    Products.ProductID,Products.ProductName, YEAR(Sales.SaleDate)
ORDER BY SalesAmount desc;
