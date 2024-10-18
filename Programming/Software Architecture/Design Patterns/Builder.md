Is a creaational [[Design Patterns]] that allows for the step-by-step construction of complex objects. It separates the construction of an object from its representation, enabling the same construction process to create different representations of an object. This pattern is particularly useful when an object requires a significant amount of configuration or when the construction process is complex and involves many optional components.

Here's a simplified example to illustrate the Builder pattern:

```java
public class Car {
    private String color;
    private String model;
    private int year;

    private Car(CarBuilder builder) {
        this.color = builder.color;
        this.model = builder.model;
        this.year = builder.year;
    }

    public static class CarBuilder {
        private String color;
        private String model;
        private int year;

        public CarBuilder(String color) {
            this.color = color;
        }

        public CarBuilder model(String model) {
            this.model = model;
            return this;
        }

        public CarBuilder year(int year) {
            this.year = year;
            return this;
        }

        public Car build() {
            return new Car(this);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car.CarBuilder("Red")
               .model("Toyota")
               .year(2020)
               .build();

        System.out.println("Car color: " + car.color);
        System.out.println("Car model: " + car.model);
        System.out.println("Car year: " + car.year);
    }
}

```


In this example, a `Car` object is constructed using a `CarBuilder`. The `CarBuilder` class provides methods to set the color, model, and year of the car. The `build()` method constructs the `Car` object. This approach allows for a clear separation between the construction of the `Car` object and its representation, making the code more readable and maintainable.

The Builder pattern is beneficial in scenarios where:

- An object has many optional components or configurations.
- The construction of an object involves a step-by-step process.
- Constructors with multiple parameters become unwieldy.
- Immutable objects need to be constructed gradually.
- Different configurations or variations of an object need to be created flexibly.
- A common interface is needed for constructing different representations of an object.

This pattern helps in avoiding the telescoping constructor problem, where constructors with many parameters can become difficult to manage and use. By using the Builder pattern, you can construct objects step by step, making the code cleaner and more understandable.

```java
public class Pizza {
    private String massa;
    private String molho;
    private boolean queijo;
    private boolean calabresa;
    private boolean champignon;

    public Pizza(PizzaBuilder builder) {
        this.massa = builder.massa;
        this.molho = builder.molho;
        this.queijo = builder.queijo;
        this.calabresa = builder.calabresa;
        this.champignon = builder.champignon;
    }

    public static class PizzaBuilder {
        private String massa;
        private String molho;
        private boolean queijo;
        private boolean calabresa;
        private boolean champignon;

        public PizzaBuilder(String massa, String molho) {
            this.massa = massa;
            this.molho = molho;
        }

        public PizzaBuilder queijo(boolean queijo) {
            this.queijo = queijo;
            return this;
        }

        public PizzaBuilder calabresa(boolean calabresa) {
            this.calabresa = calabresa;
            return this;
        }

        public PizzaBuilder champignon(boolean champignon) {
            this.champignon = champignon;
            return this;
        }

        public Pizza build() {
            return new Pizza(this);
        }
    }
}
```

```java
Pizza pizza = new Pizza.PizzaBuilder("Tradicional", "Tomate com manjericão")
            .queijo(true)
            .calabresa(true)
            .champignon(true)
            .build();

```