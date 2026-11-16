# Coding-Rules Profile: java-spring-boot

## Versions and framework
- Java with Spring Boot, built with Maven. Use the versions already declared in the project; do not change them.
- Static analysis: Checkstyle and SpotBugs.

## Project layout
- Standard Maven layout: `src/main/java`, `src/main/resources`, `src/test/java`.
- Package by feature under the root package of the `@SpringBootApplication` class; never the default package.
- Layers: controller (HTTP boundary only) -> service (business logic, transactions) -> repository (persistence).
- DTOs at the API boundary; entities never leave the service layer.
- Detailed Java, Spring, JPA, security, Maven and testing practices live in `.github/rules/java-*.instructions.md`, `spring-*.instructions.md` and `maven.instructions.md`.

## Naming
- Packages lowercase; classes `UpperCamelCase`; methods and fields `lowerCamelCase`; constants `UPPER_SNAKE_CASE`.
- Suffixes: `*Controller`, `*Service`, `*Repository`, `*Dto`; test classes `*Test`.

## Error handling
- Centralise error translation in a `@RestControllerAdvice` returning RFC 9457 `ProblemDetail`.
- Throw specific exceptions from services; never swallow exceptions; preserve the cause when wrapping.
- Validate input with `@Valid` on request bodies and parameters.
- Never expose stack traces or internal messages in responses.

## Testing conventions
- JUnit Jupiter, AssertJ and Mockito, with tests mirroring the main package under `src/test/java`.
- Unit-test services with mocked repositories; slice tests (`@WebMvcTest`, `@DataJpaTest`) for controllers and repositories.
- Tests are written, never run.

## Build command
`mvn -B -q compile`

## Lint command
`mvn -B -q checkstyle:check spotbugs:check`

## Prerequisites
- Maven available on the path, with the Checkstyle and SpotBugs plugins and their configs already configured in the project.
- Dependencies already resolved locally.

## Additional denied paths
- `target/`

## Forbidden commands
- `mvn install`
- `mvn deploy`
- `mvn test`
- `mvn verify`

## Protected config files
- `pom.xml`
- Checkstyle configuration
- SpotBugs configuration

## Forbidden patterns
- Field injection and setter injection; `@Autowired` belongs only on a constructor (use constructor injection only).
- Eagerly injected rarely used dependencies (mark the constructor parameter `@Lazy` or use `ObjectProvider<T>`).
- `printStackTrace`.
- SQL built from strings.
- Unsafe deserialization.
- Entities returned from controllers.
- `@CrossOrigin("*")`.
- CSRF disabled without a written justification.
- Secrets in `application*.yml` or `application*.properties`.
- `System.out` / `System.err` instead of SLF4J.
- `@Transactional` on controllers.
- `FetchType.EAGER` on collections.
- `@Data`, `@EqualsAndHashCode` or `@ToString` on JPA entities.
- `Optional.get()` without a presence check.
- `Date`, `Calendar` or `SimpleDateFormat` (use `java.time`).
- `double` or `float` for monetary values.
- `spring.jpa.hibernate.ddl-auto` set to `create`, `create-drop` or `update` outside local development.

## Stack-specific security rules
- Spring Security with deny-by-default: every endpoint requires authentication unless explicitly permitted.
- Restrict CORS to named origins.
- Declare a `SecurityFilterChain` bean ending with `anyRequest().authenticated()`.
- Check resource ownership on identifier lookups; use `@PreAuthorize` where authorisation depends on the resource.
- Hash passwords with a `DelegatingPasswordEncoder`, BCrypt or Argon2.
