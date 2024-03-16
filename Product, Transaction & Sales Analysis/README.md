# Product, Transaction & Sales Analysis of a Clothing Company

## Table of Content
* [Introduction](#introduction)
* [Entity Relationship Diagram](#entity-relationship-diagram)
* [Tools](#tools)
* [Methodology](#methodology)
* [SQL Queries](#sql-queries)
* [Insights](#insights)
* [Note](#note)

## Introduction
The project aims to assist the merchandising team in analyzing their sales performance and generate a basic financial report to share with the wider business. The analysis is performed at the product, sales, and transactions level and a reporting solution has been developed to automate the end entire analysis and reporting process.

## Entity Relationship Diagram
``product_details`` table includes all information about the entire range of products.

``Sales`` table contains product-level information for all the transactions made for Balanced Tree including quantity, price, percentage discount, member status, a transaction ID, and also the transaction timestamp.


![image](https://i.imgur.com/A4134db.png)


## Tools
MySQL

## Methodology
### Analysis
* Performed analysis at product, transaction, and sales levels by developing SQL queries.
* For this data from ``sales`` table and ``product_details`` table were used.

### Reporting
* Created a new table ``sales_m`` to store the required monthly sales data. This has the same structure as the ``sales`` table.
* Created two procedures and combined them into one procedure to automate the entire reporting process for the required month and year.
* Created 1st procedure ``monthly_sales_4 `` with input parameters - month and year. The purpose of the procedure is to get the sales data from the ``sales`` table based on the month and year and insert it into the new table ``sales_m``. Every time this procedure is executed, the older records of the year and month are removed and new records are inserted.
* Created 2nd procedure ``auto_select`` without any input parameter. The purpose of this procedure is to run all the select queries for  product, transaction, and sales analysis on the sales data in the new table ``sales_m``.
* Created 3rd procedure ``report`` with input parameters - month and year. The purpose of the procedure is to combine the 1st and 2nd procedures. It will first
extract the data from the ``sales`` table for the required year and month and insert it into the ``sales_m`` table. And then run all the queries for reporting.


## SQL Queries
1. [Product Analysis](https://github.com/MukulGehlot/SQL-Projects/blob/main/Product%2C%20Transaction%20%26%20Sales%20Analysis/1.%20Product%20Analysis.sql)
2. [Transaction Analysis](https://github.com/MukulGehlot/SQL-Projects/blob/main/Product%2C%20Transaction%20%26%20Sales%20Analysis/2.%20Transaction%20Analysis.sql)
3. [Sales Analysis](https://github.com/MukulGehlot/SQL-Projects/blob/main/Product%2C%20Transaction%20%26%20Sales%20Analysis/3.%20Sales%20Analysis.sql)
4. [Reporting](https://github.com/MukulGehlot/SQL-Projects/blob/main/Product%2C%20Transaction%20%26%20Sales%20Analysis/4.%20Reporting.sql)

## Insights
### Product Analysis
1. What are the top 3 products by total revenue before discount? <br> ![image](https://i.imgur.com/XuQar5W.png)

2. What is the total quantity, revenue, and discount for each segment? <br> ![image](https://i.imgur.com/PLpLEuH.png)

3. What is the top-selling product for each segment?<br> ![image](https://i.imgur.com/2EeIkMP.png)

4. What is the total quantity, revenue, and discount for each category?<br> ![image](https://i.imgur.com/VLlcoB8.png)

5. What is the top-selling product for each category?<br> ![image](https://i.imgur.com/udvJkNZ.png)

6. What is the percentage split of revenue by product for each segment?<br> ![image](https://i.imgur.com/vP1IcCU.png)

7. What is the percentage split of revenue by segment for each category?<br> ![image](https://i.imgur.com/cHg0FIG.png)

8. What is the percentage split of total revenue by category?<br> ![image](https://i.imgur.com/bFoHxmT.png)

9. What is the total transaction “penetration” for each product? (hint: penetration = number of transactions where at least 1 quantity of a product was purchased divided by the total number of transactions)<br> ![image](https://i.imgur.com/3mSv6bD.png)

10. What is the most common combination of at least 1 quantity of any 3 products in a 1 single transaction?<br> ![image](https://i.imgur.com/dMEnqHO.png)


### Transaction Analysis
1. 2500 unique transactions were there.
2. 6 average unique products were purchased in each transaction.
3. The 25th, 50th, and 75th percentile values for the revenue per transaction are 376.6,
509.8, and 647.1 respectively.
4. 73.1 is the average discount value per transaction.
5. The percentage split of all transactions for members vs non-members is 39.8 and 60.2.
6. The average revenue for member transactions is 516.3 and for non-member transactions is 515.0.
   
### Sales Analysis
1. The total quantity sold is 45216.
2. The total generated revenue for all products before discounts is 1289453.
3. The total discount amount for all products is 15622914.

## Note
This project is one of the [SQL challenges](https://8weeksqlchallenge.com/case-study-7/) by [Danny Ma](https://www.linkedin.com/in/datawithdanny/).
