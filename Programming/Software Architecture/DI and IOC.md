Dependency Injection (DI) and Inversion of Control (IoC) are fundamental concepts in software development aimed at reducing coupling between components and facilitating maintenance, testing, and extensibility of code. Let's delve deeper into these concepts.

# Dependency Injection (DI)

Dependency Injection is a design pattern where dependencies of an object are supplied to it through constructors, configuration methods, or even method parameters, instead of being instantiated within the object itself. This means that the object is not responsible for creating its own dependencies but receives them from outside.

For example, instead of class A instantiating class B directly inside one of its methods, class B would be injected into class A via a constructor or configuration method. This makes class A more flexible, as it can receive different implementations of B without needing to be modified.

# Inversion of Control (IoC)

Inversion of Control is a design principle that complements Dependency Injection. It suggests that the responsibility for configuring and managing an object's dependencies should be inverted, i.e., delegated to an external component (usually an IoC container) instead of being handled internally by the object itself.

In simpler terms, objects delegate the creation and management of their dependencies to an external mechanism. This allows for greater flexibility and decoupling between components, as dependencies can be easily replaced or configured without altering the code of dependent objects.

## Together

Dependency Injection and Inversion of Control are often used together to promote a more flexible, modular, and testable software design. They facilitate the creation of independent and reusable components, promoting cohesion and separation of concerns.

A practical example of using these concepts is in dependency injection frameworks like Spring (for Java) or Angular (for JavaScript), where objects are externally configured and managed through configuration files or annotations, allowing for more flexible configuration and easy replacement of dependencies.

In Spring, application components are typically managed by the Spring container. To have an object managed by Spring, it must be annotated to identify it as a Spring component. Common annotations for this purpose are @Component, @Service, @Repository, and @Controller, depending on the type of component being defined.

Once application components are managed by Spring, dependencies can be injected into them using annotations. The most common annotation for injecting dependencies is @Autowired. When a component is marked with @Autowired, Spring automatically searches for an appropriate instance of the dependency type and injects it into the component.

To ensure Spring recognizes and manages application components, component scanning needs to be configured in the Spring configuration file (usually an XML file or a Java configuration class), similar to how we configured our UsuarioConfig class using the @Configuration annotation and also annotating our methods with the @Bean annotation, used to define methods that produce instances of objects to be managed by the Spring container.