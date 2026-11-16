---
description: Spring Boot application structure, dependency injection, REST and error-handling rules.
applyTo: 'src/main/java/**/*.java'
---

## Structure
- Put the `@SpringBootApplication` class in the root package; never use the default package.
- Package by feature (`customer/`, `order/`), each with its controller, service, repository and DTOs; avoid global `controllers/` or `services/` packages.
- Dependencies point inward: controller -> service -> repository. Never call a controller from a service, or a service from a repository.
- Keep `@Configuration` classes small and focused; expose beans with `@Bean` methods, not component scanning of third-party types.

## Dependency injection
- Constructor injection only; put `@Autowired` on the constructor, never on fields or setters.
- With a single constructor `@Autowired` is optional; with several constructors it is required on the one Spring must use.
- In `@Configuration` classes, declare dependencies as parameters of the `@Bean` factory method; do not use `@Autowired` there.
- Store injected dependencies in `private final` fields; no setter or field injection.
- Inject only what the class uses; a long constructor signals a class with too many responsibilities.
- To defer creating a rarely used dependency until first use, mark the constructor parameter `@Lazy` or inject an `ObjectProvider<T>`.
- Do not inject `ApplicationContext` or use `getBean`; depend on the collaborator directly.
- Depend on the narrowest type needed; inject interfaces where more than one implementation exists.

## Controllers
- `@RestController` handles the HTTP boundary only: map request to DTO, call one service method, map result to response DTO.
- No business logic, persistence calls or `@Transactional` in controllers.
- Use `@RequestMapping` on the class for the base path and `@GetMapping`, `@PostMapping`, ... on methods.
- Return `ResponseEntity` only when status or headers vary; otherwise use `@ResponseStatus`.
- Use the correct status codes: `201` with `Location` on create, `204` on empty success, `404` for missing resources, `409` for conflicts.
- Version and name endpoints as plural nouns (`/api/v1/orders`); no verbs in paths.
- Paginate every collection endpoint that can grow (`Pageable`); cap the maximum page size.

## DTOs and mapping
- Separate request and response DTOs; never expose or accept JPA entities at the API boundary.
- Prefer `record` DTOs when the declared Java version supports it.
- Annotate request DTOs with Jakarta Bean Validation (`@NotBlank`, `@Size`, `@Email`, ...) and apply `@Valid` / `@Validated` on the controller parameter.
- Map entities to DTOs in the service layer or a dedicated mapper (MapStruct if already used); never in the entity.
- Use `jakarta.*` imports on Spring Boot 3+; `javax.*` only on Boot 2.x.

## Services and transactions
- `@Service` classes hold business logic and own transaction boundaries.
- Put `@Transactional` on service methods or classes, not on controllers or repositories.
- Use `@Transactional(readOnly = true)` for queries.
- Keep transactions short; no remote calls or blocking I/O inside a transaction.
- Remember that `@Transactional` is proxy-based: self-invocation and `private` methods are not intercepted.

## Error handling
- Define a small domain exception hierarchy (`ResourceNotFoundException`, `ConflictException`, ...) thrown by services.
- Translate exceptions in one `@RestControllerAdvice`, returning RFC 9457 `ProblemDetail` responses.
- Extend `ResponseEntityExceptionHandler` to cover Spring MVC exceptions consistently.
- Never expose stack traces, SQL messages, class names or internal paths in responses.
- Map validation failures to `400` with field-level details.

## Configuration
- Bind configuration with `@ConfigurationProperties` on an immutable record or class, validated with `@Validated`; avoid scattered `@Value`.
- Provide environment-specific values through profiles and environment variables; commit only non-secret defaults.
- Never hard-code URLs, credentials or timeouts that differ per environment.

## Operations
- Expose health and metrics through Spring Boot Actuator; restrict endpoints to the minimum needed and secure the rest.
- Configure timeouts on every outbound HTTP client (`RestClient`, `WebClient`).
- Use `@Async`, scheduling and virtual threads only with an explicitly configured executor and error handling.
