PostgreSQL is a powerful, open source object-relational [[database]] system that uses and extends the SQL language combined with many features that safely store and scale the most complicated data workloads. The origins of PostgreSQL date back to 1986 as part of the [POSTGRES](https://www.postgresql.org/docs/current/history.html) project at the University of California at Berkeley and has more than 35 years of active development on the core platform. ([about, 2023](https://www.postgresql.org/about/))

## Setup
A simple [[Docker]] compose setup of Postgre database and PgAdmin manager:
```yml
version: '3.1'

services:
  postgresql:
    container_name: postgresql_database
    image: postgres:15.0
    ports:
      - 5432:5432
    environment:
      POSTGRES_USER: dbuser
      POSTGRES_PASSWORD: dbpassword
    volumes:
      - my-db:/var/lib/postgresql
  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: dbpassword
    ports:
      - 8080:80
volumes:
  my-db:
```

Connecting in Postgres [[CLI]] client:
```bash
docker exec -it postgres-container psql -U dbuser -d dbpassword
```

## Explaining query:
```
EXPLAIN ANALYZE SELECT * FROM tenk1 WHERE ten < 7;
```
response:
```                              QUERY PLAN
-------------------------------------------------------------------​--------------
 Seq Scan on tenk1  (cost=0.00..483.00 rows=7000 width=244) (actual time=0.016..5.107 rows=7000 loops=1)
   Filter: (ten < 7)
   Rows Removed by Filter: 3000
 Planning time: 0.083 ms
 Execution time: 5.905 ms
```

- `cost=0.00..483.00`: 0.00 is the relative cost to query the first row and 483.00 to query the all the others;
- `time=0.016..5.107`: 0.016ms time to receive the first row record and 5.107 ms to receive al the others 6999 rows. Ther first row time is important to  know the latency that the application will have between carrying out the search and receiving the first result.
  