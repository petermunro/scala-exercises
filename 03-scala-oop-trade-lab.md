# Scala Object-Oriented Programming Lab: Trade Use Case

In this lab, we'll explore object-oriented programming in Scala using a Trade use case. We'll start with a basic Trade case class and build upon it to cover various OOP concepts.

## Exercise 1: Creating a Trade Case Class

Create a case class called `Trade` with the following specifications:

1. It should have fields for `id` (String), `symbol` (String), `quantity` (Int), and `price` (Double).
2. Use a case class to automatically get useful features like immutability, pattern matching, and default implementations of methods like `toString`, `equals`, and `hashCode`.

<details>
<summary>Reveal Solution</summary>

```scala
case class Trade(id: String, symbol: String, quantity: Int, price: Double)

// Usage
val trade1 = Trade("T1", "AAPL", 100, 150.25)
println(trade1)  // Output: Trade(T1,AAPL,100,150.25)
```
</details>

## Exercise 2: Adding Methods to the Trade Case Class

Enhance the `Trade` case class by adding the following methods:

1. `value`: Calculate the total value of the trade (quantity * price).
2. `isLargeTrade`: Return true if the trade value is over 1,000,000.
3. `adjustQuantity`: Return a new Trade with an adjusted quantity.

<details>
<summary>Reveal Solution</summary>

```scala
case class Trade(id: String, symbol: String, quantity: Int, price: Double) {
  def value: Double = quantity * price
  
  def isLargeTrade: Boolean = value > 1000000
  
  def adjustQuantity(newQuantity: Int): Trade = this.copy(quantity = newQuantity)
}

// Usage
val trade1 = Trade("T1", "AAPL", 100, 150.25)
println(trade1.value)  // Output: 15025.0
println(trade1.isLargeTrade)  // Output: false
val adjustedTrade = trade1.adjustQuantity(200)
println(adjustedTrade)  // Output: Trade(T1,AAPL,200,150.25)
```
</details>

## Exercise 3: Companion Object for Trade

Create a companion object for the `Trade` case class with the following features:

1. A method `apply` that creates a Trade with a generated ID.
2. A method `fromCSV` that creates a Trade from a CSV string.
3. A `unapply` method for pattern matching on the trade value.

<details>
<summary>Reveal Solution</summary>

```scala
import java.util.UUID

case class Trade(id: String, symbol: String, quantity: Int, price: Double) {
  def value: Double = quantity * price
}

object Trade {
  def apply(symbol: String, quantity: Int, price: Double): Trade = 
    new Trade(UUID.randomUUID().toString, symbol, quantity, price)
  
  def fromCSV(csv: String): Trade = {
    val parts = csv.split(",")
    Trade(parts(0), parts(1), parts(2).toInt, parts(3).toDouble)
  }
  
  def unapply(trade: Trade): Option[(String, Double)] = 
    Some((trade.symbol, trade.value))
}

// Usage
val trade1 = Trade("AAPL", 100, 150.25)  // ID is auto-generated
println(trade1)

val trade2 = Trade.fromCSV("T2,GOOGL,50,2500.75")
println(trade2)

trade1 match {
  case Trade(symbol, value) => println(s"Symbol: $symbol, Value: $value")
}
```
</details>

## Exercise 4: Extension Methods for Trade

In this exercise, we'll add extension methods to the `Trade` class using implicit classes for Scala 2. In Scala 3, the same use case is handled using extension methods. Complete the Scala 2 version, then research Scala 3 extension methods.

We want to add the following methods:

- A method `valueInEuros` that converts the trade value to Euros (assume 1 USD = 0.85 EUR).
- A method `summary` that returns a formatted string with trade details.

### Implicit Class for Trade Extensions (Scala 2)

In Scala 2, we use implicit classes to add extension methods to existing types.

1. Create an implicit class `TradeOps` in an object `TradeExtensions`.
2. Add the methods specified above into that object.
3. Test your solution.


<details>
<summary>Reveal Scala 2 Solution</summary>

```scala
case class Trade(id: String, symbol: String, quantity: Int, price: Double) {
  def value: Double = quantity * price
}

object TradeExtensions {
  implicit class TradeOps(trade: Trade) {
    def valueInEuros: Double = trade.value * 0.85
    
    def summary: String = 
      f"Trade ${trade.id} | ${trade.symbol}%5s | Qty: ${trade.quantity}%5d | Price: ${trade.price}%8.2f | Value: ${trade.value}%10.2f"
  }
}

// Usage
import TradeExtensions._

val trade = Trade("T1", "AAPL", 100, 150.25)
println(trade.valueInEuros)  // Output: 12771.25
println(trade.summary)  // Output: Trade T1 | AAPL | Qty:   100 | Price:   150.25 | Value:   15025.00
```
</details>

## Exercise 5: Trait for Tradable Assets

Create a trait called `Tradable` that the `Trade` case class will extend:

1. The trait should have an abstract method `marketValue`.
2. Implement the `marketValue` method in the `Trade` case class.
3. Create an object that can work with any `Tradable` asset.

<details>
<summary>Reveal Solution</summary>

```scala
trait Tradable {
  def marketValue: Double
}

case class Trade(id: String, symbol: String, quantity: Int, price: Double) extends Tradable {
  def value: Double = quantity * price
  override def marketValue: Double = value
}

object TradingSystem {
  def processTrade(tradable: Tradable): Unit = {
    println(s"Processing trade with market value: ${tradable.marketValue}")
  }
}

// Usage
val trade = Trade("T1", "AAPL", 100, 150.25)
TradingSystem.processTrade(trade)  // Output: Processing trade with market value: 15025.0
```
</details>

## Conclusion

In this lab, you've practiced creating and working with a `Trade` case class in Scala, covering various object-oriented programming concepts. You've explored case classes, companion objects, implicit classes for extensions, and traits. These exercises provide a solid foundation for working with trade-related data and operations, and set the stage for introducing inheritance (like EquityTrade and FXTrade) in future exercises.

The use of a case class for `Trade` provides many benefits out of the box, such as immutability and useful default method implementations. This approach aligns well with functional programming principles in Scala while still leveraging OOP concepts.
