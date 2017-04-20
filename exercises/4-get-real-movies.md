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

Your task is to get the movies from the movie-service and the ratings from the movie-ratings-service.

Below you find the API doucmentation for both services:

| Movie Service         | https://movie-service.herokuapp.com/swagger-ui.html         |
| Movie Rating Service  | https://movie-rating-service.herokuapp.com/swagger-ui.html  |

You can play around with swagger to get an better understanding for these REST services.

### Get Some Real Movies

Now it is time to get some real movies instead of the hard coded once in the **MovieController**. 
The **MoiveController** should now make a REST call `GET https://movie-service.herokuapp.com/api/v1/movies` to get the movies from the **Movie Service**.

First you should create a class **MoviesAdapter** which act as an adapter between the **Movie Service** and the **Movice Ticket Service**. This class should call the external REST service.

Below you find an Integration Test **MoviesAdapterIT** and an empty **MoviesAdapter** skeleton which you can use as a starting point.

```java
// IntegrationTest
public class MoviesAdapterIT {
    @Test
    public void getAll() throws Exception {
        MoviesAdapter moviesAdapter = new MoviesAdapter("https://movie-service.herokuapp.com/");

        List<Movie> movies = moviesAdapter.getAll();

        assertThat(movies, hasSize(7));
        assertThat(movies, hasItem(new Movie(1, "Batman Begins", "https://images-na.ssl-images-amazon.com/images/M/MV5BNTM3OTc0MzM2OV5BMl5BanBnXkFtZTYwNzUwMTI3._V1_SX300.jpg")));
    }
}
```

```java
// Skeleton
public class MoviesAdapter {

    public MoviesAdapter(String url) {

    }

    public List<Movie> getAll() {
        return Collections.emptyList();
    }
}
```


