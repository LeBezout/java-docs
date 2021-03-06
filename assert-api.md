# Assertion or Validation Java APIs

:pushpin: Overview of some APIs we can use for assertions.

## Production code

| API | Class | Example | Exception thrown |
|-----|-------|---------|------------------|
| JDK | - | `assert input != null;` | `java.lang.AssertionError` |
| [JDK](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Objects.html) | `java.util.Objects` | `Object value = Objects.requireNonNull(input);` | `java.lang.NullPointerException` |
| [Spring](https://spring.io/) | `org.springframework.util.Assert` | `Assert.notNull(input);` | `java.lang.IllegalArgumentException` |
| [Apache commons-lang3](https://commons.apache.org/proper/commons-lang/) | `org.apache.commons.lang3.Validate` | `Object value = Validate.notNull(input);` | `java.lang.NullPointerException` |
| [Google Guava](https://github.com/google/guava) | `com.google.common.base.Verify` | `Verify.verifyNotNull(input);` | `com.google.common.base.VerifyException` |

## Test code

| API | Class | Example | Exception thrown |
|-----|-------|---------|------------------|
| [JUnit 4](https://junit.org/junit4/) | `junit.framework.Assert` | `Assert.assertNotNull(input);` | `junit.framework.AssertionFailedError` |
| [JUnit 5](https://junit.org/junit5/) | `org.junit.jupiter.api.Assertions` | `Assertions.assertNotNull(input);` | `org.opentest4j.AssertionFailedError` |
| [Hamcrest](http://hamcrest.org/) | `org.hamcrest.MatcherAssert` | `MatcherAssert.asserthat(X, Y);` | `java.lang.AssertionError` |
| [AssertJ](https://assertj.github.io/doc/) | `org.assertj.core.api.Assertions` |  `Assertions.asserthat(X, Y);` | `java.lang.AssertionError` |
| [TestNG](https://testng.org/doc/) | `org.testng.Assert` | `Assert.assertNotNull(input);` | `java.lang.AssertionError` |
