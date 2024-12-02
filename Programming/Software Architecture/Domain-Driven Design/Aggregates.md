**Aggregates** in [[DDD]] are clusters of related objects treated as a single unit for the purpose of data changes. An Aggregate ensures the integrity of changes to its constituent objects by enforcing consistency rules. Within an Aggregate, one of the entities is designated as the **Aggregate Root**, acting as the entry point for interacting with the Aggregate. The Aggregate Root controls access to the Aggregate, ensuring that all changes are funneled through it to maintain the Aggregate's integrity. For example, in a library management system, a `Book` entity might be the Aggregate Root of an Aggregate that includes `Author`, `Publisher`, and `ISBN` entities, ensuring that all book-related data changes are managed through the `Book`.