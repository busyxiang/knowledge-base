# Connect to DB
## Local
```bash
psql -U postgres -h localhost
```
## Remote
```bash
psql -h 127.0.0.1 -p [PORT] -d [DB_NAME] -U [USER]
```
# Update Value

## JSON
```sql
update TABLE set COLUMN = jsonb_set(COLUMN, '{FIELD}', 'true') where id = 2;
```
## Array
#### Add Item
```sql
update TABLE set COLUMN = COLUMN || '{VALUE}' where id = 2
```
#### Remove Item
```sql
update TABLE set COLUMN = array_remove(COLUMN, 'VALUE') where id = 1
```
## Advanced
### Update Using Two Tables
```sql
UPDATE table1
SET column_to_update = new_value
FROM table2
WHERE table1.common_column = table2.common_column
AND table2.some_column = some_value;
```
# Best Practice
- [Don't Do This](https://wiki.postgresql.org/wiki/Don't_Do_This#Don.27t_use_char.28n.29)