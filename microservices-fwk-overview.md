# Microservices Frameworks Overview

:pushpin: A comparison between **Spring Boot**, **Micronaut**, **Quarkus** & **Helidon**

:construction: :warning: :construction_worker:

## Global Overview

|  | Spring Boot | Micronaut | Quarkus | Helidon |
|--|-------------|-----------|---------|---------|
| Description | Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". | A modern, JVM-based, full-stack framework for building modular, easily testable microservice and serverless applications. | Supersonic Subatomic Java. A Kubernetes Native Java stack tailored for OpenJDK HotSpot and GraalVM, crafted from the best of breed Java libraries and standards. | Helidon is a collection of Java libraries for writing microservices that run on a fast web core powered by Netty. |
| Home page | <https://spring.io/projects/spring-boot> | <https://micronaut.io/> | <https://quarkus.io/> | <https://helidon.io/> |
| Sponsor | [VM Ware](https://www.vmware.com/) | [Object Computing](https://objectcomputing.com/) | [Red Hat](https://www.redhat.com/) | [Oracle](https://www.oracle.com/) |
| Starter page | [Spring Initializr](https://start.spring.io/) | [Micronaut Launch](https://micronaut.io/launch/) | [Quarkus Start Coding](https://code.quarkus.io/) | none : archetype:generate |
| Run the app | `mvn spring-boot:run -Dspring-boot.run.profiles=foo,bar` | `java -jar target/myapp.jar` | `mvn compile quarkus:dev` | `java -jar target/myapp.jar` |

## Health Checks URL

* Spring-Boot :
  * `(/actuator)/health`
  * `(/actuator)/health/liveness`
  * `(/actuator)/health/readiness`
* Micronaut :
  * `/health`
  * `/health/liveness`
  * `/health/readiness`
* Quarkus /  Helidon (Microprofile) :
  * `/health`
  * `/health/live`
  * `/health/ready`

## Reactive implementations

### Spring Boot

Use : Tomcat, jetty,  Undertow, netty

[**Reactor**](https://projectreactor.io/) is a fourth-generation reactive library, based on the Reactive Streams

* `reactor.core.publisher.Mono`
* `reactor.core.publisher.Flux`

### Micronaut

Use : netty

[**ReactiveX**](http://reactivex.io/) - An API for asynchronous programming with observable streams

* `io.reactivex.Single`
* `io.reactivex.Maybe`
* `io.reactivex.Flowable`

### Quarkus

Use : vert.x

[**SmallRye Mutiny**](https://smallrye.io/smallrye-mutiny/) - Intuitive Event-Driven Reactive Programming Library for Java

* `io.smallrye.mutiny.Uni` - for asynchronous action providing 0 or 1 result
* `io.smallrye.mutiny.Multi` - for multi-item (with back-pressure) streams

### Helidon

Use : netty

* `io.helidon.common.reactive.Single`
* `io.helidon.common.reactive.Multi`
