Clean [[Software Architecture|Architecture]], proposed by Robert C. Martin ("Uncle Bob"), aims to create systems that are independent of frameworks, UIs, and databases. It outlines a layered architecture where the core application contains the most important business rules, and external layers contain implementation details.

Key principles include:

- **Framework Independence**: The source code should not depend on any specific framework. Frameworks are external and volatile tools that may change over time, so the architecture should be designed to isolate the application code from these changes.
- **User Interface Independence**: The application's business logic should not be directly tied to the user interface (UI). This allows different UIs (web interfaces, REST APIs, command-line interfaces, etc.) to easily connect to the same business logic.
- **Database Independence**: Similar to the UI, data access code should not be directly coupled with the business logic. This enables easy substitution or alteration of different data storage systems (SQL databases, NoSQL, cloud storage services, etc.) without affecting the business logic.
- **Policy Independence**: Business rules should be independent of implementation details, such as persistence policies, UI policies, security policies, etc. This allows different policies to be easily swapped or modified without altering the core application.

Based on these principles, clean architecture organizes code into concentric layers, with the core application (known as "business entities" or "domain") surrounded by layers containing implementation details, such as user interfaces, data access, etc. These layers are organized in a concentric ring format, with the core application at the center and outer layers around it.

Typical layers in clean architecture include:

- **Business Entities**: The innermost layer containing domain entities or business objects representing concepts of the application's domain. These encapsulate the state and behavior of the application and are independent of any implementation details.
- **Use Cases or Interactors**: This layer contains the application's use cases or services offered to users. Use cases orchestrate the execution of business operations using domain entities and coordinate interaction with external layers.
- **Controllers, Presenters**, and Gateways: Outer layers responsible for translating UI inputs and outputs to application use cases and vice versa. They adapt data and events between the UI and use cases, ensuring separation of responsibilities and independence between these layers.
- **User Interfaces**, Frameworks, and Drivers: This layer contains user interfaces (web interfaces, REST APIs, command-line interfaces, etc.), responsible for receiving user requests, presenting information, and collecting inputs. It also contains implementation-specific details, such as frameworks, libraries, and drivers for infrastructure handling, like data access and network communication. These details are encapsulated and isolated from the application's internal layers.

![[CleanArchitecture.jpg]]

Clean architecture is not prescriptive about specific technologies or directory structures. It provides general architectural guidelines and principles that can be applied in various ways, depending on the specific needs and requirements of the project.

In summary, the main objectives of these three types of architecture are the development of well-structured, testable, scalable software, independent of frameworks, with clear separation of responsibilities and a strong emphasis on cohesion, modularity, and dependency inversion.