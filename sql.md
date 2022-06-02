# SQL

## CRUD
- Create in SQL is achieved with the `INSERT` command
- Retrieve with `SELECT`
- Update with `UPDATE`
- Delete with `DELETE`

SQL is a relational database, meaning it's comprised of tables made of rows and columns. 
A row is often called a `record`
A column is often called a `field`
Each row has a unique `key`. The column used as the unique key is called the `primary key`
We use the keys to create relationships; thus, our relational database.
A table that relates to another table is connected via a `foreign key`. The image below shows foreign keys that connect the SALE table with the ITEM and CUSTOMER tables.

<img width="1094" alt="image" src="https://user-images.githubusercontent.com/2437758/171489555-2ca17cc0-b82c-4656-b875-bd7641765a55.png">

## Syntax
Semicolon is not always required but often is, so best practice to use it.

A query is comprised of statements, which includes keywords such as `SELECT`, `FROM`, `ORDER BY`, etc.

## Retrieve Data
```sql
# sqllite uses limit
SELECT * FROM Countries LIMIT 10;

# Get the next 10
SELECT * FROM Countries LIMIT 10 OFFSET 10;

# sqlserver uses the TOP keyword instead of LIMIT 
SELECT TOP 10 * FROM Countries;
```
Narrow the resulting fields with column names. 

Note that the clauses in SQL need to be in a particular sequence: generally, most implementations require:

`SELECT` > `FROM` > `WHERE` in that order.

`ORDER BY` must follow any `WHERE` clause; `LIMIT` and `OFFSET` need to be last.
```sql
SELECT Name, LifeExpectancy FROM Countries ORDER BY LifeExpectancy;
```

Use `COUNT` to print the number of records
```sql
# Gives all the rows in the table
SELECT COUNT(*) FROM Country;

# Gives only the rows that have a value for that column
SELECT COUNT(LifeExpectancy) FROM Country;
```

More complex query:
```sql
SELECT Name AS Country, SurfaceArea AS "Surface Area" 
  FROM Country 
  WHERE SurfaceArea > 100000 
  AND Continent = "Europe" 
  ORDER BY SurfaceArea DESC
  LIMIT 5;
```
The above returns something like this:

<img width="512" alt="image" src="https://user-images.githubusercontent.com/2437758/171496799-a91d24eb-132b-4e6f-b11f-153178a25a22.png">

## Create, Update, Delete
```sql
# Name the fields you want to insert into. 
# The following will have NULL as the value for any other columns, e.g. zip or phone.
INSERT INTO customer (name, address, state) 
  VALUES ('Janet Gummy', '1 Old Log Avenue', 'Parkertown');

UPDATE customer SET zip = 023313, city = "Boston", state = "Massachusetts" WHERE ID = 6;

DELETE FROM customer WHERE ID = 5;