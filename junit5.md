# JUnit 5 - Cheat Sheet

## Requirements

* Java 8 or higher

* Dependency :

```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.4.2</version>
  <scope>test</scope>
</dependency>
```

> :bulb: JUnit Jupiter aggregator artifact that transitively pulls in dependencies on `junit-jupiter-api`, `junit-jupiter-params`, and `junit-jupiter-engine` for simplified dependency management in build tools such as Gradle and Maven.

* Dependency Management :

```xml
<dependency>
  <groupId>org.junit</groupId>
  <artifactId>junit-bom</artifactId>
  <version>5.4.2</version>
  <type>pom</type>
  <scope>import</scope>
</dependency>
```

## JUnit 4 vs JUnit 5

| JUnit 4 | JUnit 5 |
|---------|---------|
| `@Test(expected = MyException.class)` | `Assertions.assertThrows(MyException.class, () -> { ... });` |
| `@Test(timeout = 10_000)` | `Assertions.assertTimeout(Duration.ofMillis(10_000), () -> { ... });` |
| `expectedEx.expect(MyException.class);` + `expectedEx.expectMessage("message");` | `MyException ex = Assertions.assertThrows(MyException.class, () -> { ... }); Assertions.assertEquals("message", ex.getMessage());` |
| `@Before` | `@BeforeEach` |
| `@After` | `@AfterEach` |
| `@BeforeClass` | `@BeforeAll` |
| `@AfterClass` | `@AfterAll` |
| `@Ignore` | `@Disabled` |
| `@Category(Annot.class)` | `@Tag("string")` |
| `@RunWith` | `@ExtendWith` |
| `@Rule` | `@ExtendWith` |
| `@Rule public TestName testName = new TestName();` | Inject `TestInfo` as method parameter |
| `@ClassRule` | `@ExtendWith` |
| `@FixMethodOrder(MethodSorters.NAME_ASCENDING)` | `@TestMethodOrder(MethodOrderer.Alphanumeric.class)` (@since 5.4) |
| :no_entry_sign: | `@DisplayName` |
| :no_entry_sign: | `@DisplayNameGeneration` (only on class - @since 5.4) |
| `org.junit.Assert` | `org.junit.jupiter.api.Assertions` |
| public class | package private class |
| public methods | package private methods |

## Migrating from JUnit 4

:information_source: [junit.org - 6. Migrating from JUnit 4](https://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4)

```xml
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <version>5.4.2</version>
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
</build>
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.4.2</version>
  </dependency>
</dependencies>
```

:warning: maven-surefire-plugin version > 2.22.0

## New

### Annotations

* [JUnit Jupiter Annotations](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations)

### Assertions

* `Assertions.assertAll()`

### Assumptions

> [Assumptions](https://junit.org/junit5/docs/current/user-guide/#writing-tests-assumptions) signal that a test should be aborted instead of marked as a failure, and are static methods in the `org.junit.jupiter.api.Assertions` class :

* assumeTrue
* assumeFalse
* assumingThat

### Parameterized Tests

Add **junit-jupiter-params** dependency if we don't use **junit-jupiter** aggregator dependency :

```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter-params</artifactId>
</dependency>
```

:warning: **Use `@ParameterizedTest` instead of `@Test`, not both. Otherwise JUnit throw a `ParameterResolutionException`**

[@ValueSource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-ValueSource) / [@EmptySource / @NullSource / @NullAndEmptySource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-null-and-empty) : 

```java
@ParameterizedTest
@ValueSource(strings = { "v1", "v2", "v3" })  // for non null parameters
@NullSource // for null parameter
void test_something(String param) {
    // something with param
}
```
[@CsvSource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-CsvSource) :

```java
@ParameterizedTest(name = "test for param {0} of value {1}")
@CsvSource(value = # "param1;value1", "param2,value2" }, delimiter=";")
void test_something(String arg1, String arg2) {
    // something with param
}
```

[@CsvFileSource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-CsvFileSource) :

```java
@ParameterizedTest
@CsvFileSource(resources = "/data.csv", numLinesToSkip = 1)
void test_something(String col1, int col2) {
    // something with col1 & col2
}
```

[@MethodSource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-MethodSource) :

```java
@ParameterizedTest
@MethodSource("myBeanSupplier")
void test_something(MyBean myBean) {
    // something with myBean
}

static Stream<MyBean> myBeanSupplier() {
    return Stream.of(
     // TODO
    );
}
```

```java
@ParameterizedTest
@MethodSource("myArgsSupplier")
void test_something(Arg1 arg1, Arg2 arg2) {
    // something with arg1 & arg2
}

static Stream<Arguments> myArgsSupplier() {
    return Stream.of(
      Arguments.arguments(new Arg1(), new Arg2())
    );
}
```

[@EnumSource](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-EnumSource) :

```java
@ParameterizedTest
@EnumSource(MyEnum.class)
void test_something(MyEnum myEnum) {
    // something with myEnum
}
```

### Nested Tests

[@Nested](https://junit.org/junit5/docs/current/user-guide/#writing-tests-nested) :

```java
class SomeTests {
    // some tests
    
    @Nested
    class SomeOtherTests {
      // some other tests
    }
}
