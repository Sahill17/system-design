#### Liskov’s Substitution Principle (LSP)

Derived or child classes must be substitutable for their base or parent classes. Means any class that is the child of a parent class should be usable in place of its parent without any unexpected behaviour.

```java
// StreamingMovie can’t be watched in theaters
class Movie {
    public void watchInTheater() {
        // logic to buy a ticket and play in theater
    }
}

class TheatricalMovie extends Movie {
    @Override
    public void watchInTheater() {
        // theater playback logic here
    }
}

class StreamingMovie extends Movie {
    @Override
    public void watchInTheater() {
        throw new UnsupportedOperationException("Not available in theaters");
    }
}

```

If you force every `Movie` to support both in-theater and online playback, you’ll break Liskov when a streaming-only title can’t play in a theater, or a theatrical-only title can’t stream.

Because `StreamingMovie` and `TheatricalMovie` can’t honor all of `Movie`’s promises, substituting them breaks the system.

```java
// Each class only implements what it truly supports

interface Movie {
    String getTitle();
}

interface TheaterWatchable {
    void watchInTheater();    // only for theatrical releases
}

interface Streamable {
    void watchOnline();       // only for streaming titles
}

class TheatricalMovie implements Movie, TheaterWatchable {
    private final String title;
    TheatricalMovie(String title) { this.title = title; }
    public String getTitle() { return title; }
    public void watchInTheater() {
        // Logic here
    }
}

class StreamingMovie implements Movie, Streamable {
    private final String title;
    StreamingMovie(String title) { this.title = title; }
    public String getTitle() { return title; }
    public void watchOnline() {
        // Logic here
    }
}

```

Now your review system can handle any `Movie` subtype without unexpected failures, and each class upholds exactly the behavior it supports.