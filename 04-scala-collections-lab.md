# Scala Collections Lab Exercise: Movie Rental System

In this lab, you'll work with Scala collections to build parts of a movie rental system. You'll use various collection types and practice converting between them.

## Scenario

You're developing a system for a movie rental company. The system needs to manage movies, customer rentals, and generate reports.

## Exercise

### 1. Creating and Using Lists

Start by creating a list of movies:

1. Create a `case class` named `Movie` with fields for `title: String`, `year: Int`, `genre: String`, and `director: String`.

<details>
<summary>Reveal Solution</summary>

```scala
case class Movie(title: String, year: Int, genre: String, director: String)
```
</details>

2. Create a `List` of at least 9 `Movie` objects, including some famous Bollywood movies.
    - Here's a list to help you:

      ```
      "Inception", 2010, "Sci-Fi", "Christopher Nolan"
      "The Shawshank Redemption", 1994, "Drama", "Frank Darabont"
      "Dilwale Dulhania Le Jayenge", 1995, "Romance", "Aditya Chopra"
      "3 Idiots", 2009, "Comedy-Drama", "Rajkumar Hirani"
      "Lagaan", 2001, "Drama", "Ashutosh Gowariker"
      "The Dark Knight", 2008, "Action", "Christopher Nolan"
      "Sholay", 1975, "Action-Adventure", "Ramesh Sippy"
      "Pulp Fiction", 1994, "Crime", "Quentin Tarantino"
      "Mughal-e-Azam", 1960, "Historical Drama", "K. Asif
      ```


<details>
<summary>Reveal Solution</summary>

```scala
val movies = List(
  Movie("Inception", 2010, "Sci-Fi", "Christopher Nolan"),
  Movie("The Shawshank Redemption", 1994, "Drama", "Frank Darabont"),
  Movie("Dilwale Dulhania Le Jayenge", 1995, "Romance", "Aditya Chopra"),
  Movie("3 Idiots", 2009, "Comedy-Drama", "Rajkumar Hirani"),
  Movie("Lagaan", 2001, "Drama", "Ashutosh Gowariker"),
  Movie("The Dark Knight", 2008, "Action", "Christopher Nolan"),
  Movie("Sholay", 1975, "Action-Adventure", "Ramesh Sippy"),
  Movie("Pulp Fiction", 1994, "Crime", "Quentin Tarantino"),
  Movie("Mughal-e-Azam", 1960, "Historical Drama", "K. Asif")
)
```
</details>

3. Print all movie titles.

<details>
<summary>Reveal Solution</summary>

```scala
println("All movie titles:")
movies.foreach(movie => println(movie.title))
```
</details>

4. Find and print the oldest movie in the list.

<details>
<summary>Reveal Solution</summary>

```scala
val oldestMovie = movies.minBy(_.year)
println(s"\nOldest movie: ${oldestMovie.title} (${oldestMovie.year})")
```
</details>

5. Create a new list containing only movies from the 21st century (year 2000 and later).

<details>
<summary>Reveal Solution</summary>

```scala
val modernMovies = movies.filter(_.year >= 2000)
println("\n21st century movies:")
modernMovies.foreach(movie => println(s"${movie.title} (${movie.year})"))
```
</details>

6. Print the number of movies for each genre in the list.

<details>
<summary>Reveal Solution</summary>

```scala
val genreCounts = movies.groupBy(_.genre).map { case (genre, movieList) => (genre, movieList.length) }
println("\nMovies per genre:")
genreCounts.foreach { case (genre, count) => println(s"$genre: $count") }
```
</details>

### 2. Working with Sets

The rental system needs to keep track of unique attributes:

1. Create a `Set` of all unique genres from the `movies` list.

<details>
<summary>Reveal Solution</summary>

```scala
val genres: Set[String] = movies.map(_.genre).toSet
```
</details>

2. Create another `Set` of all unique directors from the `movies` list.

<details>
<summary>Reveal Solution</summary>

```scala
val directors: Set[String] = movies.map(_.director).toSet
```
</details>

3. Print the number of unique genres and directors.

<details>
<summary>Reveal Solution</summary>

```scala
println(s"Number of unique genres: ${genres.size}")
println(s"Number of unique directors: ${directors.size}")
```
</details>

4. Find and print the genres that are not "Drama" or "Sci-Fi".

<details>
<summary>Reveal Solution</summary>

```scala
val otherGenres = genres -- Set("Drama", "Sci-Fi")
println(s"Genres other than Drama and Sci-Fi: $otherGenres")
```
</details>

5. Create a new `Set` that combines both unique genres and directors.

<details>
<summary>Reveal Solution</summary>

```scala
val combinedSet = genres ++ directors
println(s"Combined set size: ${combinedSet.size}")
```
</details>

6. Check if this combined `Set` contains "Christopher Nolan" and "Romance".

<details>
<summary>Reveal Solution</summary>

```scala
println(s"Contains Christopher Nolan: ${combinedSet.contains("Christopher Nolan")}")
println(s"Contains Romance: ${combinedSet.contains("Romance")}")
```
</details>

### 3. Using Maps for Movie Ratings and Reviews

Now, let's add user ratings and reviews to our movies:

1. Create a `Map` where the keys are movie titles and the values are `Double` ratings.

<details>
<summary>Reveal Solution</summary>

```scala
val ratings: Map[String, Double] = Map(
  "Inception" -> 8.8,
  "The Shawshank Redemption" -> 9.3,
  "Dilwale Dulhania Le Jayenge" -> 8.6,
  "3 Idiots" -> 8.4,
  "Lagaan" -> 8.1
)
```
</details>

2. Print the rating for "Inception" (or another movie in your list).

<details>
<summary>Reveal Solution</summary>

```scala
println(s"Rating for Inception: ${ratings("Inception")}")
```
</details>

3. Try to get the rating for a movie not in the map. Use `getOrElse` to return "Not rated" if the movie isn't found.

<details>
<summary>Reveal Solution</summary>

```scala
val shoLayRating = ratings.getOrElse("Sholay", "Not rated")
println(s"Rating for Sholay: $shoLayRating")
```
</details>

4. Create another `Map` where the keys are movie titles and the values are `List[String]` representing user reviews.

<details>
<summary>Reveal Solution</summary>

```scala
val reviews: Map[String, List[String]] = Map(
  "Inception" -> List("Mind-bending!", "Incredible visuals", "Confusing plot"),
  "Dilwale Dulhania Le Jayenge" -> List("Classic romantic film", "Shah Rukh and Kajol's chemistry is amazing", "Iconic scenes"),
  "3 Idiots" -> List("Funny and thought-provoking", "Great message about education", "Aamir Khan's brilliant performance")
)
```
</details>

5. Print all reviews for a specific movie.

<details>
<summary>Reveal Solution</summary>

```scala
println("Reviews for Dilwale Dulhania Le Jayenge:")
reviews("Dilwale Dulhania Le Jayenge").foreach(println)
```
</details>

6. Create a function that takes a movie title and returns a tuple of (rating, number of reviews).

<details>
<summary>Reveal Solution</summary>

```scala
def movieStats(title: String): (String, Int) = {
  val rating = ratings.getOrElse(title, "Not rated").toString
  val reviewCount = reviews.get(title).map(_.length).getOrElse(0)
  (rating, reviewCount)
}

val (ddljRating, ddljReviewCount) = movieStats("Dilwale Dulhania Le Jayenge")
println(s"DDLJ - Rating: $ddljRating, Number of reviews: $ddljReviewCount")
```
</details>

### 4. Converting Between Collections

To generate reports, we need to convert between collection types:

1. Convert the `List` of `Movie` objects to an `Array`.

<details>
<summary>Reveal Solution</summary>

```scala
val movieArray: Array[Movie] = movies.toArray
```
</details>

2. Create a `Vector` of all movie titles from this `Array`.

<details>
<summary>Reveal Solution</summary>

```scala
val movieTitles: Vector[String] = movieArray.map(_.title).toVector
```
</details>

3. Convert the `Vector` to a `Set` to get unique movie titles (in case of duplicates).

<details>
<summary>Reveal Solution</summary>

```scala
val uniqueTitles: Set[String] = movieTitles.toSet
println(s"Number of unique titles: ${uniqueTitles.size}")
```
</details>

4. Create a `Map` where the keys are years and the values are `List[String]` of movie titles released in that year.

<details>
<summary>Reveal Solution</summary>

```scala
val moviesByYear: Map[Int, List[String]] = movies.groupBy(_.year).map { case (year, movieList) => 
  (year, movieList.map(_.title))
}
```
</details>

5. Convert this `Map` to a `List` of tuples (year, number of movies).

<details>
<summary>Reveal Solution</summary>

```scala
val yearMovieCounts: List[(Int, Int)] = moviesByYear.map { case (year, movies) => 
  (year, movies.length)
}.toList
```
</details>

6. Sort this `List` by the number of movies in descending order.

<details>
<summary>Reveal Solution</summary>

```scala
val sortedYearMovieCounts = yearMovieCounts.sortBy(-_._2)
println("Years sorted by number of movies (descending):")
sortedYearMovieCounts.foreach { case (year, count) => println(s"$year: $count movie(s)") }
```
</details>

## Conclusion

In this lab, you've practiced using various Scala collections (List, Set, Map, Array, and Vector) in the context of a movie rental system. You've also converted between different collection types and performed various operations on these collections. These skills are fundamental for working with data in Scala applications.

Remember, each collection type has its strengths:
- `List` is great for sequential access
- `Set` for unique elements
- `Map` for key-value pairs
- `Array` and `Vector` for indexed access

Practice using these collections in your own projects to become more comfortable with Scala's powerful collection library.
