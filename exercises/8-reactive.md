# Going Reactive

In this bonus exercise, you will rebuild the movie ticket service with Spring Boot 2 and Spring Framework 5.0. Spring Framework 5.0 introduced Spring WebFlux a new reactive web framework. Unlike Spring MVC, it does not require the Servlet API, is fully asynchronous and non-blocking. This has the advantage that the movie ticket service can handle more requests per seconds.

You can find documentation about the Spring WebFlux Framework [here](https://docs.spring.io/spring-boot/docs/2.0.0.RC1/reference/htmlsingle/#boot-features-webflux).

An example solution can be found in this [repository](https://github.com/mat1/movie-ticket-service-reactive).

The movie ticket service should provide the same REST API as before but the implementation should be completely asynchronous.
