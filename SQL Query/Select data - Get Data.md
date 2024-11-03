Get all data from the table **books**
```
SELECT * from 'table_name'
```
Get all data where the Book publish after 2005
```
SELECT * from 'table_name' WHERE column_name > 2005
```
## Count data row
You can count the data row with the count() function
```
SELECT COUNT(*) from 'table_name'
```
## Rename the table name
You can rename the table name in this way
```
SELECT COUNT(*) as new_table_name FROM 'table_name'
```
## MAX Value 
You can get the max value easily with the MAX function
```
SELECT MAX(column_name) FROM 'table_name'
```
## MIN Value 
To get the MIN value to the table 
```
SELECT MIN(column_name) FROM 'table_name'
```
## JOIN Table
```
SELECT * FROM 'table1' JOIN 'table2' ON table1.id = table2.customer_id
```
If you want any specific column, here is the another query
```
SELECT table1.id, table1.name, table2.facebook_link FROM 'table1' JOIN 'table2' ON table1.id = table2.customer_id
```
Notes: It will show only that data is not NULL
## LEFT JOIN
If you want to see all data even the column is NULL  of your left table you should apply the LEFT JOIN
```
SELECT table1.id, table1.name, table2.facebook_link FROM 'table1' LEFT JOIN 'table2' ON table1.id = table2.customer_id
```
## RIGHT JOIN
If you want to see all data even the column is NULL  of your right table you should apply the RIGHT JOIN
```
SELECT table1.id, table1.name, table2.facebook_link FROM 'table1' RIGHT JOIN 'table2' ON table1.id = table2.customer_id
```
## IS CONDITION
You can get also the specific data with the IS condition
```
SELECT table1.id, table1.name, table2.facebook_link FROM 'table1' LEFT JOIN 'table2' ON table1.id = table2.customer_id WHERE table2.column_name IS NULL;
```
## Multiple JOIN
```
SELECT table1.id, table1.name, table2.facebook_link FROM 'table1' JOIN 'table2' ON table1.id = table2.customer_id
JOIN table3 ON table3.id = table2.id;
```

Note: When the Many to Many relationship is created on the database, usually we take a 3rd table which name is **pivot table** or **junction table**.