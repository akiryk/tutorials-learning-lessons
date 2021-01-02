# Databases

## SQL
First, just go watch the [Frontend Masters course](https://frontendmasters.com/courses/databases/introducing-join/).

SQL (pronounced *ess-q-ell*) is a relational database. You have tables that are connected to each other by *foreign keys*. For example, the users table is connected to the comments table by user_id:
```
// \d table_name will describe the table, which will show something like following:
 Column   |            Type             | Collation | Nullable |           Default
------------+-----------------------------+-----------+----------+------------------------------
 user_id    | integer                     |           | not null | generated always as identity
 username   | character varying(25)       |           | not null |
 email      | character varying(50)       |           | not null |
```
