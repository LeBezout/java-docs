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

| JUnit 4 | JUnit 5 |
|---------|---------|
| `@Test(expected = MyException.class)` | `Assertions.assertThrows(MyException.class, () -> { ... });` |
| `@Test(timeout = 10_000)` | `Assertions.assertTimeout(Duration.ofMillis(10_000), () -> { ... });` |
| `@Before` | `@BeforeEach` |
| `@After` | `@AfterEach` |
| `@BeforeClass` | `@BeforeAll` |
| `@AfterClass` | `@AfterAll` |
| `@Ignore` | `@Disabled` |
| `@Category` | `@Tag` |
| `@RunWith` | `@ExtendWith` |
| `@Rule` | `@ExtendWith` |
| `@ClassRule` | `@ExtendWith` |
| :no_entry_sign: | `@DisplayName` |
| `org.junit.Assert` | `org.junit.jupiter.api.Assertions` |

## Migrating from JUnit 4

:information_source: [junit.org - 6. Migrating from JUnit 4](https://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4)

### Maven

Instruct _Maven Surefire Plugin_ to use the **JUnit Platform Surefire Provider** :

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>2.19.1</version>
      <dependencies>
        <dependency>
          <groupId>org.junit.platform</groupId>
          <artifactId>junit-platform-surefire-provider</artifactId>
          <version>1.1.0</version>
        </dependency>
      </dependencies>
    </plugin>
  </plugins>
</build>
```

## New

### Annotations

* [JUnit Jupiter Annotations](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations)

### Assertions

* `Assertions.assertAll()`

### Assumptions

TODO
