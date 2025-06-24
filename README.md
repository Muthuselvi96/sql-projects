**DDL-CREATE SCHEMA [FoxcoreDatabase| AUTHORIZATION FoxcoreOwner]**
CREATE TABLE EventType (
event_type_id INT PRIMARY KEY NOT NULL,
event_type_name VARCHAR(50) NOT NULL
)
CREATE TABLE Event (
event_id INT PRIMARY KEY NOT NULL,
event_name VARCHAR(50) NOT NULL,
start_date DATE NOT NULL,
end_date DATE NOT NULL,
Event_Description VARCHAR(100) NOT NULL,
event_type_id INT NOT NULL,
venue_id INT NOT NULL,
FOREIGN KEY (event_type_id) REFERENCES EventType(event_type_id),
FOREIGN KEY (venue_id) REFERENCES Venue(venue_id)
)
CREATE TABLE Booth (
booth_id INT PRIMARY KEY NOT NULL,
event_id INT NOT NULL,
booth_location VARCHAR(100) NOT NULL,
FOREIGN KEY (event_id) REFERENCES Event(event_id)
)
CREATE TABLE Product (
product_id INT PRIMARY KEY NOT NULL,
product_name VARCHAR(50) NOT NULL,
wholesale_cost DECIMAL(10,2) NOT NULL,
min_selling_price DECIMAL(10,2) NOT NULL,
max_selling_price DECIMAL(10,2) NOT NULL
)
CREATE TABLE Salesperson (
salesperson_id INT PRIMARY KEY NOT NULL,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50),
address VARCHAR(100) NOT NULL,
phone_number VARCHAR(15) NOT NULL,
sales_incentives DECIMAL(10,2) NOT NULL
)
CREATE TABLE Shift (
shift_id INT PRIMARY KEY NOT NULL,
salesperson_id INT NOT NULL,
booth_id INT NOT NULL,
shift_start_time DATETIME NOT NULL,
shift_end_time DATETIME NOT NULL,
FOREIGN KEY (salesperson_id) REFERENCES Salesperson(salesperson_id),
FOREIGN KEY (booth_id) REFERENCES Booth(booth_id)
)
CREATE TABLE Sales (
sales_id INT PRIMARY KEY NOT NULL,
salesperson_id INT NOT NULL,
booth_id INT NOT NULL,
product_id INT NOT NULL,
quantity_sold INT NOT NULL,
selling_price DECIMAL(10,2) NOT NULL,
sale_date DATE NOT NULL,
FOREIGN KEY (salesperson_id) REFERENCES Salesperson(salesperson_id),
FOREIGN KEY (booth_id) REFERENCES Booth(booth_id),
FOREIGN KEY (product_id) REFERENCES Product(product_id)
)
**DCL COMMANDS**
/Table Name: Event
GRANT ALL PRIVILEGES
ON Event
TO Fox;
GRANT ALL PRIVILEGES
ON Event
TO Corrigan;
//Table Name: Venue
GRANT ALL PRIVILEGES
ON Venue
TO Fox;
GRANT ALL PRIVILEGES
ON Venue
TO Corrigan;
//Table Name: EventType
GRANT ALL PRIVILEGES
ON EventType
TO Fox;
GRANT ALL PRIVILEGES
ON EventType
TO Corrigan;
//Table Name: Booth
GRANT ALL PRIVILEGES
ON Booth
TO Fox;
GRANT ALL PRIVILEGES
ON Booth
TO Corrigan;
//Table Name: Shift
GRANT ALL PRIVILEGES
ON Shift
TO Fox;
GRANT ALL PRIVILEGES
ON Shift
TO Corrigan;
//Table Name: Product
GRANT ALL PRIVILEGES
ON Product
TO Fox;
GRANT ALL PRIVILEGES
ON Product
TO Corrigan;
//Table Name: Sales
GRANT ALL PRIVILEGES
ON Sales
TO Fox;
GRANT ALL PRIVILEGES
ON Sales
TO Corrigan;
//Table Name: Salesperson
GRANT ALL PRIVILEGES
ON Salesperson
TO Fox;
GRANT ALL PRIVILEGES
ON Salesperson
TO Corrigan;
**DML**
**Loading new datas into EventType table?**
INSERT INTO EventType (event_type_id, event_type_name) VALUES
(1, 'Trade Show'),
(2, 'Rib Fest'),
(3, 'Waterfront Festival'),
(4, 'Music Festival'),
(5, 'Beer Festival'),
(6, 'Sporting Event'),
(7, 'Street Festival');
**Values  into Venue table**
INSERT INTO Venue (venue_id, venue_name, address, Venue_Description) VALUES
(1, 'Venue 1', 'Address 1', 'Description 1'),
(2, 'Venue 2', 'Address 2', 'Description 2'),
(3, 'Venue 3', 'Address 3', 'Description 3');
P a g e 19 | 25
**Values into Event table**
INSERT INTO Event (event_id, event_name, start_date, end_date, Event_Description,
event_type_id, venue_id) VALUES
(1, 'Event 1', '2024-05-01', '2024-05-05', 'Event Description 1', 1, 1),
(2, 'Event 2', '2024-06-10', '2024-06-15', 'Event Description 2', 4, 2),
(3, 'Event 3', '2024-07-20', '2024-07-25', 'Event Description 3', 7, 3);
**Values in Booth table**
INSERT INTO Booth (booth_id, event_id, booth_location) VALUES
(1, 1, 'Location 1'),
(2, 2, 'Location 2'),
(3, 3, 'Location 3');
**values into Product table**
INSERT INTO Product (product_id, product_name, wholesale_cost, min_selling_price,
max_selling_price) VALUES
(1, 'Product 1', 10.00, 15.00, 25.00),
(2, 'Product 2', 12.00, 18.00, 30.00),
(3, 'Product 3', 8.00, 12.00, 20.00);
P a g e 20 | 25
**values into salesperson**
INSERT INTO Salesperson (salesperson_id, first_name, last_name, address, phone_number,
sales_incentives) VALUES
(1, 'John', 'Doe', 'Address 1', '123-456-7890', 0.05),
(2, 'Jane', 'Smith', 'Address 2', '456-789-0123', 0.07),
(3, 'Alice', 'Johnson', 'Address 3', '789-012-3456', 0.08);
 **insert new information into shifttable**
INSERT INTO Shift (shift_id, salesperson_id, booth_id, shift_start_time, shift_end_time)
VALUES
(1, 1, 1, '2024-05-01 08:00:00', '2024-05-01 17:00:00'),
(2, 2, 2, '2024-06-10 09:00:00', '2024-06-10 18:00:00'),
(3, 3, 3, '2024-07-20 10:00:00', '2024-07-20 20:00:00');
**add new sales into the sales table**
INSERT INTO Sales (sales_id, salesperson_id, booth_id, product_id, quantity_sold,
selling_price, sale_date) VALUES
(1, 1, 1, 1, 20, 20.00, '2024-05-01'),
(2, 2, 2, 2, 15, 25.00, '2024-06-10'),
(3, 3, 3, 3, 10, 15.00, '2024-07-20');
**data manipulation**
1.Update the information of Event_Descrpition of first event?
UPDATE Event SET Event_Description = 'New Event Description' WHERE event_id = 1;
2.How to update the min_selling_price for Product as 20 where product_id=2?
UPDATE Product SET min_selling_price = 20.00 WHERE product_id = 2
3. How to update the sales_incentives for Salesperson with ID=3?
UPDATE Salesperson SET sales_incentives = 0.10 WHERE salesperson_id = 3;
8.3. DELETE STATEMENTS TO REMOVE DATA FROM THE DATABASE
1. How to delete the shift id=3?
SET FOREIGN_KEY_CHECKS=1;
DELETE FROM Shift WHERE shift_id = 3;
SET FOREIGN_KEY_CHECKS=0;
2.How to delete the salesperson with salesperson_id=2?
SET FOREIGN_KEY_CHECKS=1;
DELETE FROM Salesperson WHERE salesperson_id = 2;
SET FOREIGN_KEY_CHECKS=0;
3. How to delete the sales records for event_id=1?
SET FOREIGN_KEY_CHECKS=1;
DELETE FROM Sales WHERE booth_id IN (SELECT booth_id FROM Booth WHERE
event_id = 1);
SET FOREIGN_KEY_CHECKS=0;
8.4. SQL STATEMENTS REQUIRED TO PREPARE THE REPORTS DESCRIBED IN
THE CASE
1.Total Sales by Event Type and Date Range:
SELECT et.event_type_name, e.event_name, b.booth_id, SUM(s.selling_price *
s.quantity_sold) AS Total_sales
FROM event e
JOIN booth b ON b.event_id = e.event_id
JOIN sales s ON s.booth_id = b.booth_id
JOIN eventtype et ON et.event_type_id = e.event_type_id
WHERE e.start_date >= '2024-01-01' AND e.end_date <= '2024-12-12'
GROUP BY et.event_type_name, e.event_name, b.booth_id;
**report Sales of each Salesperson**
SELECTconcat(sp.first_name,'',sp.last_name)AS
Salesperson_name,sum(s.quantity_sold*s.selling_price) as total_sales from sales s
JOIN salesperson sp on sp.salesperson_id = s.salesperson_id
GROUP BY Salesperson_name;
**show the Sales by each Product**
SELECT Product.product_name, SUM(Sales.quantity_sold * Sales.selling_price) AS
total_sales
FROM Product
JOIN Sales ON Product.product_id = Sales.product_id
GROUP BY Product.product_name;
**report the Sales by Event**
SELECT Event.event_name, SUM(Sales.quantity_sold * Sales.selling_price) AS total_sales
FROM Event
JOIN Booth ON Event.event_id = Booth.event_id
JOIN Sales ON Booth.booth_id = Sales.booth_id
GROUP BY Event.event_name;
