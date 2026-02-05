# plsql_window_functions_-28840-_-Byiringiro-Benjamin-

            Problem Definition 
# Business Context:
A film rental company operating in the Customer Service Department within the entertainment industry.

# Data Challenge:
The company records data on films rented by customers, but it is difficult to track which films are borrowed most often and how frequently customers return. This makes it hard to manage film inventory and plan future purchases.

# Expected Outcome:
Identify the most rented films.
Analyze customer rental frequency.
Support better inventory management and decision-making for future film acquisitions.

# Success Criteria

Top 5 films per month or quarter — Use RANK() to identify the most rented films.
Running total of rentals — Use SUM() OVER() to track cumulative rentals over time.
Month-over-month rental growth — Use LAG() or LEAD() to compare rental numbers between months.
Customer segmentation by rentals — Use NTILE(4) to divide customers into quartiles based on how often they rent films.
Three-month moving average of rentals — Use AVG() OVER() to analyze rental trends over a rolling three-month period.

# Database Schema Design (ER Diagram Included)

Tables
1. Customers

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL,
    Region VARCHAR(50)
);


2. Films

CREATE TABLE Films (
    FilmID INT PRIMARY KEY,
    FilmTitle VARCHAR(100) NOT NULL,
    Category VARCHAR(50)
);


3. Rentals

CREATE TABLE Rentals (
    RentalID INT PRIMARY KEY,
    CustomerID INT NOT NULL,
    FilmID INT NOT NULL,
    RentalDate DATE NOT NULL,
    ReturnDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (FilmID) REFERENCES Films(FilmID)
);


ER Diagram:![ ER Daigram ](https://github.com/user-attachments/assets/0a132754-3a77-4b06-a6fc-43044ae845b9)

# SQL JOINs Implementation

1. INNER JOIN — Rentals with valid customers and films

SELECT r.RentalID, c.CustomerName, f.FilmTitle, r.RentalDate, r.ReturnDate
FROM Rentals r
INNER JOIN Customers c ON r.CustomerID = c.CustomerID
INNER JOIN Films f ON r.FilmID = f.FilmID;

             Interpretation:
All rentals returned are valid, showing which films were rented by which customers.

2. LEFT JOIN — Customers who never rented a film

SELECT c.CustomerName, r.RentalID
FROM Customers c
LEFT JOIN Rentals r ON c.CustomerID = r.CustomerID
WHERE r.RentalID IS NULL;


            Interpretation:
Identifies customers who have not rented any films, useful for marketing campaigns.

3. Products/Films with no rentals (LEFT JOIN)

SELECT f.FilmTitle, r.RentalID
FROM Films f
LEFT JOIN Rentals r ON f.FilmID = r.FilmID
WHERE r.RentalID IS NULL;


              Interpretation:
Shows films that were never rented, helpful for inventory review or promotion.

4. FULL OUTER JOIN — Compare customers and films including unmatched records

SELECT c.CustomerName, f.FilmTitle, r.RentalID
FROM Customers c
FULL OUTER JOIN Rentals r ON c.CustomerID = r.CustomerID
FULL OUTER JOIN Films f ON r.FilmID = f.FilmID;


            Interpretation:
Shows all customers and films, including rentals not yet made or unmatched entries.

5. SELF JOIN — Compare customers within the same region

SELECT c1.CustomerName AS CustomerA, c2.CustomerName AS CustomerB, c1.Region
FROM Customers c1
INNER JOIN Customers c2 ON c1.Region = c2.Region AND c1.CustomerID < c2.CustomerID;


          Interpretation:
Useful for analyzing customer clusters and regional rental patterns.

# Window Functions Implementation

1. Ranking Functions — Top 5 films by rentals

SELECT FilmID, COUNT(*) AS TotalRentals,
       RANK() OVER (ORDER BY COUNT(*) DESC) AS RentalRank
FROM Rentals
GROUP BY FilmID;


           Interpretation:
Shows the most popular films for better inventory and promotional planning.

2. Aggregate Window Functions — Running total of rentals

SELECT RentalDate, COUNT(*) OVER (ORDER BY RentalDate ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS RunningTotal
FROM Rentals;


           Interpretation:
Displays cumulative rentals to observe overall trends over time.

3. Navigation Functions — Month-over-month rental growth

SELECT DATE_TRUNC('month', RentalDate) AS Month,
       COUNT(*) AS MonthlyRentals,
       LAG(COUNT(*)) OVER (ORDER BY DATE_TRUNC('month', RentalDate)) AS PreviousMonthRentals,
       COUNT(*) - LAG(COUNT(*)) OVER (ORDER BY DATE_TRUNC('month', RentalDate)) AS RentalsGrowth
FROM Rentals
GROUP BY DATE_TRUNC('month', RentalDate);


          Interpretation:
Highlights rental growth trends month by month.

4. Distribution Functions — Customer quartile segmentation

SELECT CustomerID, COUNT(*) AS TotalRentals,
       NTILE(4) OVER (ORDER BY COUNT(*) DESC) AS RentalQuartile
FROM Rentals
GROUP BY CustomerID;


          Interpretation:
Divides customers into four groups to target high-value renters.

5. Moving Averages — Three-month moving average of rentals

SELECT DATE_TRUNC('month', RentalDate) AS Month,
       AVG(COUNT(*)) OVER (ORDER BY DATE_TRUNC('month', RentalDate) ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS ThreeMonthAvg
FROM Rentals
GROUP BY DATE_TRUNC('month', RentalDate);
# screenshot 
<img width="943" height="375" alt="image" src="https://github.com/user-attachments/assets/22a86a22-3348-4dbb-b8ca-e7f36fc8c76c" />

         REFERENCES
MySQL Documentation – Window Functions Overview: https://dev.mysql.com/doc/refman/8.0/en/window-functions.html
MySQL Tutorial – Window Functions Examples for Business Analytics: https://www.mysqltutorial.org/mysql-window-functions/
Oracle Blog – Using SQL Window Functions for Customer Segmentation: https://blogs.oracle.com/sql/using-sql-window-functions-for-analytics         
