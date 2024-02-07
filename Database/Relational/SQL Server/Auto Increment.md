[[SQL Server]] has the **Identity** property, which creates an identity column in a table.

```sql
IDENTITY [ (seed , increment) ]
```
#### Arguments
- _seed_: The value that is used for the very first row loaded into the table.
- _increment_: The incremental value that is added to the identity value of the previous row that was loaded.
#### Example:
```sql
CREATE TABLE new_employees (
	id_num INT IDENTITY(1, 1),
	fname VARCHAR(20),
	minit CHAR(1),
	lname VARCHAR(30) 
);
```