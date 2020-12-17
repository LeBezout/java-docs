# Java Logging Frameworks Overview

## Main frameworks

* JDK Logging (JUL : java.util.logging)
* Log4J 1.X
* Log4J 2.X
* Apache Commons-logging (JCL)
* SLF4J

:information_source: [Logback](https://logback.qos.ch/) is the reference implementation for [SLF4J](https://www.slf4j.org/)

:information_source: Spring Framework historically use [commons-loggins](https://commons.apache.org/logging)

## Loggers

### Implementation classes

| Framework | Class name |
|-----------|------------|
| **JDK Logging** | `java.util.logging.Logger` |
| **Log4J 1** | `org.apache.log4j.Logger` |
| **Log4J 2** | `org.apache.logging.log4j.Logger` |
| **Commons-Logging** | `org.apache.commons.logging.Log` |
| **SLF4J** | `org.slf4j.Logger` | `org.slf4j.Logger` |
| **Logback** | `ch.qos.logback.classic.Logger` |

:information_source: Note the Commons-Logging singularity

### Obtain a Logger instance

| Framework | Package | From name | From class |
|-----------|---------|-----------|------------|
| **JDK Logging** | `java.util.logging` | `Logger.getLogger("name")` | :no_entry_sign: |
| **Log4J 1** | `org.apache.log4j` | `Logger.getLogger("name")` |  `Logger.getLogger(clazz)` |
| **Log4J 2** | `org.apache.logging.log4j` | `LogManager.getLogger("name")` | `LogManager.getLogger(clazz)` |
| **Commons-Logging** | `org.apache.commons.logging` | `LogFactory.getLog("name")` | `LogFactory.getLog(clazz)` |
| **SLF4J** | `org.slf4j` | `LoggerFactory.getLogger("name")` | `LoggerFactory.getLogger(clazz)` |

## Trace Methods

| JDK Logging | Log4J 1 | Log4J 2 | Commons-Logging | SLF4J |
|-------------|---------|---------|-----------------|-------|
| finest() | trace() | trace() | trace() | trace() |
| finer() | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: |
| fine() | debug() | debug() | debug() | debug() |
| config() | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: |
| info() | info() | info() | info() | info() |
| warning() | warn() | warn() | warn() | warn() |
| :no_entry_sign: | error() | error() |  error() | error() |
| severe() | fatal() | fatal() | fatal() | :no_entry_sign: |
| log() | log() | log() | :no_entry_sign: | :no_entry_sign: |

:information_source: Logback/SLF4J does not have a `FATAL` level

## Levels

### Implementation classes

| Framework | Class name |
|-----------|------------|
| **JDK Logging** | `java.util.logging.Level` |
| **Log4J 1** | `org.apache.log4j.Level` |
| **Log4J 2** | `org.apache.logging.log4j.Level` |
| **Commons-Logging** | :no_entry_sign: |
| **SLF4J** | `org.slf4j.event.Level` |
| **Logback** | `ch.qos.logback.classic.Level` |

### Effectives levels

| JDK Logging | Log4J 1 | Log4J 2 | Commons-Logging | SLF4J |
|-------------|---------|---------|-----------------|-------|
| ALL | ALL | ALL | :no_entry_sign: | :no_entry_sign: |
| FINEST | TRACE | TRACE | _TRACE_ | TRACE |
| FINER | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: |
| FINE | DEBUG | DEBUG | _DEBUG_ | DEBUG |
| CONFIG | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: | :no_entry_sign: |
| INFO | INFO | INFO | _INFO_ | INFO |
| WARNING | WARN | WARN | _WARN_ | WARN |
| :no_entry_sign: | ERROR | ERROR | _ERROR_ | ERROR |
| SEVERE | FATAL | FATAL | _FATAL_| :no_entry_sign: |
| OFF | OFF | OFF | :no_entry_sign: | :no_entry_sign: |

## IsEnabled Methods

| JDK Logging | Log4J 1 | Log4J 2 | Commons-Logging | SLF4J |
|-------------|---------|---------|-----------------|-------|
| isLoggable(Level) | isEnabledFor(Priority) | isEnabled(Level) | :no_entry_sign: | :no_entry_sign: |
| :no_entry_sign: | isTraceEnabled() | isTraceEnabled() | isTraceEnabled() | isTraceEnabled() |
| :no_entry_sign: | isDebugEnabled() | isDebugEnabled() | isDebugEnabled() | isDebugEnabled() |
| :no_entry_sign: | isInfoEnabled() | isInfoEnabled() | isInfoEnabled() | isInfoEnabled() |
| :no_entry_sign: | :no_entry_sign: | isWarnEnabled() | isWarnEnabled() | isWarnEnabled() |
| :no_entry_sign: | :no_entry_sign: | isErrorEnabled() | isErrorEnabled() | isErrorEnabled() |
| :no_entry_sign: | :no_entry_sign: | isFatalEnabled() | isFatalEnabled() | :no_entry_sign: |

## Context

| JDK Logging | Log4J 1 | Log4J 2 | Commons-Logging | SLF4J |
|-------------|---------|---------|-----------------|-------|
| :no_entry_sign: | NDC | [ThreadContext](https://logging.apache.org/log4j/2.x/manual/thread-context.html) | :no_entry_sign: | :no_entry_sign: |
| :no_entry_sign: | MDC | [ThreadContext](https://logging.apache.org/log4j/2.x/manual/thread-context.html) | :no_entry_sign: | [MDC](http://logback.qos.ch/manual/mdc.html) |

## Links

### Official pages

* [SLF4J](https://www.slf4j.org/)
* [Logback - Configuration](https://logback.qos.ch/manual/configuration.html)
* [Log4J 1.2](https://logging.apache.org/log4j/1.2/)
* [Log4J 2 - Manual](https://logging.apache.org/log4j/2.x/manual/)
* [Apache Commons - commons-loggins](https://commons.apache.org/proper/commons-logging/)
* [Java Logging Overview](https://docs.oracle.com/javase/8/docs/technotes/guides/logging/overview.html)

### Tutorials

* [Baeldung - Introduction to Java Logging](http://www.baeldung.com/java-logging-intro)
* [Baeldung - Java Logging with Nested Diagnostic Context (NDC)](http://www.baeldung.com/java-logging-ndc-log4j)
* [Spring - Spring Boot Logging](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html)
