# Assertions or Validation APIs

:pushpin: Overview of some API we can use for assertions.

## Production code

| API | Class | Example | Exception thrown |
|-----|-------|---------|------------------|
| JDK | `java.util.Objects` | `Object value = Objects.requireNonNull(input);` | `NullPointerException` |
| Spring | `org.springframework.util.Assert` | `Assert.notNull(input);` | `IllegalArgumentException` |
| Apache commons-lang3 | `org.apache.commons.lang3.Validate` | `Object value = Validate.notNull(input);` | `NullPointerException` |
| Google Guava | `com.google.common.base.Verify` | `Verify.verifyNotNull(input);` | `com.google.common.base.VerifyException` |

## Test code

| API | Class | Example | Exception thrown |
|-----|-------|---------|------------------|
| JUnit 4 | `junit.framework.Assert` | `Assert.assertNotNull(input);` | `junit.framework.AssertionFailedError` |
| JUnit 5 | `org.junit.jupiter.api.Assertions` | `Assertions.assertNotNull(input);` | `org.opentest4j.AssertionFailedError` |
| hamcr | `MatcherAssert` | `MatcherAssert.asserthat()` | `AssertionError` \
| AssertJ | TODO | TODO | TODO |
