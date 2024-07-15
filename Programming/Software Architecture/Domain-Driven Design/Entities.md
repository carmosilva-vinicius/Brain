In Domain-Driven Design ([[DDD]]), **Entities** serve as fundamental building blocks representing unique and identifiable objects within the domain. These objects possess a distinct identity throughout their lifecycle, mirroring real-world entities that exist independently. Entities are typically modeled as persistent objects within the system, allowing for the tracking of changes and states over time. For instance, a `Customer` entity in an e-commerce application would have a unique identifier (`customerId`) that remains constant even if other attributes change, reflecting the entity's persistence and uniqueness.

```java
public class Car { 
	private final String licensePlate;
	private final Color color; 
	
	public Car(String licensePlate, Color color) { 
		this.licensePlate = licensePlate; 
		this.color = color; 
	}
}
```