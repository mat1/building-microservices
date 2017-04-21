# Are you there?

In this exercise, you learn how to monitor your Spring Boot App and how to know if something is wrong.

### Spring Boot Actuator

Spring Boot Actuator provides many features to monitor and manage your REST service. Add Actuator to your pom.xml and start your Spring Boot App. You should now see many new REST endpoints in the console for example http://localhost:8080/health.
You can find a detailed description to all actuator endpoints [here](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#production-ready-endpoints)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

To get access to all Actuator endpoints you can set temporary `management.security.enabled=false` in the application.properties.
Play around a little bit and see which information Spring Boot Actuator provides.

### Logging

It is often helpful to see all incoming requests and outgoing responses and all calls to external services.
Your first task is to to configure Spring Boot so that every HTTP requests and response is logged. 
The second task is to configure Feign to log all REST calls.

### Health Checks

Spring Boot Actuator provides an `GET /health` endpoint which returns the health information about a service. It is possible to add your own health indicators to Spring Actuator. 
Your task is to add an health check which calls `https://movie-service.herokuapp.com/health` to see if the `Movie Service` is available.
You can find more infos about HealthIndicators [here](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#production-ready-health).