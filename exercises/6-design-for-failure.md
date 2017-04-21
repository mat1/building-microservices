# Design For Failure

In this exercise, you learn how to use Hystrix to make your application more resilient. Hystrix provides many configuration options. You can find details and explanations about these options [here](https://github.com/Netflix/Hystrix/wiki/Configuration).

### Load Test

To check that your Hystrix configuration works correctly you should use this [LoadTest](https://github.com/mat1/movie-ticket-service/blob/master/src/test/java/com/zuehlke/movie/MovieControllerLoadIT.java). Copy the test to your test folder and remove the @Ignore during this exercise.

### Timeouts

The **MovieControllerLoadIT** test fails sometimes because many calls are aborted because they reach the timeout configured in Hystrix. Your task is to increase the default timeout to 5 Seconds.

### Fallback

The `GET /api/v1/movies/1` call fails if the rating service is not available. Implement a fallback function that if the rating service is not available an empty rating list is returned. You should use the fallback functionality from Feign for this [see](https://github.com/OpenFeign/feign/tree/master/hystrix).

If you have implemented the fallback correctly, the load test should pass.

### Circuit Breaker



### Bonus: Hystrix Dashboard
