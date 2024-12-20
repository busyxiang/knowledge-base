## Connection
### Local Connection
```bash
psql -U postgres -h localhost
```
### Remote Connection
```bash
psql -h [HOST] -p [PORT] -d [DB_NAME] -U [USER]
```
## Database Operations
### List Databases
```bash
\l  # Inside psql
```
```sql
SELECT datname FROM pg_database;  -- SQL equivalent
```
## Table Operations
### List Tables
```bash
\dt  # Inside psql
```
```sql
SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';  -- SQL equivalent
```
## Query Operations
### JSON Operations
```sql
-- Update a JSON field
UPDATE table SET column = jsonb_set(column, '{field}', '"new_value"') WHERE id = 1;

-- Extract a JSON field
SELECT column->>'field' FROM table;
```
### Array Operations
```sql
-- Add an item to an array
UPDATE table SET column = column || '{VALUE}' WHERE id = 1;

-- Remove an item from an array
UPDATE table SET column = array_remove(column, 'value_to_remove') WHERE id = 1;

-- Check if an array contains a value
SELECT * FROM table WHERE 'value' = ANY(column);
```
### Advanced Queries
#### Update Using Two Tables
```sql
UPDATE table1
SET column_to_update = new_value
FROM table2
WHERE table1.common_column = table2.common_column
AND table2.some_column = some_value;
```
#### Insert into Select
```sql
INSERT INTO payments_adyen (table_a_fk, column_a, column_b, column_c)
SELECT id, $1 AS column_a, $2 AS column_b, $3 AS column_c
FROM table_a
WHERE pubic_id = $4;
```

```sql
INSERT INTO archived_orders (order_id, customer_id, order_date, total_amount, archived_date)
SELECT order_id, customer_id, order_date, total_amount, $2 AS archived_date
FROM orders
WHERE order_date < $1;
```
## User and Permissions
### Create User
```sql
CREATE USER [USERNAME] SUPERUSER;
```
### List Users
```sql
SELECT usename FROM pg_user;
```
# Best Practice
- [Don't Do This](https://wiki.postgresql.org/wiki/Don't_Do_This#Don.27t_use_char.28n.29)