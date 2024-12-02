A **relational database** is a type of database that stores and organizes data in a structured way. It uses a structure that allows data to be identified and accessed in relation to other data in the database. Data in a [relational database](https://roadmap.sh/sql) is stored in various data tables, each of which has a unique key identifying every row.

Relational databases are made up of a set of tables with data that fits into a predefined category. Each table has at least one data category in a column, and each row contains a certain data instance for the categories defined in the columns.

## ACID
ACID are the four properties of relational database systems that help in making sure that we are able to perform the transactions in a reliable manner. It’s an acronym which refers to the presence of four properties: **atomicity**, **consistency**, **isolation** and **durability.**

- **Atomicity**: This property ensures that all operations within a [[Transaction|transaction]] are either completed successfully or none of them are executed at all. In case of any failure, the transaction is aborted and the database is returned to its previous state [mongodb.com](https://www.mongodb.com/basics/acid-transactions).
- **Consistency**: Consistency ensures that a transaction only makes changes to the database in a predefined, predictable way, maintaining the integrity of the data. Any update operation within a transaction must adhere to the database's constraints, or the transaction should be aborted [mongodb.com](https://www.mongodb.com/basics/acid-transactions).
- **Isolation**: This property guarantees that concurrent transactions do not interfere with or affect one another. Each transaction occurs as if it were happening sequentially, even though they might be occurring simultaneously [mongodb.com](https://www.mongodb.com/basics/acid-transactions).
- **Durability**: Durability ensures that changes made to the database by successfully executed transactions are saved permanently, even in the event of system failure. This is typically achieved through the use of changelogs or write-ahead logs [bmc.com](https://www.bmc.com/blogs/acid-atomic-consistent-isolated-durable/).
