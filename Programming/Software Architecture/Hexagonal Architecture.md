Also known as Ports and Adapters architecture, proposed by Alistair Cockburn in 2005. This [[Software Architecture|architecture]] isolates the application's core logic, which contains business logic, from any implementation details such as database interfaces, user interfaces, and external services. This isolation is achieved through the concept of "ports" and "adapters":

- **Ports**: These are interfaces that define contracts between the application's core and external components. For instance, a port could be an interface defining methods for accessing database data or handling HTTP requests.
    
- **Adapters**: These are concrete implementations of the ports. They connect the application's core with external components, translating the core's method calls into the specific APIs of those external components. For example, an adapter might implement a database access interface using JDBC or Hibernate.
    

The Hexagonal Architecture promotes modularity and code reuse, allowing each component to be replaced or altered without affecting the rest of the system, as long as it adheres to the contract defined by the ports. This also facilitates testing by enabling the substitution of real implementations with mocks or stubs during unit tests.

Furthermore, it simplifies integration with external systems like third-party APIs, legacy systems, and cloud services, as these integrations are handled by adapters that can be easily replaced or reconfigured.

![[hexagonal.png]]