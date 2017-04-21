# Configuration

In this exercise, you learn how to configure your Spring Boot App. You can find more details about how the Spring Boot Configuration mechanism works [here](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html).

### Externalized Configuration

Your task is to make the two endpoint URLs configurable. The URLs should be configured in the `application.properties` file similar to 
the example below:

```
# External Endpoints
endpoint.movie-service=https://movie-service.herokuapp.com/
endpoint.movie-rating-service=https://movie-rating-service.herokuapp.com/
```

### Bonus: Configure Logging Level

Configure the logging level so that you can see the Feign HTTP requests in the console.