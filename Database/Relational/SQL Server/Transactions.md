Transaction in [[SQL Server]] is a unit of processing that ensures data integrity and consistency. It is used to prevents data corruption by grouping related operations together.

**How it works:**
- **BEGIN TRANSACTION:** Saves the current database state.
- **COMMIT:** Makes all changes since the **BEGIN TRANSACTION** permanent.
- **ROLLBACK:** Discards all changes since the **BEGIN TRANSACTION** and reverts to the saved state.

**Benefits:**
- Ensures data integrity by preventing partial updates or inconsistent data.
- Allows for data recovery in case of errors.
- Improves performance by grouping multiple operations into a single unit.

**Examples:**
```sql
BEGIN TRANSACTION

UPDATE VENDEDORES SET COMISSAO = COMISSAO * 1.1

COMMIT
```

```sql
BEGIN TRANSACTION

INSERT INTO VENDEDORES
VALUES ('239','Maria Joana','Copacabana',0.2,
'2015-01-01',1);

ROLLBACK
```

**Important points:**
- Use **BEGIN TRANSACTION** with caution, as it can lock tables and prevent other users from accessing them.
- Use **COMMIT** to make changes permanent and **ROLLBACK** to undo changes.
- Transactions can be used to improve performance and ensure data integrity.