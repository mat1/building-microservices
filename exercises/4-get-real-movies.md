# Configuation and Get Real Movies

In this exercise, you will learn how to configure your spring boot application and how to integrate other REST services
with Feign. You can find more details about Feign [here](https://github.com/OpenFeign/feign).

### Add Feign

Add Feign to your pom.xml.

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>Dalston.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-feign</artifactId>
    </dependency>
    <dependency>
        <groupId>com.netflix.feign</groupId>
        <artifactId>feign-jackson</artifactId>
        <version>8.18.0</version>
    </dependency>
</dependencies>
```

## Service Integration

Your task is to get the movies from the **Movie Service** and the ratings from the **Movie Rating Service**.

Below you find the API doucmentation for both services:

| Service               | Url           |
| --------------------- | ------------- | 
| Movie Service         | https://movie-service.herokuapp.com/swagger-ui.html         |
| Movie Rating Service  | https://movie-rating-service.herokuapp.com/swagger-ui.html  |

You can play around with swagger to get an better understanding for these REST services.

### Get Some Real Movies

Now it is time to get some real movies instead of the hard coded once in the *MovieController*. 
The *MoiveController* should now make a REST call `GET https://movie-service.herokuapp.com/api/v1/movies` to fetch the movies from the *Movie Service*.

First you should create a class **MovieSerciceAdapter** which act as an adapter between the *Movie Service* and the *Movice Ticket Service*. This class should use Feign to call the external REST service.

Below you find an Integration Test **MoviesAdapterIT** and an empty **MovieServiceAdapter** skeleton which you can use as a starting point.

```java
// IntegrationTest
public class MovieServiceAdapterIT {
    
    // Hystrix will be explained later in the course
    static {
        System.setProperty("hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds", "5000");
    }

    @Test
    public void getAll() throws Exception {
        MovieServiceAdapter movieServiceAdapter = new MovieServiceAdapter("https://movie-service.herokuapp.com/");

        List<Movie> movies = movieServiceAdapter.getAll();

        assertThat(movies, hasSize(7));
        assertThat(movies, hasItem(new Movie(1, "Batman Begins", "https://images-na.ssl-images-amazon.com/images/M/MV5BNTM3OTc0MzM2OV5BMl5BanBnXkFtZTYwNzUwMTI3._V1_SX300.jpg")));
    }
}
```

```java
// Skeleton
public class MovieServiceAdapter {

    public MovieServiceAdapter(String url) {

    }

    public List<Movie> getAll() {
        return null;
    }
}
```

As soon as the Integration Test is green you can inject the *MovieServiceAdapter* into the *MovieController*. If you start your Spring Boot App now `GET /api/v1/movies` should return at least 7 movies.

#### Feign Problems?

Do you have problems making rest calls with feign? Below you find an factory and an example which makes it a little bit easier to create an Feign client.

```java
// Feign RestClientFactory
public class RestClientFactory {
    public static <T> T createClient(String url, Class<T> clazz) {
        ObjectMapper mapper = new ObjectMapper()
                .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false)
                .configure(MapperFeature.ACCEPT_CASE_INSENSITIVE_PROPERTIES, true);

        return HystrixFeign.builder()
                .decoder(new JacksonDecoder(mapper))
                .logger(new Slf4jLogger(RestClientFactory.class))
                .logLevel(Logger.Level.FULL)
                .target(clazz, url);
    }
}

// How to use the Factory
public class MovieServiceAdapter {

    private final MovieServiceApiClient moviesApiClient;

    public MovieServiceAdapter(String url) {
        moviesApiClient = RestClientFactory.createClient(url, MovieServiceApiClient.class);
    }

    // ...
}
```

### Get the Details

Add the method `getMovieById(long id)` on the **MovieServiceAdapter** which should call `GET /api/v1/movies/{id}` on the *Movie Service*.

```java

public Optional<Movie> getMovieById(long id) {
    return null;
}

```

### Get the Ratings

Pretty similar to the previous task. Now you should get the movie ratings from the *Movie Rating Service*.
Create an *RatingAdapter* simliar to the *MovieAdapter* in the first task. You find an Integration Test and a Sekelton for the *RatingAdapter* below:

```java
// IntegrationTest
public class RatingAdapterIT {

    static {
        System.setProperty("hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds", "5000");
    }

    @Test
    public void getRatingsById() throws Exception {
        RatingAdapter ratingAdapter = new RatingAdapter("https://movie-rating-service.herokuapp.com");

        List<Rating> ratings = ratingAdapter.getRatingsById(1);

        assertThat(ratings, hasSize(3));
    }

}
```

```java
// Skeleton
public class RatingAdapter {

    public RatingAdapter(String url) {
        
    }

    public List<Rating> getRatingsById(long id) {
        return null;
    }
}
```

### Combine the Details and the Ratings

As soon as the Integration Test is green you can inject the *RatingAdapter* into the *MovieController*. 
Now you can call the *MovieServiceAdapter* first to get the details about a movie and afterwards the *RatingAdapter* to get the ratings.
Your **MovieController* should now look simliar to the code below:

```java
@RequestMapping("/api/v1/")
@Controller
public class MovieController {

    private final MovieServiceAdapter movieServiceAdapter = new MovieServiceAdapter("https://movie-service.herokuapp.com/");
    private final RatingAdapter ratingAdapter = new RatingAdapter("https://movie-rating-service.herokuapp.com/");

    @GetMapping("/movies")
    @ResponseBody
    public List<Movie> getMovies() {
        return movieServiceAdapter.getAll();
    }

    @GetMapping("/movies/{id}")
    @ResponseBody
    public MovieDetail getMovieById(@PathVariable("id") long id) {
        return new MovieDetail(1,
                "Batman Begins",
                "https://images-na.ssl-images-amazon.com/images/M/MV5BNTM3OTc0MzM2OV5BMl5BanBnXkFtZTYwNzUwMTI3._V1_SX300.jpg",
                "After training with his mentor, Batman begins his fight to free crime-ridden Gotham City from the corruption that Scarecrow and the League of Shadows have cast upon it.",
                2005,
                "Action",
                asList(new Rating("Internet Movie Database", "8.3/10"), new Rating("Rotten Tomatoes", "84%")));
    }
}
```

If you start your Spring Boot App now `GET /api/v1/movies/1` should return the movie *Batman* with 3 ratings.

