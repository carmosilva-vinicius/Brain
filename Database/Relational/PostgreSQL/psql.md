**List All Databases**: Once connected, you can list all databases by using the `\l` or `\list` meta-command. This will display a list of all databases along with their owners, encoding, collation configurations, and access privileges.
```
\l
```

**Additional Information**: If you want more detailed information about each database, including size, tablespace, and description, you can use the `\l+` command instead.
```
\l+
```

**Switch to a Database**: From within `psql`, you can switch to a specific database using the `\c` or `\connect` command followed by the database name.
```
\c your_database_name
```

**List Tables**: After switching to the desired database, you can list its tables using the `\dt` command.
```
\dt
```

**Describe Table Structure**: To see the columns and details of a table named `your_table_name` in the `public` schema, use:
```
\dt your_table_name
```