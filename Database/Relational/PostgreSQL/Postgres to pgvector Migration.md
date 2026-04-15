# PostgreSQL to pgvector Migration Guide

This guide explains how to migrate your existing PostgreSQL data to a new `pgvector` container.

## 1. Prerequisites
- Both containers must be running or accessible via Docker.
- New volumes `pgvector_data` and `pgadmin_vector_data` must be created.

## 2. Backup Current Database
Use `pg_dumpall` to create a complete backup of all databases, roles, and schemas from the original PostgreSQL container.

```bash
docker exec -t postgres pg_dumpall -c -U postgres > full_dump.sql
```
*Note: The `-c` flag adds commands to drop databases before creating them, which is useful for a clean restore.*

## 3. Prepare pgvector Container
Ensure your new `pgvector` service is running:
```bash
cd pgvector
docker compose up -d
```

## 4. Restore Data to pgvector
Pipe the dump file into the new container's `psql` utility.

```bash
cat full_dump.sql | docker exec -i pgvector psql -U postgres
```

## 5. Enable pgvector Extension
Once the data is restored, you can enable the `vector` extension on any database where you need RAG features (like the `LibreChat` database).

Connect via `pgadmin` (at port 8091) or use the CLI:
```bash
docker exec -it pgvector psql -U postgres -d your_database_name -c "CREATE EXTENSION IF NOT EXISTS vector;"
```

## 6. Cleanup
After verifying that all data and the `vector` extension are working correctly in the new container:
- You can stop and remove the old `postgres` container.
- Delete the `full_dump.sql` file.

---
**Note on Versions:**
The image `pgvector/pgvector:0.8.2-pg18-trixie` uses:
- **pgvector 0.8.2**: Latest extension version.
- **Postgres 18**: Upcoming major release (bleeding edge).
- **Trixie**: Debian 13 "Testing" branch.
