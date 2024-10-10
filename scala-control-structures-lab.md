# Scala Control Structures Lab: For Loops, For Comprehensions, and Ranges

## Objective

In this lab, you'll practice using Scala's control structures, specifically for loops, for comprehensions, and ranges. You'll start with basic examples and progress to more complex scenarios.

## Additional Resources

- [Scala Documentation on For Comprehensions](https://docs.scala-lang.org/tour/for-comprehensions.html)
- [Scala Documentation on Ranges](https://www.scala-lang.org/api/current/scala/collection/immutable/Range.html)

## Exercises

### 1. For Loop with Range Step

Create a for loop that prints even numbers from 2 to 10.

<details>
<summary>Reveal Solution</summary>

```scala
for (i <- 2 to 10 by 2) {
  println(i)
}
```
</details>

### 2. For Loop with Collection

Given the following list of fruits, use a for loop to print each fruit:

```scala
val fruits = List("apple", "banana", "cherry", "date")
```

<details>
<summary>Reveal Solution</summary>

```scala
for (fruit <- fruits) {
  println(fruit)
}
```
</details>

### 3. For Loop with Multiple Ranges

Create a for loop that prints the multiplication table for numbers 1 to 3.

<details>
<summary>Reveal Solution</summary>

```scala
for (i <- 1 to 3; j <- 1 to 3) {
  println(s"$i * $j = ${i * j}")
}
```
</details>

### 4. For Comprehension with Filtering

Given the following list of numbers, use a for comprehension to create a new list containing only the even numbers:

```scala
val numbers = List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

<details>
<summary>Reveal Solution</summary>

```scala
val evenNumbers = for {
  num <- numbers
  if num % 2 == 0
} yield num

println(evenNumbers)
```
</details>

### 5. Nested For Comprehension

Create a for comprehension that generates all possible pairs of numbers from two lists:

```scala
val list1 = List(1, 2, 3)
val list2 = List('a', 'b', 'c')
```

<details>
<summary>Reveal Solution</summary>

```scala
val pairs = for {
  num <- list1
  char <- list2
} yield (num, char)

println(pairs)
```
</details>

### 6. For Comprehension with Tuple Destructuring

Given a list of tuples representing names and ages, use a for comprehension to print only the names of people who are 18 or older:

```scala
val people = List(("Alice", 25), ("Bob", 17), ("Charlie", 30), ("David", 16))
```

<details>
<summary>Reveal Solution</summary>

```scala
for {
  (name, age) <- people
  if age >= 18
} println(name)
```
</details>

### 7. Complex For Comprehension

Create a for comprehension that generates a list of all prime numbers between 2 and 20. (Hint: You may want to create a helper function to check if a number is prime)

<details>
<summary>Reveal Solution</summary>

```scala
def isPrime(n: Int): Boolean = {
  if (n <= 1) false
  else if (n == 2) true
  else !(2 to Math.sqrt(n).toInt).exists(x => n % x == 0)
}

val primes = for {
  n <- 2 to 20
  if isPrime(n)
} yield n

println(primes)
```
</details>

## Conclusion

In this lab, you've practiced using Scala's for loops, for comprehensions, and ranges. You've progressed from simple loops to more complex comprehensions involving filtering, tuple destructuring, and custom logic. These control structures are powerful tools in Scala for working with collections and generating new data based on existing collections.

