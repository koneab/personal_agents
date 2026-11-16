---
description: JUnit, Mockito and Spring Boot test rules for Java test sources.
applyTo: 'src/test/java/**/*.java'
---

## Structure and naming
- Mirror the main package; name test classes `<ClassUnderTest>Test` (unit/slice) or `<Feature>IT` (integration).
- One behavior per test; name methods after the behavior, e.g. `rejectsOrderWhenStockIsInsufficient`.
- Use `@DisplayName` only when the method name cannot express the behavior clearly.
- Use arrange / act / assert, separated by blank lines; no logic (loops, conditionals) in tests.
- Use `@ParameterizedTest` with `@CsvSource` / `@MethodSource` instead of copy-pasted tests.

## Frameworks
- Use JUnit Jupiter and AssertJ (`assertThat`); use `assertThatThrownBy` / `assertThrows` for exceptions.
- Use Mockito for collaborators; prefer `@ExtendWith(MockitoExtension.class)` with `@Mock` and `@InjectMocks` or explicit constructor wiring.
- Mock only external boundaries and direct collaborators; never mock the class under test or value objects.
- Verify interactions only when they are the behavior; prefer asserting on results and state.

## Spring Boot tests
- Prefer plain unit tests for services; no Spring context when none is needed.
- Use slice tests: `@WebMvcTest` for controllers (with `MockMvc` and `@MockitoBean` / `@MockBean` for services), `@DataJpaTest` for repositories.
- Use `@SpringBootTest` sparingly, for a few end-to-end paths; set `webEnvironment` explicitly.
- Use Testcontainers for database and broker integration tests instead of in-memory substitutes with different SQL semantics.
- Keep the Spring context cache effective: avoid unnecessary `@DirtiesContext` and per-test property overrides.
- Test security rules explicitly (`@WithMockUser`, unauthenticated and forbidden cases).

## Data and isolation
- Build test data with small builders or factory methods; keep each test's data local to it.
- No shared mutable state or execution-order dependence between tests.
- Inject a fixed `Clock` instead of relying on the system time; no `Thread.sleep` (use Awaitility).
- Never use real external services, secrets or production data.
