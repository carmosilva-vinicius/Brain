In [[SQL Server]], default values play a crucial role in defining how data behaves when it is inserted or updated in tables. Understanding how to specify and work with default values for different data types such as `NULL`, `NOT NULL`, strings, integers, and dates is essential for database design and management.
### Null Values
- A `NULL` value represents missing or unknown data. It is not equivalent to zero or an empty string (`''`). When a column allows `NULL` values, it means that the column can store data that is intentionally left blank or undefined.
- To explicitly allow `NULL` values in a column, you don't need to do anything special during table creation. However, if you want to ensure that a column never accepts `NULL` values, you can use the `NOT NULL` constraint.
### Not Null Constraint
- The `NOT NULL` constraint ensures that a column cannot have a `NULL` value. This means every record must have a value for this column upon insertion or update. Attempting to insert or update a record without providing a value for a `NOT NULL` column will result in an error [2](https://www.w3schools.com/sql/sql_notnull.asp).
### Strings
- For string data types like `VARCHAR`, `NVARCHAR`, etc., you can specify a default value directly in the column definition. For example, `VARCHAR(100) DEFAULT 'Default Value'`. This sets a default string value for records where no explicit value is provided.
- Alternatively, you can use the `ISNULL()` function to replace `NULL` values with a specified string after data has been inserted or updated. For instance, `SELECT ISNULL(column_name, 'Default String') FROM table_name`.
### Integers
- Similar to strings, you can define a default value for integer columns directly in the column definition, such as `INT DEFAULT 0`.
- To replace `NULL` values with a specific integer after data manipulation, you can use the `COALESCE()` function, which returns the first non-NULL value in a list. For example, `SELECT COALESCE(column_name, 0) FROM table_name`.
### Dates
- For date and time data types, you can specify a default value using functions like `GETDATE()` to automatically insert the current date and time. For example, `DATETIME DEFAULT GETDATE()`.
- To handle `NULL` values in date columns, you might encounter scenarios where `NULL` values are represented as `'1900-01-01 00:00:00.000'` due to the underlying storage mechanism. To replace these with an empty string or another placeholder, you can use `ISNULL()` or `COALESCE()` combined with `CONVERT()` to change the data type temporarily, allowing for replacement logic [1](https://stackoverflow.com/questions/19930599/change-null-values-in-datetime-format-to-empty-string).
### Example
`CREATE TABLE Employees (     ID INT PRIMARY KEY,     FirstName NVARCHAR(50),     LastName NVARCHAR(50) NOT NULL,     HireDate DATETIME DEFAULT GETDATE(),     Salary DECIMAL(10, 2) NOT NULL DEFAULT 50000 );`

In this example:
- `FirstName` and `HireDate` columns allow `NULL` values.
- `LastName` and `Salary` columns are defined with the `NOT NULL` constraint, meaning they must always have a value.
- `HireDate` uses `DEFAULT GETDATE()` to automatically insert the current date and time if no value is provided.
- `Salary` defaults to `50000` if no value is specified.

Understanding and correctly applying default values and constraints in SQL Server helps in designing robust databases that enforce data integrity and business rules effectively.