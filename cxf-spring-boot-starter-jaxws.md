# Spring Boot : JAX-WS : How to use `cxf-spring-boot-starter-jaxws`

:bulb: Official Documentation <http://cxf.apache.org/docs/springboot.html#SpringBoot-SpringBootCXFJAX-WSStarter>

## Step 1: add dependency

In `pom.xml` file (I let you deduce equivalence for Gradle) :

```xml
<dependency>
  <groupId>org.apache.cxf</groupId>
  <artifactId>cxf-spring-boot-starter-jaxws</artifactId>
  <version>3.2.4</version>
</dependency>
```

## Step 2: configuration

In `application.properties` file (I let you deduce equivalence for Yaml) :

```properties
cxf.path=/ws
cxf.servlet.load-on-startup=1
cxf.servlet.init.service-list-title=My App
```

:information_source: `cxf.path` defaults to `/services`

## Step 3: implement services

Package `com.mycompany.myapp.soap.endpoint` :

```java
@Component
@javax.jws.WebService(serviceName = "SampleSoapService", portName = "SampleSoapPort", targetNamespace = "http://soap.myapp.mycompany.com/sample/")
public class SampleSoapService {
	private final MyService sampleService;
	public SampleSoapService(MyService sampleService) {
		this.sampleService = sampleService;
	}
  
	@WebResult(name = "version")
	public String wsVersion() {
		return "1.0";
	}
	
	@WebResult(name = "sample")
	public SampleDTO getEntityById(@WebParam(name = "idSample") @XmlElement(required = true) Long id) {
		return sampleService.getSampleEntity(id);
	}
}
```

## Step 4: declare services

I write a single `@Configuration` class to centralize the declarations :

```java
@Configuration
public class WebServicePublisher {
  private static final String LOG_MSG_PATTERN = "Publishing CXF Webservice {}";
  private static final Logger LOGGER = LoggerFactory.getLogger(WebServicePublisher.class);
	
  @Autowired
  private SpringBus springBus;
  // inject here all endpoints
  @Autowired
  private SampleSoapService sampleSoapService;
  @Autowired
  private AnotherSampleSoapService anotherSampleSoapService;

  @Bean
  public Endpoint publishSampleEndpoint() {
    LOGGER.info(LOG_MSG_PATTERN, sampleSoapService);
    EndpointImpl endpoint = new EndpointImpl(springBus, sampleSoapService);
    endpoint.publish("/sample");
    return endpoint;
  }

  @Bean
  public Endpoint publishAnotherSampleEndpoint() {
    LOGGER.info(LOG_MSG_PATTERN, probeSoapService);
    EndpointImpl endpoint = new EndpointImpl(springBus, anotherSampleSoapService);
    endpoint.publish("/other");
    return endpoint;
  }
	
  // ... and more
}
```

## Step 5: add some security

As usual use Spring Security :

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
  @Override
  public void configure(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication().withUser("admin-ws").password("{noop}secret").authorities("G_ADMIN_WS");
    //auth.authenticationProvider(your_custom_auth_provider);
  }
    
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    // 403 - Could not verify the provided CSRF token because your session was not found.
    http.csrf().disable();
    // Secure each service with a single role
    http.authorizeRequests().anyRequest().hasAuthority("G_ADMIN_WS").and().httpBasic();
  }
	
  @Override
  public void configure(WebSecurity web) throws Exception {
    // let acess everyone to the WSDL, the services list and CXF generated stylesheets
    web.ignoring().antMatchers("/ws", "/ws/probe").regexMatchers(".*\\?wsdl").regexMatchers(".*\\?stylesheet=.*");
  }
}
```

## Step 6: add some JUnit tests

TODO
