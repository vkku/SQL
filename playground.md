![image](https://github.com/user-attachments/assets/23cda1f6-2dc6-42dd-9878-2b889c6e291e)
rexon_metals.db
https://sqliteonline.com/#urldb=https://raw.githubusercontent.com/vkku/SQL/master/database/rexon_metals.db

weather_stations.db
https://sqliteonline.com/#urldb=https://raw.githubusercontent.com/vkku/SQL/master/database/weather_stations.db

> Use HAVING on aggregated fields as MAX()
```
SELECT year, max(snow_depth) AS max_depth
FROM STATION_DATA
GROUP BY year
HAVING max_depth > 50
```

> SELECT the report_code, year, quarter, and temperature, where a “quarter” is “Q1”, “Q2”, “Q3”, or
“Q4” reflecting months 1-3, 4-6, 7-9, and 10-12 respectively
```
SELECT report_code, year, temperature,
CASE
    WHEN month BETWEEN 1 AND 3 THEN 'Q1'
    WHEN month BETWEEN 4 AND 6 THEN 'Q2'
    WHEN month BETWEEN 7 AND 9 THEN 'Q3'
    WHEN month BETWEEN 10 AND 12 THEN 'Q4'
END AS quarter
FROM STATION_DATA;
```
![image](https://github.com/user-attachments/assets/328dc389-151e-4f90-a752-4532974392e0)
> SELECT the ORDER_ID, ORDER_DATE, and DESCRIPTION (from PRODUCT)
```
select CUSTOMER_ORDER.order_id, CUSTOMER_ORDER.order_date, PRODUCT.description
FROM CUSTOMER_ORDER INNER JOIN PRODUCT
ON CUSTOMER_ORDER.PRODUCT_ID = PRODUCT.PRODUCT_ID
```
> SELECT NAME, BUSINESS from each vendor where business is the number of items sold to vendor, vendors with 0 business should also be displayed
```
SELECT CUSTOMER.CUSTOMER_ID, CUSTOMER.NAME,
COALESCE( SUM( CUSTOMER_ORDER.ORDER_QTY * PRODUCT.PRICE ), 0) ||  ' INR' AS BUSINESS
FROM
    CUSTOMER
    Left JOIN
    CUSTOMER_ORDER on CUSTOMER.CUSTOMER_ID = CUSTOMER_ORDER.CUSTOMER_ID
    LEFT JOIN
    PRODUCT on CUSTOMER_ORDER.PRODUCT_ID = PRODUCT.PRODUCT_ID
GROUP BY CUSTOMER.CUSTOMER_ID
ORDER BY BUSINESS DESC
```
![image](https://github.com/user-attachments/assets/25d61c73-43d5-4baf-9945-59c480d60d7a)

