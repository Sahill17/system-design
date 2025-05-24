#### Single Responsibility Principle (SRP)

A class should have only one reason to change or have only one job or purpose within the system.

```java
class Movie {
    String name;
    float rating;
    float boxOffice;

    public Movie(String name, float rating, float boxOffice) {
        this.name = name;
        this.rating = rating;
        this.boxOffice = boxOffice;
    }

    public void updateRating(float newRating) {
        // Logic here
    }

    public void addRevenue(float amount) {
        // Logic here
    }
}
```

Above `Movie` class does not follow the Single Responsibility Principle because it handles more than one task. It stores the movie's basic information like the name, but it also manages changing ratings and tracks box office revenue. Ratings can change over time as more people vote, and box office earnings go up as the movie stays in theaters. These are different responsibilities that may change for different reasons, so putting them all in one class makes the code harder to maintain.

```java
class MovieInfo {
    String name;

    public MovieInfo(String name) {
        this.name = name;
    }
}

class Rating {
    float rating;

    public Rating(float rating) {
        this.rating = rating;
    }

    public void update(float newRating) {
        // Logic here
    }
}

class BoxOffice {
    float revenue;

    public BoxOffice(float revenue) {
        this.revenue = revenue;
    }

    public void addRevenue(float amount) {
        // Logic here
    }
}
```

To follow the Single Responsibility Principle, we can split the class into three smaller ones. One class, `MovieInfo`, just stores the name. Another class, `Rating`, handles rating updates. A third class, `BoxOffice`, tracks the revenue. Now, each class has only one job, so if the rating logic changes, we only update the `Rating` class. This keeps the code cleaner and easier to manage.