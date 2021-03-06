# JUnit 4 - Tips & Tricks

## How to specify a "Runner"

With the `@RunWith(MyRunner.class)` annotation on the test class:

Common Runners :

* Spring : `@RunWith(SpringJUnit4ClassRunner.class)`
* Spring-Boot : `@RunWith(SpringRunner.class)` [Spring Boot features - Testing](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-testing.html)
* Mockito : `@RunWith(MockitoJUnitRunner.class)` <http://site.mockito.org/>
* JMockit : `@RunWith(JMockit.class)` <http://jmockit.github.io/>
* PowerMock : `@RunWith(PowerMockRunner.class)` <http://powermock.github.io/>

## How to sort methods

With the `@FixMethodOrder` annotation on the test class:

```java
@RunWith(MonRunnerHabituel.class)
@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class SomeTest {
  @Test
  public void test_1_first() {
    System.out.println("first executed test");
  }
  @Test
  public void test_2_second() {
    System.out.println("second executed test");
  }
  @Test
  public void test_3_third() {
    System.out.println("third executed test");
  }
}
```

:warning: Alphabetic order (`NAME_ASCENDING`)

## How to specify a timeout

For example, for a test that performs a remote service call (to be avoided) or a local HTTP server mock, it is advisable to set a delay.
So that JUnit can stop the test if it lasts too long.

Simply with `@Test` :

```java
  @Test(timeout = 10_000)
  public void should_test() {
    callHttpService();
  }
```

:information_source: Timeout in milliseconds.

> :warning: JUnit JavaDoc : Test methods with a timeout parameter are run in a thread other than the thread which runs the fixture's @Before and @After methods.

## Deal with exceptions

### First way (poor)

Simply with `@Test` :

```java
  @Test(expected = TechnicalException.class)
  public void should_test() {
    callService();
  }
```

### Second way (better)

With `@Rule` :

On the test class:

```java
  @Rule
  public final ExpectedException expectedEx = ExpectedException.none();
```

In the test method:

```java
  @Test
  public void should_test() {
    expectedEx.expect(TechnicalException.class);
    expectedEx.expectMessage("my expected message");

    callService();
  }
```

Validate an exception cause:

```java
  @Test
  public void should_test() {
    expectedEx.expectCause(IsInstanceOf.instanceOf(IllegalArgumentException.class));
    expectedEx.expectMessage("my expected message");

    callService();
  }
```

## How to ignore tests

### First way (very poor)

Simply with `@Ignore` :

```java
  @Test
  @Ignore
  public void should_test() {
    callService();
  }
```

### Second way (poor)

With the Maven Surefire plugin:

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <configuration>
    <excludes>
      <exclude>**/IgnoredTest1*</exclude>
      <exclude>**/IgnoredTest2*</exclude>
    </excludes>
  </configuration>
</plugin>
```

### Third way (better)

With `@Category`annotation.

**First step** Define an annotation like this one:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyLocalTest {

}
```

**Second step** Configure the Maven Surefire plugin:

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <configuration>
    <groups></groups>
    <excludedGroups>com.myorg.category.MyLocalTest</excludedGroups>
  </configuration>
</plugin>
```

**Third step** Add the `@Category` annotation with your own annotation on the categorized tests:

```java
  @Test
  @Category(MyLocalTest.class)
  public void should_be_ignored_by_maven() {
    callService();
  }
```
