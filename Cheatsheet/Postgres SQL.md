# Connect to DB
## Local
```bash
psql -U postgres -h localhost
```
## Remote
```bash
psql -h 127.0.0.1 -p [PORT] -d [DB_NAME] -U [USER]
```
# Query
## Update

### JSON
```sql
update TABLE set COLUMN = jsonb_set(COLUMN, '{FIELD}', 'true') where id = 2;
```
### Array
#### Add Item
```sql
update TABLE set COLUMN = COLUMN || '{VALUE}' where id = 2
```
#### Remove Item
```sql
update TABLE set COLUMN = array_remove(COLUMN, 'VALUE') where id = 1
```
### Advanced
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
# User
## Create
```sql
CREATE USER postgres SUPERUSER;
```
# Command
## List All Databases
```bash
\l
```
# Best Practice
- [Don't Do This](https://wiki.postgresql.org/wiki/Don't_Do_This#Don.27t_use_char.28n.29)