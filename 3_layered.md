##### Layered (n-tier)

<img src="./layered.png" style="width:550px;" />

+++

- most web services use this pattern
- each layer has distinct role
- number of layers is not strictly defined
- key feature - **separation of concerns** - e.g. components within a specific layer deal only with logic that pertains to that layer
- monolithic

+++

API:

```Java
@Controller("/user")
class UserController {
  IUserService userService;

  @Get("/:id")
  User getUserById(String id) {
    return userService.getUserById(id);
  }
}
```

+++

Service layer:

```Java
class IUserService {
  User getUserById(String id);
}
```

```Java
class UserService implements IUserService {
  UserRepository userRepository;

  User getUserById(String id) {
    User u = userRepository.findById(id);
    if(!u) throw UserNotFoundException();
    u.password = null;
    return u;
  }
}
```

+++

Persistence layer:

```Java
@Repository
class UserRepository extends CrudRepository<UserEntity, String>{}
```

```Java
@Entity("user")
class UserEntity {
  @Id
  String id;
  String name;
}
```
