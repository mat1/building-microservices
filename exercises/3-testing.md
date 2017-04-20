# Testing Microservices

In this exercise, you will write some component tests with REST Assured.

## First Step

Your task is to write some component tests for the MovieController. You should test the two operations `GET /api/v1/movies` and `GET /api/v1/movies/{id}`.

REST Assured is a library which helps you to test REST services with Java. You can find more deatils about REST Assured [here](http://rest-assured.io/).

### Add REST Assured

First we need to add REST Assured to our pom.xml.

```xml
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>3.0.2</version>
    <scope>test</scope>
</dependency>
```

### Write Tests

Write two tests for the two operations `GET /api/v1/movies` and `GET /api/v1/movies/{id}` with REST Assured.
Make sure you check the JSON responses in your tests. You can use the example below as starting point.

```java
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class MovieControllerComponentTest {

    @LocalServerPort
    private int port;

    @Before
    public void setUp() throws Exception {
        RestAssured.port = port;
    }

    @Test
    public void getMovies() throws Exception {

    }

    @Test
    public void getMovieById() throws Exception {

    }

}
```