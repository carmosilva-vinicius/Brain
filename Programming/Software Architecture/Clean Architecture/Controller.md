The **Controller** acts as the entry point for handling incoming requests. It receives input, processes it through the application logic, and returns a response. Controllers should be thin, focusing on routing and delegating business logic to other layers. They interact with the Use Case layer but should not contain business rules themselves.

```java
public class UserController {
    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    public UserDto createUser(CreateUserRequest request) {
        return userService.createUser(request);
    }
}

```