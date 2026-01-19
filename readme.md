# SQL Internship Task – Task 3

## Dataset
Chinook Database imported into MySQL.

## Tools Used
- MySQL Server
- MySQL Workbench / Command Line
- CSV Export for outputs

---

## Steps Performed

### Step 1: Database Creation
Created a new database in MySQL and prepared table structures based on the Chinook dataset.

### Step 2: Data Import
Imported Chinook dataset into MySQL and ensured all 11 tables were created successfully.

### Step 3: Data Verification
Used basic queries to verify data:
- SHOW TABLES;
- SELECT COUNT(*) FROM each table;
This confirmed that all tables were filled with correct data.

### Step 4: Filtering and Sorting (WHERE + ORDER BY)
Wrote multiple queries using:
- WHERE to filter records
- ORDER BY to sort results
Used these to find top expensive tracks, high value invoices, top customers, etc.

### Step 5: Aggregation (GROUP BY + SUM, AVG, COUNT)
Created summary reports using:
- SUM(Total) for total sales
- AVG(Total) for average invoice value
- COUNT(*) for counting records
Grouped data by country, customer, genre, artist, track, and employee.

### Step 6: HAVING Clause
Filtered grouped results using HAVING, such as:
- Countries with sales greater than a value
- Customers who spent more than a value
- Tracks sold more than a number of times

### Step 7: BETWEEN and LIKE
Used:
- BETWEEN for filtering date ranges and numeric ranges
- LIKE for searching patterns in names, emails, cities, etc.

---

## Key SQL Outputs Exported to CSV

### 1) Sales Summary by Country  
Query:
SELECT BillingCountry, SUM(Total) AS TotalSales
FROM Invoice
GROUP BY BillingCountry
ORDER BY TotalSales DESC;

Exported as: sales_summary.csv  

Explanation: 

This query calculates the total sales amount for each country.

SUM(Total) adds all invoice totals.

GROUP BY BillingCountry groups sales by country.

ORDER BY TotalSales DESC sorts countries from highest to lowest sales.

The CSV file shows how much revenue each country generated.
---

### 2) Top 10 Customers by Total Spending  
Query:
SELECT c.CustomerId, c.FirstName, c.LastName, SUM(i.Total) AS TotalSpent
FROM Customer c
JOIN Invoice i ON c.CustomerId = i.CustomerId
GROUP BY c.CustomerId, c.FirstName, c.LastName
ORDER BY TotalSpent DESC
LIMIT 10;

Exported as: top_customers.csv  

Explanation:
This query finds the top 10 customers based on total money spent.

Joins Customer and Invoice tables.

SUM(i.Total) calculates total spending per customer.

GROUP BY groups data by each customer.

ORDER BY TotalSpent DESC ranks customers from highest spender to lowest.

The CSV file lists the top 10 highest-spending customers.
---

### 3) Top 10 Best-Selling Tracks  
Query:
SELECT t.TrackId, t.Name, SUM(il.Quantity) AS TotalSold
FROM InvoiceLine il
JOIN Track t ON il.TrackId = t.TrackId
GROUP BY t.TrackId, t.Name
ORDER BY TotalSold DESC
LIMIT 10;

Exported as: top_tracks.csv  

Explanation:
This query shows the tracks that were sold the most.

Joins InvoiceLine and Track.

SUM(il.Quantity) counts how many times each track was sold.

GROUP BY groups by each track.

ORDER BY TotalSold DESC shows the most sold tracks first.

The CSV file contains the top 10 best-selling tracks.
---

### 4) Invoices in Date Range (BETWEEN Example)  
Query:
SELECT *
FROM Invoice
WHERE InvoiceDate BETWEEN '2012-01-01' AND '2012-12-31';

Exported as: invoices_2012.csv  

Explanation:
This query selects all invoices from the year 2012.

BETWEEN filters records within a date range.

The CSV file contains all invoices created during 2012.

---

### 5) Customers with Name Pattern (LIKE Example)  
Query:
SELECT *
FROM Customer
WHERE FirstName LIKE 'A%';

Exported as: customers_A.csv  
Explanation:
This query finds customers whose first name starts with “A”.

LIKE 'A%' means names beginning with the letter A.

The CSV file lists all customers whose first name starts with A
---

## Files in Submission

- queries_task3.sql – Contains all SQL queries used in this task  
- sales_summary.csv – Sales summary by country  
- top_customers.csv – Top 10 customers by spending  
- top_tracks.csv – Top 10 best-selling tracks  
- invoices_2012.csv – Invoices from year 2012  
- customers_A.csv – Customers whose name starts with A  
- README.md – This documentation file  

---

## Conclusion

This task demonstrates:
- Database creation and data import  
- Data verification  
- Filtering and sorting using WHERE and ORDER BY  
- Aggregation using GROUP BY, SUM, AVG, COUNT  
- Filtering grouped data using HAVING  
- Range filtering using BETWEEN  
- Pattern matching using LIKE  
- Exporting SQL results into CSV files  

All practice queries are saved in queries_task3.sql and key outputs are exported as CSV files.
