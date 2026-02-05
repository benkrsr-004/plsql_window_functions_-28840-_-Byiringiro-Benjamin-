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
    CustomerID
    CustomerName
    Region 


2. Films


    FilmID 
    FilmTitle
    Category



3. Rentals
   
    RentalID 
    CustomerID 
    FilmID 
    RentalDate 
    ReturnDate 
  

ER Diagram:![ ER Daigram ](https://github.com/user-attachments/assets/0a132754-3a77-4b06-a6fc-43044ae845b9)

# SQL JOINs Implementation

1. INNER JOIN
             Interpretation:
All rentals returned are valid, showing which films were rented by which customers.

2. LEFT JOIN 

            Interpretation:
Identifies customers who have not rented any films, useful for marketing campaigns.

3. Products/Films with no rentals (LEFT JOIN)

              Interpretation:
Shows films that were never rented, helpful for inventory review or promotion.

4. FULL OUTER JOIN — Compare customers and films including unmatched records

            Interpretation:
Shows all customers and films, including rentals not yet made or unmatched entries.


# Window Functions Implementation

1. Ranking Functions — Top 5 films by rentals

           Interpretation:
Shows the most popular films for better inventory and promotional planning.

2. Aggregate Window Functions 

           Interpretation:
Displays cumulative rentals to observe overall trends over time.

3. Navigation Functions — Month-over-month rental growth

          Interpretation:
Highlights rental growth trends month by month.

4. Distribution Functions — Customer quartile segmentation

          Interpretation:
Divides customers into four groups to target high-value renters.

# screenshot 
<img width="943" height="375" alt="image" src="https://github.com/user-attachments/assets/22a86a22-3348-4dbb-b8ca-e7f36fc8c76c" />

         REFERENCES
MySQL Documentation – Window Functions Overview: https://dev.mysql.com/doc/refman/8.0/en/window-functions.html
MySQL Tutorial – Window Functions Examples for Business Analytics: https://www.mysqltutorial.org/mysql-window-functions/
Oracle Blog – Using SQL Window Functions for Customer Segmentation: https://blogs.oracle.com/sql/using-sql-window-functions-for-analytics         
