[[Programming/Software Architecture/Clean Architecture/Value Objects|Value Objects]] are another crucial component in [[DDD]], characterized by their simplicity and immutability. They encapsulate simple values or collections thereof, which are considered as a single unit based on their attributes. Unlike Entities, Value Objects do not possess a conceptual identity and are defined solely by their attribute values. Examples include dates, geographical coordinates, or color specifications. In a banking application, a `Money` value object could represent an amount of money, consisting of a currency and an amount, without having an identity of its own.

```java
public class Color { 
	private final String name;
	public Color(String name) {
		this.name = name; 
	}
}
```