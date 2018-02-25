# JUnit 5 - Cheat Sheet

## Requirements

* Java 8

* Dependency :

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.1.0</version>
    <scope>test</scope>
</dependency>
```

## JUnit 4 vs JUnit 5

| Junit 4 | JUnit 5 |
|---------|---------|
| `@Test(expected = MyException.class)` | `Assertions.assertThrows(Exception.class, () -> { ... });` |
| `@Test(timeout = 10_000)` | `Assertions.assertTimeout(Duration.ofMillis(1), () -> { ... });` |
| `@Before` | `@BeforeEach` |
| `@After` | `@AfterEach` |
| `@BeforeClass` | `@BeforeAll` |
| `@AfterClass` | `@AfterAll` |
| `@Ignore` | `@Disabled` |
| `@Category` | `@Tag` |
| `@RunWith` | `@ExtendWith` |
| `@Rule` | `@ExtendWith` |
| :no_entry_sign: | `@DisplayName` |

## New

### Annotations

* [JUnit Jupiter Annotations](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations)

### Assertions

* `Assertions.assertAll()`

### Assumptions

TODO
