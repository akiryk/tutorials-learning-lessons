# Databases

## SQL
First, just go watch the [Frontend Masters course](https://frontendmasters.com/courses/databases/introducing-join/).

SQL (pronounced *ess-q-ell*) is a relational database. You have tables that are connected to each other by *foreign keys*. For example, the users table is connected to the comments table by user_id. `\d table_name` will describe the table, which will show something like following:
```SQL
 Table: public.users
 Column   |            Type             | Collation | Nullable |           Default
------------+---------------------------+-----------+----------+------------------------------
 user_id    | integer                   |           | not null | generated always as identity
 username   | character varying(25)     |           | not null |
 email      | character varying(50)     |           | not null |
 
 Table: public.comments
    Column  |            Type           | Collation | Nullable |           Default
------------+---------------------------+-----------+----------+------------------------------
 comment_id | integer                   |           | not null | generated always as identity
 user_id    | integer                   |           |          |
 board_id   | integer                   |           |          |
 comment    | text                      |           | not null |
```

### Basic Search
Use `SELECT`, `FROM`, etc. For help just enter `\h` or `\?`. 
```SQL
# semicolon is critical
SELECT * FROM boards WHERE board_id=1;
```

### JOIN
Use JOIN to get data from more than one table. Get the username of the user who left comment 1.
```SQL
SELECT users.username 
  FROM comments 
  INNER JOIN users 
  ON users.user_id = comments.user_id 
  WHERE comment_id = 1;
 
 # gives back username: somename
```
