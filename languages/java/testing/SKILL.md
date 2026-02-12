---
name: java-testing
description: Java test pitfalls — JUnit 5 lifecycle, Mockito verification, Spring test context. Load only when writing or reviewing Java test files (*Test.java, *IT.java).
---

# Java Testing — What Claude Gets Wrong

## JUnit 5 Mistakes
- **`@Test` is `org.junit.jupiter.api.Test`** — not the JUnit 4 `org.junit.Test`. Claude mixes them up.
- `@BeforeEach` / `@AfterEach` (JUnit 5) not `@Before` / `@After` (JUnit 4)
- `@DisplayName` for readable test names — Claude rarely adds these
- `assertThrows(ExactException.class, () -> ...)` — not `try/catch` with `fail()`
- `@Nested` for grouping related tests — cleaner than flat test classes

## Mockito Pitfalls
- **`@Mock` requires `@ExtendWith(MockitoExtension.class)`** — Claude often forgets the extension
- `verify(mock, times(1)).method()` — don't over-verify, test behavior not interactions
- `when().thenReturn()` for stubbing, `doReturn().when()` for spies and void methods
- **Never mock the class under test** — mock its dependencies
- `@InjectMocks` creates the subject with mocks injected — but prefer constructor injection in tests too

## Spring Boot Test Mistakes
- `@SpringBootTest` loads full context — slow. Use `@WebMvcTest`, `@DataJpaTest`, `@MockBean` for slices
- `@MockBean` replaces bean in Spring context — different from `@Mock`
- `@Transactional` on test class auto-rolls back — no manual cleanup needed
- `@TestPropertySource` for test-specific config — not hardcoded values

## Integration Tests
- Name convention: `*IT.java` for integration, `*Test.java` for unit
- Use `@Testcontainers` for DB/Redis/Kafka — not H2 as a "replacement" for Postgres
- Maven: `maven-failsafe-plugin` runs `*IT.java` separately from `*Test.java`
