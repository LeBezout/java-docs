# JUnit 5 - Cheat Sheet

## Requirements

* Java 8

* Dependency :

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.4.0</version>
    <scope>test</scope>
</dependency>
```

## JUnit 4 vs JUnit 5

| JUnit 4 | JUnit 5 |
|---------|---------|
| `@Test(expected = MyException.class)` | `Assertions.assertThrows(MyException.class, () -> { ... });` |
| `@Test(timeout = 10_000)` | `Assertions.assertTimeout(Duration.ofMillis(10_000), () -> { ... });` |
| `expectedEx.expect(TechnicalException.class);` + `expectedEx.expectMessage("message");` | `Assertions.assertThrows(MyException.class, () -> { ... }, "message");` |
| `@Before` | `@BeforeEach` |
| `@After` | `@AfterEach` |
| `@BeforeClass` | `@BeforeAll` |
| `@AfterClass` | `@AfterAll` |
| `@Ignore` | `@Disabled` |
| `@Category(Annot.class)` | `@Tag("string")` |
| `@RunWith` | `@ExtendWith` |
| `@Rule` | `@ExtendWith` |
| `@ClassRule` | `@ExtendWith` |
| `@FixMethodOrder(MethodSorters.NAME_ASCENDING)` | `@TestMethodOrder(MethodOrderer.Alphanumeric.class)` |
| :no_entry_sign: | `@DisplayName` |
| :no_entry_sign: | `@DisplayNameGeneration` (only on class) |
| `org.junit.Assert` | `org.junit.jupiter.api.Assertions` |

## Migrating from JUnit 4

:information_source: [junit.org - 6. Migrating from JUnit 4](https://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4)

```xml
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <version>5.4.0</version>
</dependency>
```

### Maven

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>2.22.1</version>
    </plugin>
  </plugins>
  <dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.4.0</version>
    </dependency>
  </dependencies>
</build>
```

## New

### Annotations

* [JUnit Jupiter Annotations](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations)

### Assertions

* `Assertions.assertAll()`

### Assumptions

TODO
