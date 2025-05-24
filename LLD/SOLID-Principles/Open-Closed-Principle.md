#### Open/Closed Principle

Entities ( class, functions, modules, etc.. ) should be open for extension but closed for modifications.

```java
// Every new filter requires changing this class

import java.util.List;

class MovieService {
    public List<Movie> filterByRating(List<Movie> movies, float minRating) {
        // Logic
    }

    public List<Movie> filterByRevenue(List<Movie> movies, float minRevenue) {
        // Logic
    }
    // To add filterByDirector(), you’d have to modify MovieService again
}
```

When your `MovieService` class has separate methods for each criterion—like `filterByRating` and `filterByRevenue`—you must keep editing it whenever you need a new filter (by director, by year, etc.). That means it isn’t closed for modification.

```java
// MovieService stays the same, filters grow independently

interface MovieFilter {
    boolean matches(Movie m);
}

class RatingFilter implements MovieFilter {
    private final float threshold;
    RatingFilter(float threshold) { this.threshold = threshold; }
    public boolean matches(Movie m) {
        // rating comparison logic here
    }
}

class RevenueFilter implements MovieFilter {
    private final float minRevenue;
    RevenueFilter(float minRevenue) { this.minRevenue = minRevenue; }
    public boolean matches(Movie m) {
        // revenue comparison logic here
    }
}

class MovieService {
    public List<Movie> filter(List<Movie> movies, MovieFilter filter) {
        // generic filtering logic here
    }
}
```

Instead, give `MovieService` a single `filter` method and define each criterion in its own class. Now you can add new filters without touching `MovieService`, keeping it closed to change but open to extension.