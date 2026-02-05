# plsql_window_functions_-28840-_-Byiringiro-Benjamin-

# Project Overview

A film rental company operating in the customer service department within the entertainment industry. This project applies SQL window functions to analyze customer rental behavior, track popular films, and optimize inventory management.

# Problem Definition

Company: Film Rental Co.
Department: Customer Service & Analytics

# Business Challenge:
The company collects data on film rentals but struggles to identify which films are rented most often, which customers rent frequently, and how to manage inventory efficiently. Without clear insights, decisions about film purchases, promotions, and stock levels are mostly guesswork.

# Expected Outcome:
Determine the most rented films.
Segment customers based on rental frequency.
Optimize inventory planning and promotions using data-driven insights.

                Database Schema

The database contains three related tables:
1.Customers
Customer_id (PK)
CustomerName
Region

2.Films
Film_id (PK)
FilmTitle
Category

3.Rentals
Rental_id (PK)
Customerid (FK → Customers.Customer_id)
Filmid (FK → Films.Film_id)
Rentaldate
Returndate
Amount

(An ER-Diagram can visually show these relationships.)

# Window Functions Implemented

1.RANK() – Top 5 films by rental count per month
Interpretation: Shows which films are most popular each month to guide inventory decisions.

2.SUM() OVER() – Running total of rentals per month
Interpretation: Tracks cumulative rentals over time to monitor growth trends.

3.LAG()/LEAD() – Month-over-month rental changes
Interpretation: Shows whether rentals are increasing or decreasing compared to previous months.

4.NTILE(4) – Customer quartiles by total rentals
Interpretation: Identifies top renters (high-value customers) and low-activity customers for targeted marketing.

5.AVG() OVER() – 3-month moving average of rentals
Interpretation: Smooths seasonal fluctuations to reveal underlying rental trends.

# Result Analysis
        Descriptive (What Happened)
Action/Adventure and Comedy films were rented the most.
March and December saw the highest rental activity.

       Diagnostic (Why It Happened)
Popular genres match customer preferences.
Seasonal trends: March holidays and December festivities increased rentals.

        Prescriptive (What To Do Next)

Ensure high-demand films are always in stock.
Offer promotions to low-activity customers to boost engagement.
Plan inventory purchases based on genre trends and peak rental months.

         REFERENCES
MySQL Documentation – Window Functions Overview: https://dev.mysql.com/doc/refman/8.0/en/window-functions.html
MySQL Tutorial – Window Functions Examples for Business Analytics: https://www.mysqltutorial.org/mysql-window-functions/
Oracle Blog – Using SQL Window Functions for Customer Segmentation: https://blogs.oracle.com/sql/using-sql-window-functions-for-analytics         
