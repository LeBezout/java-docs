# Java Frameworks Overview

## By specifications

### JPA - Java Persistance API

* :book: [JSR 317: Java Persistence 2.0](https://www.jcp.org/en/jsr/detail?id=317)
* :book: [JSR 338: Java Persistence 2.2](https://jcp.org/en/jsr/detail?id=338)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Red Hat, Inc. | JBoss | [Hibernate](http://hibernate.org/) | |
| The Eclipse Foundation | EclipseLink | [EclipseLink](http://www.eclipse.org/eclipselink/) | Reference Implementation (TopLink derived) |
| Apache | OpenJPA | [OpenJPA](http://openjpa.apache.org/) | |
| Oracle | TopLink | [TopLink](http://www.oracle.com/technetwork/middleware/toplink/overview/index-089172.html) | |

### JAX-WS

* :book: [JSR 224: Java API for XML-Based Web Services (JAX-WS) 2.0](https://jcp.org/en/jsr/detail?id=224)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Apache | CXF | [CXF](http://cxf.apache.org/) | |
| Apache | Axis | [Axis 2](https://axis.apache.org/axis2/java/core/) | |
| Oracle | GlassFish | [Metro](https://javaee.github.io/metro/)| |
| Red Hat, Inc. | JBoss | [JBoss WS](http://jbossws.jboss.org/) | |

### JAX-RS

* :book: [JSR 311: JAX-RS: The Java API for RESTful Web Services](https://jcp.org/en/jsr/detail?id=311)
* :book: [JSR 339: JAX-RS 2.0: The Java API for RESTful Web Services](https://jcp.org/en/jsr/detail?id=339)
* :book: [JSR 370: JAX-RS 2.1: The Java API for RESTful Web Services](https://jcp.org/en/jsr/detail?id=370)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Red Hat, Inc. | JBoss | [RESTEasy](http://resteasy.jboss.org/) | |
| Oracle | GlassFish | [Jersey](https://jersey.github.io/) | Old Reference Implementation |
| The Eclipse Foundation | EE4J | [Jersey](https://projects.eclipse.org/projects/ee4j.jersey) | Current Reference Implementation |
| Apache | CXF | [CXF](http://cxf.apache.org/) | |
| Pivotal | Spring | [Spring MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html) | |

### JTA - Java Transaction API

* :book: [JSR 907: Java Transaction API (JTA)](https://jcp.org/en/jsr/detail?id=907)

| Editor | Project | Name | Description |
|---------|--------|-----|--------------|
| Atomikos BVBA | Atomikos | [Atomikos](https://www.atomikos.com/) | |
| - | Bitronix | [BTM](https://github.com/bitronix/btm) | |
| Red Hat, Inc. | JBoss | [Narayana](http://narayana.io/) | |

### JCache - Java Cache API

* :book: [JSR 107: JCACHE - Java Temporary Caching API](https://jcp.org/en/jsr/detail?id=107)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Terracotta, Inc. | Ehcache | [Ehcache](http://www.ehcache.org/) | Non distributed |
| Apache | Commons | [commons-jcs](https://commons.apache.org/proper/commons-jcs/) | Distributed caching system  |
| Hazelcast, Inc.  | Hazelcast | [Hazelcast](https://hazelcast.com/) | Distributed caching system  |
| Red Hat, Inc. | Infinispan | [Infinispan](http://infinispan.org/) | Distributed in-memory caching system  |
| Oracle | Coherence | [Coherence JCache](https://coherence.community/) | Local Cache, Partitioned Cache, Pass-Through Cache, Remote Cache |

:bulb: <https://labs.consol.de/java-caches/>

### Bean Validation

* :book: [JSR 303: Bean Validation 1.0](https://jcp.org/en/jsr/detail?id=303)
* :book: [JSR 303: Bean Validation 1.1](https://jcp.org/en/jsr/detail?id=349)
* :book: [JSR 380: Bean Validation 2.0](https://jcp.org/en/jsr/detail?id=380)
* :book: [Jakarta Bean Validation](https://beanvalidation.org/2.0-jsr380/)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Red Hat, Inc. | JBoss | [Hibernate Validator](http://hibernate.org/validator/) | Reference Implementation |
| Apache | Tapestry | [Tapestry Bean Validation](https://tapestry.apache.org/bean-validation.html) | |

### Dependency Injection

* :book: [JSR 299: Contexts and Dependency Injection for the Java EE platform](https://jcp.org/en/jsr/detail?id=299)
* :book: [JSR 330: Dependency Injection for Java](https://jcp.org/en/jsr/detail?id=330)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Pivotal | Spring Framework | [Spring Core](https://projects.spring.io/spring-framework/) | |
| Apache | DeltaSpike | [DeltaSpike](http://deltaspike.apache.org/) | CDI Implementation |
| Red Hat, Inc. | JBoss | [Weld](http://weld.cdi-spec.org/) | CDI Reference Implementation |
| Oracle | GlassFish | [HK2](https://javaee.github.io/hk2/) | Implementation of JSR-330 |
| Google | | [Guice](https://github.com/google/guice) | |

### Security

* :book: [JSR 375: Java EE Security API](https://jcp.org/en/jsr/detail?id=375)

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| The Eclipse Foundation | EE4J | [Soteria](https://github.com/eclipse-ee4j/soteriay) | |
| Pivotal | Spring Framework | [Spring Security](https://spring.io/projects/spring-security) | |

## By domain

### Logging

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Oracle | Java | [JUL - java.util.logging](https://docs.oracle.com/javase/10/docs/api/java/util/logging/package-summary.html) | JDK Loggign implementation since Java 1.4|
| Apache | Log4J | [Log4J 1](https://logging.apache.org/log4j/1.2/) | Retired in 2015 |
| Apache | Log4J | [Log4J 2](https://logging.apache.org/log4j/2.x/manual/) | |
| Apache | Commons | [Commons-Logging](https://commons.apache.org/logging) | |
| QOS.ch Sàrl. | Logback | [Logback](https://logback.qos.ch/) | natively implements the SLF4J API |
| QOS.ch Sàrl. | SLF4J | [SLF4J](https://www.slf4j.org/) | Simple Logging Facade for Java |

### Unit testing

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| - | JUnit | [JUnit](https://junit.org/) | |
| - | DbUnit | [DbUnit](http://dbunit.sourceforge.net/) | |
| - | HttpUnit | [HttpUnit](http://httpunit.sourceforge.net/) | |
| - | XMLUnit | [XMLUnit](https://www.xmlunit.org/) | |
| - | Mockito | [Mockito](http://site.mockito.org/) | |
| - | EasyMock | [EasyMock](http://easymock.org/) | |
| - | TestNG | [TestNG](http://testng.org/doc/) | |
| Red Hat, Inc. | JBoss | [Arquillian](http://arquillian.org/) | |
| - | jMock | [jMock](http://jmock.org/) | |
| - | JMockit | [JMockit](http://jmockit.github.io/gettingStarted.html) | |
| - | PowerMock | [PowerMock](http://powermock.github.io/) | |
| Joel Costigliola | AssertJ | [AssertJ](http://joel-costigliola.github.io/assertj/) | |
| - | FEST-Assert | [FEST-Assert](https://github.com/alexruiz/fest-assert-2.x/wiki/One-minute-starting-guide) | Deprecated, replaced by AspectJ |

### JSON Mapping

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| Google | google-gson | [Gson](https://github.com/google/gson) | |
| FasterXML, LLC | Jackson | [Jackson](https://github.com/FasterXML/jackson) | |

### Templating

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| - | Mustache | [{{mustache}}](https://github.com/spullara/mustache.java) | |
| Apache | FreeMarker | [FreeMarker](https://freemarker.apache.org/) | |
| Apache | Velocity | [Velocity](http://velocity.apache.org/) | |
| The Thymeleaf Team | Thymeleaf | [Thymeleaf](https://www.thymeleaf.org/) | |

## REST Client and HTTP Client

| Editor | Project | Name | Description |
|--------|---------|------|-------------|
| - | OpenFeign | [OpenFeign](https://github.com/OpenFeign/feign) | Client Java HTTP |
| Pivotal | Spring Framework | [RestTemplate](https://spring.io/guides/gs/consuming-rest/) | |
| Pivotal | Spring Framework |[FeignClient](https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-feign.html) | |
| Oracle | Glassfish | [Jersey client](https://jersey.java.net/documentation/latest/client.html) | |
| Square | OkHttp | [OkHttp](http://square.github.io/okhttp/) | |
| Square | Retrofit | [Retrofit](http://square.github.io/retrofit/) | |
| Mashape | Unirest | [Unirest](http://unirest.io/java.html) | |
| Restlet, Inc. | Restlet | [Restlet](https://restlet.com/) | |
| Apache | Commons | [HttpComponents](http://hc.apache.org/) | |
| Apache | CXF | [CXF Client](http://cxf.apache.org/docs/jax-rs-client-api.html) | |
| Google | Google APIs | [HTTP Client Library for Java](https://developers.google.com/api-client-library/java/google-http-java-client/) | |
| teamed.io | jcabi | [jcabi-http](https://http.jcabi.com/) | Fluent & lightweight Java HTTP Client |
| Netty project | Netty | [Netty](https://netty.io/) | framework non-blocking I/O client-serveur pour le développement d'applications réseau Java |
| - | rest-assured - [rest-assured](https://github.com/rest-assured/rest-assured) | Test JUnit d'API REST |
| - | rapa | [rapa](https://github.com/harikrishnan83/rapa/wiki) | REST Client for Java |
| CAELUM OBJECTS | Restfulie | [Restfulie](http://restfulie.caelum.com.br/) | |
| - | Resty | [Resty](https://beders.github.io/Resty/Resty/Overview.html) | A simple HTTP REST client for Java |
| - | - | [http-rest-client](https://github.com/g00dnatur3/http-rest-client) | A simple & easy to use REST client written in Java and levarging the HttpClient 4.3 library. |
