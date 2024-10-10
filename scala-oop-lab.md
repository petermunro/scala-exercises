# Scala Object-Oriented Programming Lab

In this lab, you'll practice various aspects of object-oriented programming in Scala. We'll cover classes, fields, constructors, methods, `val` vs `def`, lazy val, operators, objects, and companion objects.

## Exercise 1: Creating a Basic Class

Create a class called `Book` with the following specifications:

1. It should have fields for `title` (String), `author` (String), and `yearPublished` (Int).
2. Create a constructor that initializes these fields.
3. Add a method called `getInfo` that returns a string with the book's information.

<details>
<summary>Reveal Solution</summary>

```scala
class Book(val title: String, val author: String, val yearPublished: Int) {
  def getInfo: String = s"$title by $author ($yearPublished)"
}

// Usage
val myBook = new Book("1984", "George Orwell", 1949)
println(myBook.getInfo)  // Output: 1984 by George Orwell (1949)
```
</details>

## Exercise 2: Val vs Def

Modify the `Book` class to include:

1. A `val` called `uniqueID` that generates a random ID when the book is created.
2. A `def` called `randomQuote` that returns a random quote each time it's called.

<details>
<summary>Reveal Solution</summary>

```scala
import scala.util.Random

class Book(val title: String, val author: String, val yearPublished: Int) {
  val uniqueID: String = Random.alphanumeric.take(8).mkString
  def randomQuote: String = {
    val quotes = List(
      "To be or not to be",
      "All that glitters is not gold",
      "The only way to do great work is to love what you do"
    )
    quotes(Random.nextInt(quotes.length))
  }
  
  def getInfo: String = s"$title by $author ($yearPublished)"
}

// Usage
val myBook = new Book("1984", "George Orwell", 1949)
println(myBook.uniqueID)  // Output: A random 8-character string
println(myBook.randomQuote)  // Output: A random quote
println(myBook.randomQuote)  // Output: Possibly a different random quote
```
</details>

## Exercise 3: Lazy Val

Add a `lazy val` to the `Book` class that simulates a time-consuming operation:

1. Create a `lazy val` called `complexAnalysis` that performs a "complex" analysis of the book.
2. This analysis should simply be a string that includes the book's title and the number of characters in the title, but pretend it's a heavy computation.

<details>
<summary>Reveal Solution</summary>

```scala
class Book(val title: String, val author: String, val yearPublished: Int) {
  // ... previous code ...
  
  lazy val complexAnalysis: String = {
    Thread.sleep(2000)  // Simulate a time-consuming operation
    s"Complex analysis of '$title': The title has ${title.length} characters."
  }
}

// Usage
val myBook = new Book("1984", "George Orwell", 1949)
println("Book created, but analysis not yet performed.")
println(myBook.complexAnalysis)  // This will take about 2 seconds to execute
println(myBook.complexAnalysis)  // This will return immediately
```
</details>

## Exercise 4: Operators

Implement a custom operator for the `Book` class:

1. Create a `+` operator that combines two books into a new `BookCollection` class.
2. The `BookCollection` class should have a list of books and a method to print all books.

<details>
<summary>Reveal Solution</summary>

```scala
class Book(val title: String, val author: String, val yearPublished: Int) {
  // ... previous code ...
  
  def +(other: Book): BookCollection = new BookCollection(List(this, other))
}

class BookCollection(val books: List[Book]) {
  def printBooks(): Unit = {
    books.foreach(book => println(book.getInfo))
  }
}

// Usage
val book1 = new Book("1984", "George Orwell", 1949)
val book2 = new Book("To Kill a Mockingbird", "Harper Lee", 1960)
val collection = book1 + book2
collection.printBooks()
```
</details>

## Exercise 5: Object and Companion Object

Create an object and a companion object for the `Book` class:

1. Create an object called `Library` that can store and retrieve books.
2. Create a companion object for `Book` that includes a method to create a book from a string.

<details>
<summary>Reveal Solution</summary>

```scala
object Library {
  private var books: List[Book] = List()
  
  def addBook(book: Book): Unit = {
    books = book :: books
  }
  
  def findBookByTitle(title: String): Option[Book] = {
    books.find(_.title == title)
  }
}

class Book(val title: String, val author: String, val yearPublished: Int) {
  // ... previous code ...
}

object Book {
  def apply(info: String): Book = {
    val parts = info.split(",")
    new Book(parts(0).trim, parts(1).trim, parts(2).trim.toInt)
  }
}

// Usage
val book1 = Book("The Great Gatsby, F. Scott Fitzgerald, 1925")
Library.addBook(book1)
Library.findBookByTitle("The Great Gatsby").foreach(book => println(book.getInfo))
```
</details>

## Conclusion

In this lab, you've practiced creating classes with various features in Scala, including different types of fields and methods, custom operators, and companion objects. You've also explored the differences between `val`, `def`, and `lazy val`. These concepts form the foundation of object-oriented programming in Scala.
