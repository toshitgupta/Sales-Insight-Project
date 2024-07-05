# Sales Insights Data Analysis Project

This project involves analyzing sales data using SQL and Power BI. The data and SQL queries provided allow for insights into customer transactions, revenue, and more.

## Instructions to Setup MySQL on Your Local Computer

1. Follow the steps in this [video](https://www.youtube.com/watch?v=WuBcTJnIuzo) to install MySQL on your local computer.
2. Download the `db_dump.sql` file to your local computer.
3. Import the `db_dump.sql` file into MySQL as per the instructions given in the tutorial video.

## Data Analysis Using SQL

1. **Show all customer records**

    ```sql
    SELECT * FROM customers;
    ```

2. **Show total number of customers**

    ```sql
    SELECT count(*) FROM customers;
    ```

3. **Show transactions for Chennai market (market code for Chennai is Mark001)**

    ```sql
    SELECT * FROM transactions where market_code='Mark001';
    ```

4. **Show distinct product codes that were sold in Chennai**

    ```sql
    SELECT distinct product_code FROM transactions where market_code='Mark001';
    ```

5. **Show transactions where currency is US dollars**

    ```sql
    SELECT * from transactions where currency="USD";
    ```

6. **Show transactions in 2020 join by date table**

    ```sql
    SELECT transactions.*, date.* 
    FROM transactions 
    INNER JOIN date ON transactions.order_date=date.date 
    WHERE date.year=2020;
    ```

7. **Show total revenue in the year 2020**

    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date=date.date 
    WHERE date.year=2020 AND (transactions.currency="INR" OR transactions.currency="USD");
    ```

8. **Show total revenue in January 2020**

    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date=date.date 
    WHERE date.year=2020 AND date.month_name="January" AND (transactions.currency="INR" OR transactions.currency="USD");
    ```

9. **Show total revenue in Chennai in 2020**

    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date ON transactions.order_date=date.date 
    WHERE date.year=2020 AND transactions.market_code="Mark001";
    ```

## Data Analysis Using Power BI

1. **Formula to create `norm_amount` column**

    ```powerquery
    = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
    ```

## Files

- `db_dump.sql` - SQL database dump file.
- `db_dump_version_2.sql` - Updated version of the SQL database dump.
- `sales_insight_dashboard.pbix` - Power BI dashboard file.
- `sales_insight_updated_dashboard.pbix` - Updated version of the Power BI dashboard.
