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