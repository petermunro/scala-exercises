# Six of the Best

These are an adaptation of the [99 Prolog Problems](https://sites.google.com/site/prologsite/prolog-problems) written by Werner Hett at the Berne University of Applied Sciences in Berne, Switzerland. Phil Gold altered them to be more amenable to programming in Scala.

1. Given a range of integers by its lower and upper limit, construct a list of all prime numbers in that range.

   ```scala
   scala> listPrimesinRange(7 to 31)
   res0: List[Int] = List(7, 11, 13, 17, 19, 23, 29, 31)
   ```

2. Lotto: draw N *different* random numbers from the set 1..M

3. If a list contains repeated, not necessarily contiguous, elements they should be replaced with a single copy of the element. The order of the elements should not be changed.

   ```scala
   scala> compress(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
   res0: List[Symbol] = List('a, 'b, 'c, 'a, 'd, 'e)
   ```

4. In financial documents, numbers must sometimes be written in full words. Example: 175 must be written as one-seven-five. Write a function `fullWords(num: Int)` to print (non-negative) integer numbers in full words.

5. Split a list into two parts. The length of the first part is given. Use a Tuple for your result.

   ```scala
   scala> split(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
   res0: (List[Symbol], List[Symbol]) = (List('a, 'b, 'c), List('d, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
   ```

6. Determine whether a given integer number is prime.

   ```scala
   scala> 7.isPrime
   res0: Boolean = true
   ```
