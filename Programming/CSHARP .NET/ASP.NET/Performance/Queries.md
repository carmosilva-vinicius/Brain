A common problem with queries using [[Entity Framework]], is when we need to fetch data with relation 1:n or n:n. This is why for each row that we fetch for a table another amount off data (provided by the relation) can be fetched. 

Commonly [[Performance and Optimization#Lazy Loading|Lazy Loading]] approach are commonly used in with `virtual` props. But in that way other queries are made before the main one. A  SQL `JOIN`, to aggregate the relation data with in just one query has better performance than this. To achieve this we can use:

```csharp
var products = await _ctx.Products.Where(p => p.Category == category || category == "all").Include(p=> p.Rating).ToListAsync();

//... at the startup:
protected override void OnConfiguring(DbContextOptionsBuilder options)
	=> options
		.UseSqlite($"Data Source={DbPath}")
		.UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking)
		.LogTo(Console.WriteLine, LogLevel.Information);
```
`UseQueryTrackingBehavior` sets the query tracking behavior for the context to `NoTracking`. This means that entities returned from queries are not tracked by the context and changes to them are not automatically persisted.