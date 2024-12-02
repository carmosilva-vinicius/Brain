In short, a [[Database]] transaction is a sequence of multiple operations performed on a database, and all served as a single logical unit of work — taking place wholly or not at all. In other words, there’s never a case where only half of the operations are performed and the results saved.

#### Example: 
```sql
-- Create a sample table
CREATE TABLE accounts (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    balance NUMERIC(10, 2)
);

-- Insert initial data
INSERT INTO accounts (name, balance) VALUES ('Alice', 1000.00);
INSERT INTO accounts (name, balance) VALUES ('Bob', 500.00);

-- Begin a transaction
BEGIN;

-- Attempt to transfer $200 from Alice to Bob
UPDATE accounts SET balance = balance - 200 WHERE name = 'Alice';
UPDATE accounts SET balance = balance + 200 WHERE name = 'Bob';

-- Print account balances
SELECT name, balance FROM accounts;

-- Commit the transaction (optional, since we're about to rollback)
-- COMMIT;

-- Simulate an error (e.g., insufficient funds)
UPDATE accounts SET balance = balance - 300 WHERE name = 'Alice';

-- Rollback the transaction
ROLLBACK;

-- Print final account balances
SELECT name, balance FROM accounts;

-- Clean up (drop the table)
DROP TABLE accounts;
```
### Summary of the code and best practices:
1. We created a simple `accounts` table to demonstrate the transaction.
2. We started a transaction using `BEGIN;`.
3. We attempted to transfer $200 between accounts using `UPDATE` statements.
4. We printed the account balances to show the intermediate state.
5. We simulated an error by attempting to withdraw more than Alice had.
6. We rolled back the transaction using `ROLLBACK;`.
7. Finally, we printed the final account balances to show the rollback effect.
8. We cleaned up by dropping the temporary table.

Best practices demonstrated:
- Using explicit transaction control (`BEGIN`, `COMMIT`, `ROLLBACK`).
- Checking for sufficient funds before performing transfers.
- Cleaning up temporary objects after demonstration.

This example demonstrates how transactions ensure data consistency and integrity in PostgreSQL. If any part of the transaction fails (like the second UPDATE statement), the entire transaction is rolled back, maintaining the database's integrity.

#### Example with [[ORM]]
```cs
public class Program
{
    public static void Main()
    {
        using var connection = new NpgsqlConnection("your_connection_string_here");
        connection.Open();

        using var context1 = new Context1(connection);
        using var context2 = new Context2(connection);

        using (var transaction = connection.BeginTransaction())
        {
            try
            {
                // Perform operations on Context1
                context1.SomeEntity.Add(new SomeEntity { Name = "Test" });
                context1.SaveChanges();

                // Perform operations on Context2
                context2.AnotherEntity.Add(new AnotherEntity { Name = "Another Test" });
                context2.SaveChanges();

                // Commit the transaction
                transaction.Commit();
                Console.WriteLine("Both contexts were updated successfully.");
            }
            catch (Exception ex)
            {
                // Rollback the transaction if an exception occurs
                transaction.Rollback();
                Console.WriteLine($"An error occurred: {ex.Message}");
            }
        }
    }
}
```